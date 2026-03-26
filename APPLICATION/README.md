# Application Planning

This folder is the working home for the application layout and page-planning phase in the planning repo.

It exists to turn the product direction in the planning documents into page-by-page implementation guidance that can be used by both planners and developers.

## What belongs here

- Page packs for specific flows such as onboarding and the main feed
- Shared documentation that explains how to read and extend the page packs
- Reusable page templates for future screen planning
- App flow and handoff documents that help Flutter work proceed in parallel with node work

## Source-of-truth rules

Use the planning repo as the canonical source of truth for this phase.

- `ARCHITECTURE/TECH_ARCHITECTURE.md` defines technical constraints such as identity, node mode, sync, local data, and client behavior
- `DRAFTS/OPERATIONS_MODEL.md` defines product rules such as project roles, voting, moderation, project lifecycle, funding, and distribution
- `DRAFTS/LEGAL.md` defines legal and stewardship boundaries that affect platform wording around funds, assets, and ownership
- The legacy `web/` repo is reference material only for prior screen ideas, naming, and layout patterns

## Folder structure

- `APP_FLOW_OVERVIEW.md` explains the purpose of this phase and how the packs fit together
- `DOCUMENT_STRUCTURE.md` explains how the folder is organized and how future packs should be added
- `PAGE_TEMPLATE.md` is the standard template for every page file in this phase
- `ONBOARDING/` contains the onboarding pack, one file per page
- `MAIN_FEED/` contains the complete main feed pack, including the canonical screen and key operational variants

## How to use this folder

1. Read `APP_FLOW_OVERVIEW.md` first.
2. Read `DOCUMENT_STRUCTURE.md` to understand how the pack is organized.
3. Use `PAGE_TEMPLATE.md` when creating new pages.
4. Read the pack overview in `ONBOARDING/README.md` or `MAIN_FEED/README.md` before opening individual page files.

## Scope for this phase

This phase is documentation-first.

Included:

- Screen purpose
- Basic text wireframes
- CTA definitions
- Navigation rules
- Data and state requirements
- Notes for Flutter implementation planning

Excluded:

- Pixel-perfect visual design
- Final copywriting polish
- Backend implementation
- Final decisions for still-open governance and moderation questions