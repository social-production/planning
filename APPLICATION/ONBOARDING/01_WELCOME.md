# Welcome

## Purpose

This is the first screen shown when a new user opens the app. Its job is to orient the user, explain what kind of platform they are entering, and move them into onboarding without overwhelming them.

## Primary user

First-time user.

## Entry points

- First app launch
- Explicit return to onboarding from a reset or reinstall state

## Exit points

- Continue into identity and key setup
- Optional exit to a learn-more or documentation path later if that exists

## Primary CTA

`Set Up My App`

Starts the onboarding flow and takes the user to identity and key setup.

## Secondary CTAs

- `Restore Existing Setup`
  Starts a recovery path for a returning user who already has an identity
- `Learn How This Works`
  Opens a short explanation modal or lightweight info panel about local-first and collective platform basics

## Layout

- Top area with product identity and short statement of purpose
- Middle area with 2 to 3 short explanation blocks
- Bottom area with primary and secondary CTAs

## Text wireframe

```text
+-----------------------------------------------------------+
| Social Production logo and name                           |
| Short statement: organize production, governance, funding |
| without centralized control                               |
|                                                           |
| Short explanation block                                   |
| Short explanation block                                   |
| Short explanation block                                   |
|                                                           |
| [ Set Up My App ]                                         |
| [ Restore Existing Setup ] [ Learn How This Works ]       |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Static app name and purpose text
- Local flag to determine if this is true first-run

Nice to have later:

- Version label
- Link to a concise explanation of node modes

Depends on node/backend work:

- None for the basic screen

## User states

- Default first-run state
- Returning user with existing local setup detected
- Corrupt local setup detected, which should route toward restore or repair guidance

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

The screen should avoid deep technical language, but it should prepare the user for the fact that the app manages local data and identity.

## Navigation notes

Back navigation should be disabled or minimized on first open because there is nowhere meaningful to return to.

## Flutter implementation notes

- Likely belongs in an `onboarding` feature module
- Can be implemented entirely with static content and local first-run state
- Shared component implications: branded onboarding shell, CTA group, simple info cards

## Open questions

- Should the welcome screen expose sign-in style language, or should identity creation be framed more explicitly around keys and local credentials from the start?

## References

- `ARCHITECTURE/TECH_ARCHITECTURE.md`
- `web/src/AuthPage.jsx`