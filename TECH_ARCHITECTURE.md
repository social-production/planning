# Social Production Technical Architecture

This document is the implementation-facing source of truth for the Social Production system architecture. It consolidates the architecture decisions that were previously split across [README.md](README.md), [PLAN.md](PLAN.md), [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md), [DATA.md](DATA.md), [LEGAL.md](LEGAL.md), and the planning drafts.

The goal of this document is to define how the platform should be built across the main stacks:

- Rust backend and node runtime
- Flutter clients
- P2P networking and sync
- Blockchain and transaction finality
- Data and storage
- Governance and legal integration

## System Overview

Social Production is a peer-to-peer platform for organizing collective production, governance, funding, and distribution without relying on centralized application servers as the system authority.

The architecture is built around four rules:

1. The blockchain is the immutable record of platform change events.
2. The application state used by clients is derived from the blockchain and stored locally in query-friendly databases.
3. Assets and large content are distributed separately from the blockchain using content-addressed storage.
4. Governance decisions become real-world actions only when they are recorded on-chain and then executed by the legal stewarding entity.

## Core Decisions

### Stack

- Rust for the backend, node runtime, sync engine, and consensus logic
- Flutter for desktop, mobile, and web clients
- gRPC for communication between client applications and the local or remote node service
- P2P networking for peer discovery, transaction propagation, and content synchronization
- Merkle-based indexes for sync verification and content-state comparison
- Blockchain for ordered transaction history and final state verification

### Node Model

Every app instance can connect to a node. A node may run inside the same device as the app or as a separate process. The node **must** be run locally; only node to node communication is supported for remote synching.

Three node modes remain part of the design:

- Full: validates transactions, syncs the full blockchain, stores all application data while practical, and serves content to other peers
- Light: syncs the blockchain and query state, but downloads content and assets on demand
- Gossip: participates in discovery, transaction propagation, and limited sync without content storage

Operational defaults:

- Mobile devices should default to Light mode and allow an explicit switch to Full mode
- Desktop devices may default to Full mode and allow an explicit switch to Light mode
- Dedicated always-on machines are the expected first high-availability Full nodes

### Identity Model

Node identity and user identity are separate.

- node_id: the infrastructure identity used for peer discovery, routing, validation participation, and sync capabilities
- user_id: the application identity used for posting, voting, membership, and governance

A user may operate across multiple devices by transferring credentials to another device and attaching a new node identity to the same user identity.

This resolves the conflict in older notes that treated device identity as if it were the permanent user identity.

### Storage Evolution

The storage model is:

1. Start with full nodes storing all blockchain data and all off-chain content that the current scale makes practical.
2. Keep light nodes on-demand from the beginning so low-resource devices are viable.
3. When full nodes storing all off-chain content becomes impractical, move off-chain content and asset storage to sharding plus replication.
4. Keep the blockchain fully synced across validating nodes even after off-chain storage becomes sharded.

This means sharding is a scale transition for content storage, not the base architecture for the network.

## System Layers

### Blockchain Layer

The blockchain stores ordered transactions and finality metadata. It does not store large assets or full query-ready documents.

Responsibilities:

- Accept signed transactions
- Order transactions into blocks or block-like batches
- Verify transaction authorization and state transitions
- Produce deterministic state changes
- Expose finalized history for replay and audit

This is the remote record of changes over time across the network.

### Database Layer

Each node maintains a local relational database. This is the local source of truth.

Responsibilities:

- Provide efficient reads for feeds, projects, proposals, distributions, and profiles
- Materialize current state from transaction history
- Support indexing and filtering for app features
- Rebuild from blockchain history when needed

This layer is the local system of record.

### Content and Asset Layer

Data, assets, and media live outside the blockchain in content-addressed storage.

Responsibilities:

- Store data by content hash
- Replicate content according to node mode and storage policy
- Support on-demand fetches for light nodes
- Transition to sharded plus replicated storage at larger scale

### Client Layer

Flutter clients present the user interface and interact with a node service over gRPC.

Responsibilities:

- Communicates with the local node state
- Acts as an interface for users to interact with the node

## Blockchain Model

### Block Creation

- Nodes have a 1 minute window in which transactions can be created
- Nodes cycle this window every 1 minute
- If a node has transactions within that 1 minute time window, a block is created with those transaction and transmitted to their Full node peers

### Transaction Model

Each transaction should have the following fields:

- transaction_id: string
- node_id: string
- user_id: string
- content_tree: string
- timestamp: timestamp in unix format
- signature: string

### Block Model

Each block should have the following fields:

- originating_node_id: string
- block_hash: string
- previous_block_hash: string
- transactions: list of transaction
- signature: string
- transactions_hash: string
- peer_signatures: list of peer_signature

