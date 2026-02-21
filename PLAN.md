# Social Production

A community platform for organising collective projects, pooling resources, and building things together.

Post ideas, recruit members, schedule meetups, organize labor and collectively fund shared goals, with collective ownership of the results.

## Technologies used

- Rust
- Flutter
- GRPC
- P2P
- Blockchain
- Merkle Tree

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
- Geofence projects and users to help with the distribution at a local level
- Offer full transparency on all transactions (project changes, funding events, distributions, etc.) made

## Architecture

- P2P Network
  - Each app is a node on the network
  - A node server can be independent of running the app
  - A node can act as a gossip without downloading any assets
  - Syncing will be done using a blockchain
- Blockchain
  - Only transactions live in the blockchain
  - Transactions live in Merkle Trees as storage
  - Synching will always sync all of the blockchain
  - A transaction will be considered valid if the blockchain has been verified by a minimum of 3 nodes
- Transaction
  - A transaction can be any change event that has happened on the platform. For example:
    - A user was:
      - Registered
      - Edited
      - Unregistered
    - An Organization was:
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
    - Can make a member a manager
  - Member
    - Can make proposals
    - Can vote on proposals
- Voting rules
  - A threshold of 70% must be yes for a vote to pass
  - A minimum of 20% of the members must vote for a vote to pass
  - A vote must be passed to remove a manager (e.g. the creator of the project)
  - A vote must be passed to promote a member to a manager
