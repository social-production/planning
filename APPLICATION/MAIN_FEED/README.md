# Main Feed Pack

This pack defines the main feed as the first everyday working screen after onboarding.

It includes the canonical logged-in feed and the most important variants needed for real app behavior.

## Pack scope

This pack covers:

- The canonical main feed layout
- First-use feed behavior
- Personalized and local variants
- Empty state behavior
- Syncing, offline, and recovery behavior

## Why the main feed needs a pack instead of one file

The feed is not a single static screen.

The user may arrive in very different conditions:

- First run after onboarding
- Returning with a healthy local cache
- Returning while still syncing
- Returning while offline
- Returning to an empty or weakly personalized feed

Treating those as explicit planned variants reduces implementation ambiguity.

## File order

1. `01_CANONICAL_MAIN_FEED.md`
2. `02_FIRST_USE_MAIN_FEED.md`
3. `03_PERSONALIZED_MAIN_FEED.md`
4. `04_LOCAL_MAIN_FEED.md`
5. `05_EMPTY_MAIN_FEED.md`
6. `06_SYNCING_OFFLINE_AND_RECOVERY.md`

## Core feed rules for this phase

- The feed is read from local derived state, not directly from a central server
- The user must be able to understand whether the feed is current, still syncing, or limited by node mode or connectivity
- Threads and projects should appear as distinct card types or at least distinct badges and statuses
- Feed CTAs should prioritize action without hiding discovery

## Notes for implementers

The feed can be built before full backend completion if the app has stable local view models for:

- Feed cards
- Sorting and filtering state
- Sync freshness state
- Empty and error banners
- Navigation into project and thread detail screens