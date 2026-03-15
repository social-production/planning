# Social Production Technical Architecture

This document is the implementation-facing source of truth for the Social Production system architecture. It consolidates the architecture decisions that were previously split across [README.md](README.md), [PLAN.md](PLAN.md), [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md), [DATA.md](DATA.md), [LEGAL.md](LEGAL.md), and the planning drafts.

The goal of this document is to define how the platform should be built across the main stacks:

- Rust backend and node runtime
- Flutter clients
- P2P networking and sync
- Blockchain and transaction finality
- Data and storage
- Governance and legal integration

## 1. System Overview

Social Production is a peer-to-peer platform for organizing collective production, governance, funding, and distribution without relying on centralized application servers as the system authority.

The architecture is built around four rules:

1. The blockchain is the immutable record of platform change events.
2. The application state used by clients is derived from the blockchain and stored locally in query-friendly databases.
3. Assets and large content are distributed separately from the blockchain using content-addressed storage.
4. Governance decisions become real-world actions only when they are recorded on-chain and then executed by the legal stewarding entity.

## 2. Core Decisions

### 2.1 Stack

- Rust for the backend, node runtime, sync engine, and consensus logic
- Flutter for desktop, mobile, and web clients
- gRPC for communication between client applications and the local or remote node service
- P2P networking for peer discovery, transaction propagation, and content synchronization
- Merkle-based indexes for sync verification and content-state comparison
- Blockchain for ordered transaction history and final state verification

### 2.2 Node Model

Every app instance can connect to a node. A node may run inside the same device as the app or as a separate process.

Three node modes remain part of the design:

- Full: validates transactions, syncs the full blockchain, stores all application data while practical, and serves content to other peers
- Light: syncs the blockchain and query state, but downloads larger content and assets on demand
- Gossip: participates in discovery, transaction propagation, and limited sync without full content storage

Operational defaults:

- Mobile devices should default to Light mode
- Desktop devices may default to Light mode and allow an explicit switch to Full mode
- Dedicated always-on machines are the expected first high-availability Full nodes

### 2.3 Identity Model

Node identity and user identity are separate.

- node_id: the infrastructure identity used for peer discovery, routing, validation participation, and sync capabilities
- user_id: the application identity used for posting, voting, membership, and governance

A user may operate across multiple devices by transferring credentials to another device and attaching a new node identity to the same user identity.

This resolves the conflict in older notes that treated device identity as if it were the permanent user identity.

### 2.4 Storage Evolution

The storage model is:

1. Start with full nodes storing all blockchain data and all off-chain content that the current scale makes practical.
2. Keep light nodes on-demand from the beginning so low-resource devices are viable.
3. When full nodes storing all off-chain content becomes impractical, move off-chain content and asset storage to sharding plus replication.
4. Keep the blockchain fully synced across validating nodes even after off-chain storage becomes sharded.

This means sharding is a scale transition for content storage, not the base architecture for the network.

## 3. System Layers

### 3.1 Blockchain Layer

The blockchain stores ordered transactions and finality metadata. It does not store large assets or full query-ready documents.

Responsibilities:

- Accept signed transactions
- Order transactions into blocks or block-like batches
- Verify transaction authorization and state transitions
- Produce deterministic state changes
- Expose finalized history for replay and audit

### 3.2 Projection Database Layer

Each node maintains a local relational projection database derived from blockchain transactions.

Responsibilities:

- Provide efficient reads for feeds, projects, proposals, distributions, and profiles
- Materialize current state from transaction history
- Support indexing and filtering for app features
- Rebuild from blockchain history when needed

This layer is queryable state, not the system of record.

### 3.3 Content and Asset Layer

Assets, attachments, media, and other large blobs live outside the blockchain in content-addressed storage.

Responsibilities:

- Store blobs by content hash
- Deduplicate identical content
- Replicate content according to node mode and storage policy
- Support on-demand fetches for light nodes
- Transition to sharded plus replicated storage at larger scale

### 3.4 Client Layer

Flutter clients present the user interface and interact with a node service over gRPC.

Responsibilities:

- Read from local or attached node state
- Create signed intents and transactions
- Show pending, confirmed, and finalized states
- Handle offline usage and later reconciliation

