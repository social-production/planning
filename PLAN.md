# Social Production Plan

A community platform for organising collective projects, pooling resources, and building things together.

Post ideas, recruit members, schedule meetups, organize labor and collectively fund shared goals, with collective ownership of the results.

## Technologies used

- Rust
- Flutter
- GRPC
- P2P
- Blockchain
- Merkle-based indexes for verification and sync comparison

## Platforms supported

- Desktop
  - Linux
  - Windows
  - Mac OS
- Web
- IOS
- Android

## Goals

Create an community driven economic ecosystem that doesn't rely on the capitalist system. Through controlling the means of production, we control economic and political influences on our communities.

### Steps to achieve this

- Produce and distribute our own products
- Create organizational structures to support this
- Build a community driven network using P2P technologies
- Provide community funding for:
  - Projects
  - Living conditions
- Automate the distributions of funding and project produce
- Build a communication system to discuss the governance
- Provide for events driven by projects
- Location-based feed filtering to help users discover nearby projects
- Offer full transparency on all transactions (project changes, funding events, distributions, etc.) made

## Architecture

- P2P Network
  - Each app is a node on the network
  - A node server can be independent of running the app
  - A node can act as a gossip without downloading any assets
  - Syncing uses the blockchain for ordered transaction history and verification
- Blockchain
  - The blockchain stores ordered transactions and finality metadata
  - Large assets and content live outside the blockchain
  - Validating nodes sync the blockchain while off-chain data can be fetched separately
  - Merkle-based indexes are used to compare state and verify sync efficiently between nodes
  - The exact finality model is defined in [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md)
- Transaction
  - A transaction can be any change event that has happened on the platform. For example:
    - A user was:
      - Registered
      - Edited
      - Unregistered
    - A Project was:
      - Posted
      - Edited
      - Status changed
    - A Project update was:
      - Added
      - Edited
      - Deleted
    - Funding for a project was:
      - Created
      - Funded
      - Distributed
    - A Post was:
      - Created
      - Updated
      - Deleted
    - A Comment was added
    - An event was:
      - Added
      - Edited
      - Cancelled
    - RSVP changes
    - Any votes that happen
    - A node was added
    - A node was removed
- Resource usage is controllable
  - Assets can be synced at a granular level
    - Sync based on a time range
    - Sync based on file size or disk availability
    - Sync on demand
  - Content can be synced at a granular level
    - Sync based on a time range
    - Sync based on file size or disk availability
    - Sync on demand
  - Merkle-based indexes can be compared between nodes to detect missing or mismatched state during sync

## Governance

- A project is created by a user
- All members of a project can:
  - Propose rules for distribution
  - Propose changes to the project
  - Vote on proposal
- All users can join a project and become a member
- Project members are given a role:
  - Manager
    - Can edit
    - Can post updates
    - Can manage events
    - Can make proposals
    - Can vote on proposals
    - Can create or edit project collective funds
    - Can make a proposal to make a member a manager
  - Member
    - Can make proposals
    - Can vote on proposals
- Voting rules
  - Members can vote yes, no, or abstain on competing proposals independently
  - Outcomes are based on broad support and participation thresholds rather than only a fixed yes-percentage rule
  - Participation thresholds scale with project size
  - A passed vote is required to remove a manager
  - A passed vote is required to promote a member to manager

For the current governance direction, use [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md).
