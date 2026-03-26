# Social Production

A community platform for organising collective projects, pooling resources, and building things together.

Post ideas, recruit members, schedule meetups, organise labor, and collectively fund shared goals — with collective ownership of the results.

## New Contributors

If you want to get up to speed quickly and start helping, begin here:

1. [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md)
2. [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md)

Use the guide to understand the repo structure, source-of-truth documents, and the best first contribution paths.

## Table of Contents

- [New Contributors](#new-contributors)
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
| Ledger | Blockchain + Merkle-based verification |

## Platforms

- Desktop: Linux, Windows, macOS
- Web
- iOS
- Android

## Architecture

This summary is intentionally high level. For the current implementation-facing direction, use [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md).

### P2P Network

Every app instance is a node on the network. A node server can run independently of the app UI. Nodes can act as gossip relays without downloading any assets.

### Blockchain

The blockchain stores ordered transaction history and finality metadata, not large assets or full query-ready documents. The full blockchain is expected to sync across validating nodes. Merkle-based verification is used to compare and validate transaction or content state efficiently during sync. Finality details are defined in [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md).

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

Large content and assets live outside the blockchain and are referenced separately.

Merkle-based indexes support sync verification and content-state comparison between nodes, but they do not replace the blockchain as the authoritative record.

### Resource Management

Assets and content can be synced at a granular level:

- By time range
- By file size or available disk space
- On demand

## Governance

Projects are created by users. All members may propose rules for distribution, propose changes, and vote on proposals. Any user can join a project.

The governance summary below is intentionally high level. For current planning details, use [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md).

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

- Members can vote yes, no, or abstain on competing proposals independently.
- Outcomes are based on broad support and participation thresholds, not just the highest raw vote total.
- Participation thresholds scale with project size.
- Role changes such as promoting or removing managers require a passed vote.

## Documentation

| Document | Description |
|---|---|
| [README.md](README.md) | Project overview, architecture, and governance summary |
| [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md) | Fast onboarding guide for new contributors |
| [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md) | Working draft for governance, production, and distribution operations |
| [DRAFTS/LEGAL.md](DRAFTS/LEGAL.md) | Working draft for legal structure and asset stewardship |
| [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md) | Primary implementation-facing architecture and stack plan |
| [ARCHITECTURE/SYSTEM_DESIGN.md](ARCHITECTURE/SYSTEM_DESIGN.md) | System design: network and clients architecture |
| [PLAN.md](PLAN.md) | Full project plan, architecture details, and governance rules |
| [ARCHITECTURE/DATA.md](ARCHITECTURE/DATA.md) | Database schema, entity relationships, and diagrams |
| [OUTREACH/PITCH_PAGE.md](OUTREACH/PITCH_PAGE.md) | Public-facing pitch and summary document |