## 4. Transaction Model

The current phrase “everything is a transaction” is too broad for implementation. The system should instead use explicit transaction families.

### 4.1 Transaction Families

- Identity: user registration, profile edits, account deactivation
- Membership: join post, role changes, manager promotion, manager removal
- Posts and projects: create post, edit post, change project status, post updates
- Content: comments, post content changes, updates, proposal content, event content
- Governance: create proposal, cast vote, close proposal, moderation action
- Funding: create fund drive, contribute funds, cancel fund drive, record withdrawal or distribution event
- Events: create event, edit event, cancel event, RSVP changes
- Products and distributions: create product, create distribution, update distribution status, attach digital delivery link
- Network: node registration, node capability updates, node removal

### 4.2 Transaction Shape

Each transaction should have the following fields:

- transaction_id
- transaction_type
- actor_id
- resource_type
- resource_id
- payload_version
- payload
- previous_state_hash when required for guarded updates
- timestamp
- signature

Each block or batch should have:

- block_id
- previous_block_hash
- ordered transaction list
- merkle_root
- proposer node id
- participating full-node signatures
- finalized_at

### 4.3 On-Chain and Off-Chain Boundary

On-chain:

- State-changing events
- Governance decisions and votes
- Membership and role changes
- Funding and distribution state changes
- References to off-chain content hashes
- Finality metadata

Off-chain:

- Large text bodies if they exceed practical transaction size limits
- Images, video, documents, and downloadable assets
- Query projections and local indexes
- Cached search and feed results

Rule: if an event changes platform state, the event is on-chain. If the payload is too large to belong in the chain, the hash and reference stay on-chain while the blob stays off-chain.

## 5. Consensus and Finality

The current repository says a transaction is valid when verified by a minimum of three nodes. The architecture discussions add two more important details: the project uses pBFT-style finality, and reputation affects which nodes are trusted by default when branches or bad actors appear.

### 5.1 Planning Default

The planning default is pBFT-style quorum finality using Full nodes. This does not require a separate permanent validator class.

- Transactions are broadcast to peers
- Full nodes validate transaction signatures, permissions, and state-transition rules
- A block or batch is finalized only after signatures from at least three distinct trusted Full nodes
- Finalized batches are appended to the local chain and applied to the projection database

In plain terms:

- Full nodes do the validation work
- pBFT-style quorum is the mechanism that turns validation into finality
- Reputation is the trust filter that decides which nodes are accepted by default when conflicts happen

### 5.2 Reputation and Trust

The network should maintain a reputation model tied to users and their nodes.

- New nodes start at the default trusted threshold
- Bad behavior lowers reputation
- Nodes following the default trust threshold discount or reject low-reputation votes during conflict resolution
- If a user lowers their own trust threshold and follows weaker peers, their own trust standing drops accordingly in the default network

This means reputation does not replace finality. It shapes whose validation counts as trustworthy in the default network view.

### 5.3 Validation Rules

Validation checks must include:

- Actor signature is valid
- Actor has permission to perform the action
- Target resource exists when required
- Status transition is legal
- Duplicate or replayed transaction is rejected
- Referenced off-chain content hash exists when required

### 5.4 Finality and Fork Handling

The initial implementation should prefer deterministic finality over long-lived forks.

- Nodes do not treat a transaction as final until the batch has quorum signatures
- Competing non-finalized branches may exist briefly during propagation
- If a node sees conflicting non-finalized branches, it follows the branch with valid quorum completion from trusted peers first
- Finalized history is authoritative for projection rebuilds and governance execution

This keeps the model close to the existing “3-node verification” rule while making the implementation boundary explicit: reputation helps determine trusted validation, and pBFT-style quorum produces finality.

## 6. Data and Storage Architecture

### 6.1 Source of Truth

- Blockchain: immutable ordered event log
- Projection database: current queryable application state
- Content-addressed storage: assets and large content blobs

### 6.2 Relational Projection Model

The relational model defined in [DATA.md](DATA.md) remains the basis for application reads, but it should be treated as a derived state model.

Tables and entities such as users, posts, proposals, fund drives, distributions, events, assets, and votes should all be updated by applying finalized blockchain transactions.