### Peer Signature Model

A peer signature has the following fields:

- node_id: string
- signature: string

### On-Chain and Off-Chain Boundary

On-chain:

- Record that data has changed

Off-chain:

- Actual data changes

## Consensus and Finality

The current repository says a transaction is valid when verified by a minimum of three nodes. The architecture discussions add two more important details: the project uses pBFT-style finality, and reputation affects which nodes are trusted by default when branches or bad actors appear.

### Planning Default

The planning default is pBFT-style quorum finality using Full nodes. This does not require a separate permanent validator class.

A quorom consists of at least 2/3 of known Full peers in network; with a minimum of 3 for the smallest network.

When a block has been created:

- The block is transferred to peers for votes
- Full node peers validate signatures
- Full node peers ensure the previous_block_hash correctly points to a valid block
- Full node peers sign the transactions and append their signature to the block peer_signatures
- Full node peers transfer the block to their Full node peers minus peers that have already signed the block

Once at least a quorum of Full node peers have signed a block and the peers that have signed pass a reputation validation:

- The block is transferred to all remaining peers and is considered part of the blockchain
- Full node peers sync with node ids in the transaction to update local data

If there is a conflict between two blocks that are fully validated:

- Both blocks are kept until a future round of block validation provides a clear winner
- The losing block is discarded

In plain terms:

- Full nodes do the validation work
- pBFT-style quorum is the mechanism that turns validation into finality
- Reputation is the trust filter that decides which nodes are filtered out by default

### Reputation and Trust

The network should maintain a reputation model tied to users and their nodes.

- New nodes start at the default trusted threshold
- Bad behavior lowers reputation
- Nodes following the default trust threshold discount or reject low-reputation votes
- If a user lowers their own trust threshold and follows weaker peers, their own trust standing drops accordingly in the default network

This means reputation does not replace finality. It shapes whose validation counts as trustworthy in the default network view.

### Validation Rules

Validation checks must include:

- The user signature is valid
- The transactions_hash is a valid hash of all transactions
- The previous_block_hash points to:
  - An actual previously validated block_hash
  - Or, a previously contested block_hash

### Finality and Fork Handling

The initial implementation should prefer deterministic finality over long-lived forks.

- Nodes do not treat a transaction as final until the block has quorum peer signatures
- Competing non-finalized branches may exist briefly during propagation
- If there is a conflict between two blocks that are fully validated:
  - Both blocks are kept until a future round of block validation provides a clear winner
  - The losing block is discarded
- If a node sees conflicting finalized branches, it follows the branch with valid quorum completion from trusted (e.g. reputation filter based) peers first
- Finalized history is authoritative for database rebuilds and governance execution

This keeps the model close to the existing “3-node verification” rule while making the implementation boundary explicit: reputation helps determine trusted validation, and pBFT-style quorum produces finality.

## Data and Storage Architecture

### Source of Truth

- Blockchain: immutable ordered event log
- Local Database: local application state

### Relational Projection Model

The relational model defined in [DATA.md](DATA.md) remains the basis for the application.

Changes triggered notated through the blockchain should trigger syncs with peers to update the relational data only.

### Merkle Indexes

Merkle indexes are used to:

- Detect content-state divergence
- Verify sync correctness
- Compare known state between peers
- Support targeted sync instead of blind re-download

The Merkle index is not a replacement for either the blockchain or the relational database structure.

### Storage Scaling Path

Early scale:

- Full nodes keep the entire blockchain, local caches, and sharded off-chain content
- Light nodes keep the blockchain and local caches
- Each shard is replicated across multiple Full node peers

### 6.5 Compression and Encoding Defaults

Compression should be selected by data type rather than applied as one global rule.

- Text and structured payloads: Zstandard for storage and backup compression
- Network transfer for text responses: Brotli when supported, gzip as fallback
- Images: transcode to WebP or AVIF (for GIFs)
- Video: use H.265
- Audio: use FLAC

## P2P Networking and Sync

### Discovery

- Kademlia for remote peer discovery
- mDNS for local peer discovery
- Known peers stored locally and periodically health-checked

### Propagation

The network should propagate two classes of data:

- Blockchain: transactions which have merkle trees of the data
- Data: all the actual data

These should be handled separately so large content does not slow down transaction finality.

### Sync Flow

Blockchain sync:

1. Compare last block with peers
2. Request missing finalized blocks
3. Verify quorum signatures
4. Apply transactions to the local database

Data sync:

1. Build merkle tree from last block transactions applied in sequence by timestamp
2. Compare current merkle tree root hash to new merkle tree
3. Download missing data (as noted by missing merkle tree hashes) from peers
4. Apply data to local database and storage

