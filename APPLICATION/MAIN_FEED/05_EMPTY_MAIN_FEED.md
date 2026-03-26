# Empty Main Feed

## Purpose

This variant handles cases where the user reaches the main feed but there is no content to show yet.

## Primary user

New or returning user with no matching local content.

## Entry points

- From any feed tab with zero results

## Exit points

- Create project
- Create thread
- Adjust interests
- Switch feed tab

## Primary CTA

`Create Project`

When the feed is empty, the best recovery is not only to wait for content but to prompt the user toward productive participation.

## Secondary CTAs

- `Create Thread`
- `Adjust Interests`
- `Go To Home Feed`
- `Retry`

## Layout

- Keep the standard feed shell so the screen still feels like the feed
- Replace the list with an empty-state block
- Offer direct recovery actions

## Text wireframe

```text
+------------------------------------------------------------------+
| tabs, filters, sort                                              |
+------------------------------------------------------------------+
| no results or no content yet                                     |
| short explanation                                                |
| [ Create Project ] [ Create Thread ]                             |
| [ Adjust Interests ] [ Retry ]                                   |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- Empty-state reason if known
- Recovery actions

Nice to have later:

- Suggested starter channels or projects

Depends on node/backend work:

- Better explanations for why the feed is empty

## User states

- Truly empty network state
- Empty because of current filter
- Empty because sync is incomplete
- Empty because personalization is too narrow

## Permissions and roles

Logged-in user required.

## Node and sync considerations

This screen should distinguish between `nothing exists locally yet` and `something may appear after sync` when possible.

## Navigation notes

Do not trap the user in a dead end. At least one recovery action should always be visible.

## Flutter implementation notes

- Can be implemented as a feed-body state object inside the main feed module
- Shared component implications: empty-state block, recovery CTA row, retry pattern

## Open questions

- Should an empty local feed lean more toward creation, discovery, or sync explanation in the first version?

## References

- `web/src/App.jsx`
- `DRAFTS/OPERATIONS_MODEL.md`