### 6.3 Merkle Indexes

Merkle indexes are used to:

- Detect chain or content-state divergence
- Verify sync correctness
- Compare known state between peers
- Support targeted sync instead of blind re-download

The Merkle index is not a replacement for either the chain or the relational projection.

### 6.4 Storage Scaling Path

Early scale:

- Full nodes keep the entire chain and full off-chain content set while practical
- Light nodes keep the chain and smaller local caches

Later scale:

- Full validating nodes still keep the full chain
- Off-chain blobs are partitioned across shards
- Each shard is replicated across multiple full-capacity storage peers
- Light nodes continue on-demand retrieval using content hashes and peer discovery

Video and large media are the primary storage pressure, so shard planning should be driven by blob storage growth rather than by the transaction ledger first.

### 6.5 Compression and Encoding Defaults

Compression should be selected by data type rather than applied as one global rule.

- Text and structured payloads: Zstandard for storage and backup compression
- Network transfer for text responses: Brotli when supported, gzip as fallback
- Images: transcode to WebP or AVIF where platform compatibility allows
- Video: use modern codecs such as H.265 or AV1 when processing cost is acceptable

The blockchain should store references and hashes, not compressed media blobs.

## 7. P2P Networking and Sync

### 7.1 Discovery

- Kademlia for remote peer discovery
- mDNS for local peer discovery
- Known peers stored locally and periodically health-checked

### 7.2 Propagation

The network should propagate two classes of data:

- Chain data: transactions, block candidates, finalized batches, and state proofs
- Blob data: assets and larger content addressed by hash

These should be handled separately so large content does not slow down transaction finality.

### 7.3 Sync Flow

Chain sync:

1. Compare chain height, finalized batch id, and Merkle root with peers.
2. Request missing finalized batches.
3. Verify quorum signatures and Merkle proofs.
4. Apply transactions to the local projection database.

Blob sync:

1. Compare locally available content hashes against referenced hashes.
2. Download missing blobs according to node mode and storage policy.
3. Verify content hashes before marking blobs available.

### 7.4 Mode-Specific Behavior

Full mode:

- Validates transactions
- Participates in quorum finality
- Serves chain data and blob data
- Stores full query state

Light mode:

- Syncs finalized chain and query state
- Requests blobs on demand
- May cache recent or user-relevant content only

Gossip mode:

- Participates in discovery and propagation
- May keep partial chain state depending on implementation limits
- Does not need to serve the full blob set

## 8. Service Boundaries and gRPC

Flutter clients should not talk directly to chain storage internals. They should interact with a node service.

### 8.1 Service Groups

- Identity service
- Feed and post service
- Governance service
- Funding service
- Event service
- Distribution service
- Sync status service
- Asset service
- Node admin service

### 8.2 gRPC Responsibilities

gRPC should handle:

- Query requests against projection state
- Transaction submission
- Upload and download coordination for assets
- Sync and health status
- Local node configuration and mode inspection

### 8.3 API Direction

The first protobuf definitions should be designed around transaction submission plus read models, not around direct table mutation.

That keeps the client aligned with the event-driven architecture.

## 9. Stack Implementation Plans

### 9.1 Rust Backend and Node Runtime

Primary modules:

- Node process bootstrap
- Peer discovery and peer registry
- Transaction validator
- Batch builder and finality coordinator
- Chain storage engine
- Projection database applier
- Blob storage manager
- gRPC service host
- Local configuration and node-mode manager

Implementation order:

1. Node bootstrap and configuration
2. Chain storage and transaction schema
3. Validation and finality pipeline
4. Projection applier
5. gRPC read and submit endpoints
6. Blob storage and on-demand retrieval
7. Mode-specific behavior controls

### 9.2 Flutter Clients

Primary responsibilities:

- Authentication and local identity handling
- Feed, project, governance, funding, and distribution views
- Transaction composition and signing
- Pending versus finalized state presentation
- Offline-first interaction with later sync
- Asset upload and on-demand media loading

Implementation order:

1. Local app shell and navigation
2. gRPC client integration
3. Read-model screens from projection state
4. Transaction submission flows
5. Pending-state UX
6. Offline cache and reconciliation behavior

