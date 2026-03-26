# Document Structure

This document explains how the application planning folder is organized and how to extend it.

## Naming choice

The folder is named `APPLICATION` because this phase is broader than wireframes alone.

It includes:

- Screen planning
- User flow planning
- CTA and navigation planning
- State and dependency planning
- Early handoff guidance for Flutter implementation

## Current structure

```text
APPLICATION/
  README.md
  APP_FLOW_OVERVIEW.md
  DOCUMENT_STRUCTURE.md
  PAGE_TEMPLATE.md
  ONBOARDING/
    README.md
    01_WELCOME.md
    02_IDENTITY_AND_KEYS.md
    03_NODE_SETUP_BASICS.md
    04_PROFILE_SETUP.md
    05_INTEREST_SELECTION.md
    06_SYNC_AND_READY.md
  MAIN_FEED/
    README.md
    01_CANONICAL_MAIN_FEED.md
    02_FIRST_USE_MAIN_FEED.md
    03_PERSONALIZED_MAIN_FEED.md
    04_LOCAL_MAIN_FEED.md
    05_EMPTY_MAIN_FEED.md
    06_SYNCING_OFFLINE_AND_RECOVERY.md
```

## Why one file per page

One file per page keeps the work modular.

Benefits:

- Each page can be reviewed independently
- Developers can implement screens in parallel
- Open questions can be attached to the exact screen they affect
- Later changes do not force a rewrite of one giant document

## Pack design rules

Each pack should have:

1. A `README.md` that explains the pack as a whole
2. One file per page or screen variant
3. Clear links to any related shared support docs

## What should become a new pack later

After onboarding and main feed, the next likely packs are:

- Thread detail
- Project detail
- Project creation and editing
- Thread creation and editing
- User profile
- Proposals and voting
- Funding and distribution
- Notifications
- Moderation
- Advanced network settings

## What should stay in shared docs

Do not repeat broad conventions in every page file if they are truly shared.

Shared material belongs in root-level support docs when it applies across many screens, such as:

- Page file template
- Navigation conventions
- Shared state expectations
- Common CTA rules

For this first phase, only the page template is formalized. More shared docs can be added once repeated patterns become stable.

## Review standard for new page files

Every new page file should be checked for:

- Clear purpose
- Clear user entry points
- Primary and secondary CTA definitions
- Required data and dependencies
- Loading, empty, error, offline, and syncing states where relevant
- Architecture alignment
- Operations alignment
- Open questions and blockers