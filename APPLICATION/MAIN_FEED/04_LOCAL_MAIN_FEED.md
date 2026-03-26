# Local Main Feed

## Purpose

This variant helps users discover nearby or regionally relevant activity once the platform’s location behavior is mature enough to support it.

## Primary user

User looking for geographically relevant projects, discussions, events, or communities.

## Entry points

- From main feed tab `Local`

## Exit points

- Project detail
- Thread detail
- Event or meetup detail later
- Location settings later

## Primary CTA

`Set Or Confirm Local Area`

Lets the user define or confirm the regional basis for this feed.

## Secondary CTAs

- `Open Project`
- `Open Thread`
- `See Nearby Activity`
- `Change Local Area`

## Layout

- Same feed shell as the canonical feed
- A location context banner near the top
- Feed cards with stronger emphasis on region, meetup, or local relevance where available

## Text wireframe

```text
+------------------------------------------------------------------+
| tabs: Home | My Feed | Local                                     |
| local context: showing activity near [area]                      |
| [ Set Or Confirm Local Area ]                                    |
+------------------------------------------------------------------+
| locally relevant feed cards                                      |
| locally relevant feed cards                                      |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- A local area marker or fallback area state
- Feed items with enough location metadata to support local ranking

Nice to have later:

- Distance or proximity explanation
- Regional event grouping

Depends on node/backend work:

- Reliable location-related metadata and filtering behavior

## User states

- Local area known and feed populated
- Local area unknown
- Local area known but no results
- Syncing local data

## Permissions and roles

Logged-in user required.

## Node and sync considerations

Because location-based filtering is still not fully finalized in planning, this tab should be treated as a planned variant with explicit open questions rather than a locked behavior spec.

## Navigation notes

If the user has never set a local area, the tab should open into a setup-focused state rather than a blank feed.

## Flutter implementation notes

- In the first implementation, this may exist as a stub tab with a setup state until the local feed model is finalized
- Shared component implications: location banner, local setup prompt, no-results guidance

## Open questions

- What exact data defines `local` in the first version?
- Does local relevance use profile location, explicit area choice, community membership, or a hybrid?

## References

- `README.md`
- `PLAN.md`
- `DRAFTS/QUESTIONS&ANSWERS/QUESTIONS FOR CLARIFICATION.md`