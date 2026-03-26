# Interest Selection

## Purpose

This page gives the user a lightweight way to shape their first feed without forcing a deep preference system.

## Primary user

New user who has completed identity, node basics, and profile basics.

## Entry points

- From profile setup

## Exit points

- Forward to sync and ready state
- Back to profile setup

## Primary CTA

`Continue To Feed Setup`

Stores selected interests and moves the user forward.

## Secondary CTAs

- `Skip For Now`
  Enters the product without personalization
- `Select Suggested Channels`
  Applies a sensible starter set based on broad productive topics or region if available

## Layout

- Header explaining that this step personalizes discovery
- Topic or channel chips in grouped sections
- Optional explanation that choices can be changed later
- Bottom CTA row

## Text wireframe

```text
+-----------------------------------------------------------+
| Choose what you want to see first                         |
| You can change this later                                 |
|                                                           |
| productive spheres                                        |
| [ Food ] [ Housing ] [ Healthcare ] [ Communications ]    |
| [ Innovation ] [ Local area ] [ Mutual aid ]             |
|                                                           |
| starter channels or topics                                |
| [ chip ] [ chip ] [ chip ]                                |
|                                                           |
| [ Continue To Feed Setup ] [ Skip For Now ]               |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Simple interest taxonomy or starter channel list
- Selection state

Nice to have later:

- Region-aware suggestions
- Existing community suggestions

Depends on node/backend work:

- Real personalized recommendations

## User states

- No selection
- Some selections made
- Suggested selections applied
- Save in progress
- Save failed with retry option

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

If channel availability depends on sync state, this screen should fall back to broad topic selection rather than blocking the user.

## Navigation notes

Skipping this page should still lead to a usable feed, likely a broad default home feed.

## Flutter implementation notes

- Can start with static chip lists and later connect to real channel/topic data
- Shared component implications: selectable chips, grouped chip sections, helper text blocks

## Open questions

- Should this step use productive spheres, channels, locations, or a hybrid starter model?
- How much of the local feed concept should appear here before location behavior is finalized?

## References

- `DRAFTS/OPERATIONS_MODEL.md`
- `DRAFTS/QUESTIONS&ANSWERS/QUESTIONS FOR CLARIFICATION.md`