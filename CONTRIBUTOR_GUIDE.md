# Social Production Contributor Guide

This guide is the fastest way to understand what Social Production is, what is already decided, and where to start contributing.

Use this guide first. Then open [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md) and pick one focused item.

## What Social Production Is

Social Production is an open source platform for organizing collective production, governance, funding, and distribution outside market relations.

In practical terms, the project is trying to build software that helps communities:

- create projects for things like food, housing, care, tools, and free software
- coordinate work and discussion
- pool resources without private ownership claims
- govern decisions collectively
- distribute outputs by need rather than by exchange

The public-facing summary is in [OUTREACH/PITCH_PAGE.md](OUTREACH/PITCH_PAGE.md).

## What Is Decided And What Is Still Draft

Some documents are stable enough to work from today. Others are still being finalized.

### Stable enough to work from

- [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md): current implementation-facing architecture direction
- [APPLICATION/README.md](APPLICATION/README.md): application planning rules and source-of-truth structure
- [APPLICATION/APP_FLOW_OVERVIEW.md](APPLICATION/APP_FLOW_OVERVIEW.md): how app planning should be translated into screens
- [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md): current priority list

### Still draft, but important

- [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md): operating model, roles, project lifecycle, distribution rules
- [DRAFTS/LEGAL.md](DRAFTS/LEGAL.md): foundation and stewardship model

### Still open or unsettled

- final moderation scope in the operations model
- final legal jurisdiction for the foundation
- cleanup of older summaries in [README.md](README.md) and [PLAN.md](PLAN.md) so they fully match the newer drafts

If two documents conflict, prefer the newer, more specific planning document over the older summary.

## Repository Map

The organization is split into multiple repos. You do not need to understand everything before helping.

### Start here

- [README.md](README.md): high-level overview of the planning repo
- [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md): current priorities
- [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md): technical direction

### Main repos

- `planning/`: source of truth for architecture, operations, legal, outreach, and app/page planning
- `network/`: Rust peer-to-peer node, blockchain, sync, and terminal UI work
- `app/`: Flutter client track; the app is still close to a starter shell, so planning docs matter more than current UI state
- `web/`: older React prototype and wireframes; useful as reference material, not the main product direction
- `assets/`: logos, app icons, and reusable brand assets
- `proto/`: reserved for protobuf and gRPC contract work
- `migrations/`: migration-related repo for future data evolution work
- `accounting/`: separate workspace area, not the current entry point for most new contributors

## Reading Order

If you are new, read in this order:

1. [README.md](README.md)
2. [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md)
3. [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md)
4. [OUTREACH/PITCH_PAGE.md](OUTREACH/PITCH_PAGE.md)
5. [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md)

Then follow the track that fits how you want to contribute.

## Contribution Tracks

### Planning and documentation

Best if you want to clarify the model, improve docs, resolve contradictions, or turn ideas into implementation-ready guidance.

Read next:

- [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md)
- [DRAFTS/LEGAL.md](DRAFTS/LEGAL.md)
- [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md)

Good first work:

- tighten language in canonical docs
- surface unresolved decisions clearly
- align older summaries with newer planning docs
- expand page-planning packs in [APPLICATION/](APPLICATION/)

### Flutter and app planning

Best if you want to help define or build the app experience.

Read next:

- [APPLICATION/README.md](APPLICATION/README.md)
- [APPLICATION/APP_FLOW_OVERVIEW.md](APPLICATION/APP_FLOW_OVERVIEW.md)
- [APPLICATION/ONBOARDING/README.md](APPLICATION/ONBOARDING/README.md)

Good first work:

- refine screen documents
- add missing page packs
- turn planning docs into implementation-ready UI requirements
- help align the future Flutter app with the current planning direction

### Rust and network

Best if you want to work on the node, peer-to-peer sync, consensus, or local data flow.

Read next:

- [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md)
- [Social Production network README](https://github.com/social-production/network/blob/main/README.md)

Good first work:

- compare implementation against the architecture direction
- help close gaps around identity, node modes, sync, and finality
- improve internal docs or developer ergonomics in the network repo

### Design and outreach

Best if you want to make the project easier to understand, share, and join.

Read next:

- [OUTREACH/PITCH_PAGE.md](OUTREACH/PITCH_PAGE.md)
- [OUTREACH/SHARE_IMAGE_BRIEF.md](OUTREACH/SHARE_IMAGE_BRIEF.md)

Good first work:

- social share graphics
- beginner-facing summaries
- organization profile copy
- diagrams and visual explanations

### Legal and governance research

Best if you want to help test the real-world feasibility of the foundation and governance model.

Read next:

- [DRAFTS/LEGAL.md](DRAFTS/LEGAL.md)
- [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md)

Good first work:

- research jurisdictions
- identify legal risks or open questions
- clarify where legal execution depends on on-chain governance

## How To Use CURRENTLY_WORKING_ON

[CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md) is the active queue.

When you open it:

1. pick one item only
2. open the linked source documents for that item
3. check whether the issue is a wording problem, a design problem, or a technical problem
4. make a focused change instead of trying to solve everything at once

Examples:

- If the item says to review [README.md](README.md), compare it against [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md), [DRAFTS/OPERATIONS_MODEL.md](DRAFTS/OPERATIONS_MODEL.md), and [DRAFTS/LEGAL.md](DRAFTS/LEGAL.md).
- If the item says to continue application page planning, start from [APPLICATION/README.md](APPLICATION/README.md) and the relevant pack README before editing an individual page file.

## First Contribution Workflow

Use this workflow for your first contribution:

1. Read this guide.
2. Pick one item from [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md).
3. Find the source-of-truth document for that item.
4. Make one focused improvement.
5. Explain what you changed and why.

Keep your first change narrow. A good first contribution is a clarification, a cleanup, a small planning addition, or a single documentation alignment pass.

## Common Traps

These are the main things that can confuse new contributors.

### Older summaries may lag behind newer planning docs

[README.md](README.md) and [PLAN.md](PLAN.md) are useful summaries, but they still need alignment with the newer architecture and operations direction.

### Not everything is final yet

The moderation model and legal jurisdiction are still being finalized. Do not write public-facing copy that treats them as settled facts.

### The web repo is not the current product direction

The React web prototype is useful reference material, but the current product direction is driven by the planning repo and the long-term Flutter plus Rust architecture.

### The app repo is not yet a full product implementation

The Flutter app is still early. If you are doing app work, start with the planning docs before assuming the current app code reflects the intended product.

## If You Want The Fastest Possible Start

Read only these files first:

1. [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md)
2. [CURRENTLY_WORKING_ON.md](CURRENTLY_WORKING_ON.md)
3. [ARCHITECTURE/TECH_ARCHITECTURE.md](ARCHITECTURE/TECH_ARCHITECTURE.md)

Then choose one item and start small.