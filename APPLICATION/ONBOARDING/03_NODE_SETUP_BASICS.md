# Node Setup Basics

## Purpose

This page introduces the local node requirement in a minimal, beginner-safe way and lets the user choose an initial node mode suitable for their device.

## Primary user

First-time user immediately after identity setup.

## Entry points

- From identity and keys after success

## Exit points

- Forward to profile setup after choosing a node mode
- Back to identity and keys if the user needs to change setup before continuing

## Primary CTA

`Use Recommended Setup`

Applies the default node mode recommended for the device and continues.

## Secondary CTAs

- `Choose Full Mode`
  Selects a full node if the device is suitable and the user wants maximum participation
- `Choose Light Mode`
  Selects a light node for lower storage and network use
- `What Is The Difference?`
  Opens a simple explanation of Full versus Light

## Layout

- Header with plain-language explanation of local node behavior
- Recommended setup card
- Alternative node mode cards
- Small note that advanced network settings come later

## Text wireframe

```text
+-----------------------------------------------------------+
| Set up how this device participates                       |
| This app connects through a local node on your device     |
|                                                           |
| Recommended for this device                               |
| [ Light mode card or Full mode card ]                     |
|                                                           |
| Other option                                              |
| [ Alternate mode card ]                                   |
|                                                           |
| [ Use Recommended Setup ]                                 |
| [ What Is The Difference? ]                               |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Device-aware recommendation rule
- Short explanation of Full and Light modes
- Selected mode state

Nice to have later:

- Estimated disk/network impact ranges
- Battery warning copy for mobile full mode

Depends on node/backend work:

- Real node startup and health reporting

## User states

- Default recommendation shown
- Manual mode selection
- Node bootstrap in progress
- Bootstrap failed
- Setup completed

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

This page should reflect the planning default that mobile devices start in Light mode and desktop devices may start in Full mode. Gossip mode is part of the architecture but should not be a first-run default in this phase.

## Navigation notes

The user may continue once a valid initial mode is selected, even if full sync has not completed.

## Flutter implementation notes

- Can be implemented before full node startup is real by using stubbed status transitions
- Shared component implications: selectable mode cards, recommendation badge, simple explainer modal

## Open questions

- Should the first version expose only recommended and alternate modes, or list all supported modes explicitly?

## References

- `ARCHITECTURE/TECH_ARCHITECTURE.md`