# Syncing, Offline, And Recovery

## Purpose

This file defines the operational feed states that appear when content freshness, connectivity, or local availability is limited.

## Primary user

Any logged-in user whose feed is affected by sync delay, offline mode, node startup issues, or recoverable data problems.

## Entry points

- From app launch into the main feed
- From any feed tab when operational status changes

## Exit points

- Back into a healthy feed state
- Into network settings later
- Into retry or refresh flows

## Primary CTA

`Retry Sync`

Attempts to refresh local state or re-run the relevant sync process.

## Secondary CTAs

- `Continue Offline`
  Keeps the user in the app using cached local content
- `See Details`
  Shows a more detailed explanation of node or sync status
- `Open Network Settings`
  For deeper control later in the app

## Layout

- Standard feed shell remains visible
- A prominent status banner or inline state card appears above or within the feed
- Cached content remains visible when safe and possible

## Text wireframe

```text
+------------------------------------------------------------------+
| status banner: sync in progress / offline / node issue           |
| short explanation                                                |
| [ Retry Sync ] [ Continue Offline ] [ See Details ]              |
+------------------------------------------------------------------+
| cached feed cards or skeleton feed                               |
| cached feed cards or skeleton feed                               |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- Sync status state
- Last successful update time if available
- Whether cached feed data is usable

Nice to have later:

- More detailed node diagnostics
- Separate asset-sync versus data-sync messaging

Depends on node/backend work:

- Real connectivity and sync telemetry

## User states

- Initial syncing with partial content available
- Initial syncing with no content yet
- Offline with cached content
- Offline with no cached content
- Node start failed
- Recoverable refresh failure

## Permissions and roles

Logged-in user required.

## Node and sync considerations

This page file exists because the architecture makes these states normal rather than exceptional. The app should treat them as first-class UX, not as edge cases.

## Navigation notes

If cached content exists, the user should usually be able to continue reading while recovery actions remain available.

## Flutter implementation notes

- Status handling should likely be represented as a feed-level state model plus reusable banners or cards
- Shared component implications: sync banner, offline banner, retry controls, skeleton feed rows, cached-content notice

## Open questions

- What exact operational states should be visible to ordinary users versus hidden behind a details view?
- How much node terminology should appear in normal user-facing banners?

## References

- `ARCHITECTURE/TECH_ARCHITECTURE.md`
- `web/src/App.jsx`