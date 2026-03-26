# Onboarding Pack

This pack defines the first-run experience for Social Production.

The goal is to move a user from opening the app for the first time to entering the product with a usable identity, basic profile, and enough system understanding to proceed without confusion.

## Pack scope

This onboarding pack covers:

- Orientation on first open
- Identity and key setup
- Basic node setup
- Profile setup
- Optional interest or channel selection
- Sync and ready state before entering the main feed

## Why onboarding is more than signup

The platform is not a simple centralized web app.

The onboarding flow has to prepare the user for:

- A local-first app model
- A node-backed experience
- A persistent identity model
- Sync and availability states that may affect what they see at first launch

## File order

1. `01_WELCOME.md`
2. `02_IDENTITY_AND_KEYS.md`
3. `03_NODE_SETUP_BASICS.md`
4. `04_PROFILE_SETUP.md`
5. `05_INTEREST_SELECTION.md`
6. `06_SYNC_AND_READY.md`

## Completion rule

The onboarding experience is complete when the user can safely land in the main feed with:

- A created or restored identity
- A selected initial node mode
- A basic profile
- A clear understanding of whether the app is still syncing

## Notes for implementers

This pack is written to support a stub-first Flutter implementation.

That means the screens can be built before full node integration exists, as long as the app can simulate:

- Identity creation or restore results
- Node mode selection
- Profile save state
- Sync progress and readiness state