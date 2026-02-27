# Social Production

A community platform for organising collective projects, pooling resources, and building things together.

Post ideas, recruit members, schedule meetups, organise labor, and collectively fund shared goals — with collective ownership of the results.

## Table of Contents

- [Goals](#goals)
- [Technologies](#technologies)
- [Platforms](#platforms)
- [Architecture](#architecture)
  - [P2P Network](#p2p-network)
  - [Blockchain](#blockchain)
  - [Transactions](#transactions)
  - [Resource Management](#resource-management)
- [Governance](#governance)
  - [Roles](#roles)
  - [Voting Rules](#voting-rules)
- [Documentation](#documentation)

## Goals

Build a community-driven economic ecosystem that doesn't rely on the capitalist system. Through controlling the means of production, we control economic and political influences on our communities.

- Produce and distribute our own products
- Create organisational structures to support this
- Build a community-driven network using P2P technologies
- Provide community funding for projects and living conditions
- Automate the distribution of funding and project produce
- Build a communication system to discuss governance
- Provide for events driven by projects
- Location-based feed filtering to help users discover nearby projects
- Full transparency on all transactions (project changes, funding events, distributions, etc.)

## Technologies

| Layer | Technology |
|---|---|
| Backend | Rust |
| Frontend | Flutter |
| Communication | gRPC |
| Networking | P2P |
| Ledger | Blockchain + Merkle Trees |

## Platforms

- Desktop: Linux, Windows, macOS
- Web
- iOS
- Android

## Architecture

### P2P Network

Every app instance is a node on the network. A node server can run independently of the app UI. Nodes can act as gossip relays without downloading any assets.

### Blockchain

Only transactions live on the blockchain, stored in Merkle Trees. The full blockchain is always synced. A transaction is considered valid once verified by a minimum of 3 nodes.

### Transactions

Any change event on the platform is recorded as a transaction:

- User registered, edited, or unregistered
- Project posted, edited, or status changed
- Project update added, edited, or deleted
- Funding created, funded, or distributed
- Post created, updated, or deleted
- Comment added
- Event added, edited, or cancelled
- RSVP changes
- Votes cast
- Node added or removed

### Resource Management

Assets and content can be synced at a granular level:

- By time range
- By file size or available disk space
- On demand

## Governance

Projects are created by users. All members may propose rules for distribution, propose changes, and vote on proposals. Any user can join a project.

### Roles

**Manager**
- Edit the project
- Post updates
- Manage events
- Make and vote on proposals
- Create or edit collective funds
- Propose member promotions to manager

**Member**
- Make proposals
- Vote on proposals

### Voting Rules

- A proposal passes with **≥ 70% yes** votes
- A minimum of **20% of members** must vote for the result to count
- A vote is required to remove a manager (including the project creator)
- A vote is required to promote a member to manager

## Documentation

| Document | Description |
|---|---|
| [README.md](README.md) | Project overview, architecture, and governance summary |
| [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md) | System design: network and clients architecture |
| [PLAN.md](PLAN.md) | Full project plan, architecture details, and governance rules |
| [DATA.md](DATA.md) | Database schema, entity relationships, and diagrams |