### Mode-Specific Behavior

Full mode:

- Validates transactions
- Participates in quorum finality
- Serves blockchain and data

Light mode:

- Syncs finalized blockchain and local data
- Requests data on demand
- Caches recent local and downloaded data

Gossip mode:

- Participates in discovery and propagation

## Service Boundaries and gRPC

Clients talk only to the local node

### gRPC Responsibilities

gRPC should handle:

- Query requests against local database
- Local node configuration and mode inspection

### API Direction

The API should only expose local database operations. All creative, modifying, or destructive database operations create transactions in the node.

## Stack Implementation Plans

### Rust Backend and Node Runtime

Primary modules:

- Node process bootstrap
- Peer discovery and peer registry
- Transaction validator
- Batch builder and finality coordinator
- Blockchain engine
- Database controller
- Storage manager
- gRPC service host
- Local configuration and node-mode manager

Implementation order:

1. Node bootstrap and configuration
2. Blockchain schema
3. Validation and finality pipeline
4. Database controller
5. gRPC endpoints
6. Storage and on-demand retrieval
7. Mode-specific behavior controls

### Flutter Clients

Primary responsibilities:

- Feed, project, governance, funding, and distribution views
- Blockchain and network presentation
- Asset upload and on-demand media loading

Implementation order:

1. Local app shell and navigation
2. gRPC client integration
3. UI Views

### P2P Networking and Sync Layer

Primary responsibilities:

- Peer discovery
- Peer health checks
- Blockchain propagation
- Finalized block sync
- Data lookup and retrieval
- Merkle proof verification

Implementation order:

1. Discovery and peer registry
2. Blockchain synchronization
3. Block propagation and validation relay
4. Data propagation and retrieval
5. Divergence detection and recovery

### Blockchain and Finality Layer

Primary responsibilities:

- Verification
- Authorization checks
- Deterministic state transitions
- Quorum-finality signatures
- Replay protection

Implementation order:

1. Verification rules
2. Block structure
3. Validator signature flow
4. Finality checks and branch resolution

### Data and Storage Layer

Primary responsibilities:

- Relational schema refinement

Implementation order:

1. Define Database rules

### Governance and Legal Integration

Primary responsibilities:

- Proposal encoding
- Vote capture and tally rules
- Finalized governance result records
- Foundation execution queue for real-world actions
- Audit trail linking on-chain decision to off-chain execution

Implementation order:

1. Define proposal types
2. Define vote and tally transactions
3. Define execution status records for legal or financial actions
4. Define review and audit queries

## Governance and Legal Execution

The foundation is not a control hub for the network. It is the legal steward for real-world assets and obligations.

The execution model is:

1. Users create proposals and vote through the application.
2. Governance transactions are finalized on-chain.
3. The finalized result creates an execution record for actions that require legal or financial handling.
4. The foundation executes only what the finalized governance record authorizes.
5. The execution result is recorded back into the system as a new transaction or linked audit record.

This keeps platform governance inside the protocol while still handling bank accounts, property, and similar external assets lawfully.

## Security and Failure Model

The first implementation should explicitly defend against:

- Replay of old transactions
- Unauthorized edits or role changes
- Double-voting
- Invalid state transitions
- Data tampering through hash mismatch
- Nodes advertising data they cannot actually provide
- Temporary network partitions

Basic requirements:

- Signed transactions
- Content-hash verification for data
- Permission checks on every state-changing action
- Deterministic validation rules across full nodes
- Rebuildable database state from finalized history

## Delivery Phases

### Phase 1

- Finalize block and finality format
- Build Rust node bootstrap, blockchain store, and projection applier
- Build Flutter client against mocked or local data

### Phase 2

- Add transaction submission flows
- Add governance, funding, and event paths
- Add light-node data retrieval
- Add sync health tooling

### Phase 3

- Harden validation and conflict handling
- Optimize indexing and projection queries
- Add data replication controls

### Phase 4

- Keep the finalized blockchain and governance model stable
- Add shard placement and replication policy procedures

## 13. Immediate Next Documents

This document should be followed by more specific implementation documents in this order:

1. Transaction specification
2. gRPC and protobuf specification
3. Projection-database rules and indexes
4. Sync protocol specification
5. Data replication and sharding specification

## Relationship to Existing Docs

- [README.md](README.md) stays the high-level project summary.
- [PLAN.md](PLAN.md) stays the broad planning document.
- [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md) remains a supporting workflow and diagram reference.
- [DATA.md](DATA.md) remains the domain and schema reference.
- [LEGAL.md](LEGAL.md) remains the legal summary.
- The DRAFTS folder remains supporting product and governance material.

Where this document and older summaries differ, this document should be treated as the architecture guide for implementation work.