### 9.3 P2P Networking and Sync Layer

Primary responsibilities:

- Peer discovery
- Peer health checks
- Chain propagation
- Finalized batch sync
- Blob lookup and retrieval
- Merkle proof verification
- Replay and recovery flows

Implementation order:

1. Discovery and peer registry
2. Chain synchronization
3. Batch propagation and validation relay
4. Blob propagation and retrieval
5. Divergence detection and recovery

### 9.4 Blockchain and Finality Layer

Primary responsibilities:

- Transaction schema and serialization
- Signature verification
- Authorization checks
- Deterministic state transitions
- Quorum-finality signatures
- Replay protection

Implementation order:

1. Transaction family definitions
2. Batch structure and merkle root generation
3. Validator signature flow
4. Finality checks and branch resolution
5. Rebuild-from-chain tooling

### 9.5 Data and Storage Layer

Primary responsibilities:

- Relational schema refinement
- Projection rebuilds
- Secondary indexes for feed and governance queries
- Blob metadata tracking
- Retention and cache rules
- Sharding transition planning for large-scale blobs

Implementation order:

1. Map each entity in [DATA.md](DATA.md) to transaction families
2. Define projection update rules
3. Add indexes for expected query patterns
4. Add blob metadata and replication tracking
5. Plan shard metadata for later scale

### 9.6 Governance and Legal Integration

Primary responsibilities:

- Proposal encoding
- Vote capture and tally rules
- Finalized governance result records
- Foundation execution queue for real-world actions
- Audit trail linking on-chain decision to off-chain execution

Implementation order:

1. Define proposal transaction types
2. Define vote and tally transactions
3. Define execution status records for legal or financial actions
4. Define review and audit queries

## 10. Governance and Legal Execution

The foundation is not a control hub for the network. It is the legal steward for real-world assets and obligations.

The execution model is:

1. Users create proposals and vote through the application.
2. Governance transactions are finalized on-chain.
3. The finalized result creates an execution record for actions that require legal or financial handling.
4. The foundation executes only what the finalized governance record authorizes.
5. The execution result is recorded back into the system as a new transaction or linked audit record.

This keeps platform governance inside the protocol while still handling bank accounts, property, and similar external assets lawfully.

## 11. Security and Failure Model

The first implementation should explicitly defend against:

- Replay of old transactions
- Unauthorized edits or role changes
- Double-voting
- Invalid state transitions
- Blob tampering through hash mismatch
- Nodes advertising data they cannot actually provide
- Temporary network partitions

Basic requirements:

- Signed transactions
- Content-hash verification for blobs
- Permission checks on every state-changing action
- Deterministic validation rules across full nodes
- Rebuildable projection state from finalized history

## 12. Delivery Phases

### Phase 1

- Finalize transaction families
- Finalize batch and finality format
- Build Rust node bootstrap, chain store, and projection applier
- Build Flutter read-only shell against mocked or local data

### Phase 2

- Add transaction submission flows
- Add governance, funding, and event paths
- Add light-node blob retrieval
- Add sync health and recovery tooling

### Phase 3

- Harden validation and conflict handling
- Optimize indexing and projection queries
- Add blob replication controls
- Measure when full-node blob storage becomes impractical

### Phase 4

- Introduce sharded plus replicated blob storage
- Keep the finalized chain and governance model stable
- Add shard placement, replication policy, and recovery procedures

## 13. Immediate Next Documents

This document should be followed by more specific implementation documents in this order:

1. Transaction specification
2. gRPC and protobuf specification
3. Projection-database rules and indexes
4. Sync protocol specification
5. Blob replication and sharding specification

## 14. Relationship to Existing Docs

- [README.md](README.md) stays the high-level project summary.
- [PLAN.md](PLAN.md) stays the broad planning document.
- [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md) remains a supporting workflow and diagram reference.
- [DATA.md](DATA.md) remains the domain and schema reference.
- [LEGAL.md](LEGAL.md) remains the legal summary.
- The DRAFTS folder remains supporting product and governance material.

Where this document and older summaries differ, this document should be treated as the architecture baseline for implementation work.