# Sync And Ready

## Purpose

This page prepares the user to enter the app while making sync state explicit. It should reduce confusion when the feed is not fully populated yet.

## Primary user

User finishing onboarding.

## Entry points

- From interest selection
- From profile setup if interests are skipped

## Exit points

- Enter the main feed
- Optional entry into a brief troubleshooting or network info path later

## Primary CTA

`Enter The Feed`

Moves the user into the main feed, even if sync is still in progress, as long as the minimum app-ready conditions are met.

## Secondary CTAs

- `See Sync Details`
  Opens a simple progress or explanation panel
- `Back`
  Returns to the previous onboarding step

## Layout

- Header confirming setup completion
- Sync status summary card
- Short explanation of what may still appear gradually
- Bottom CTA row

## Text wireframe

```text
+-----------------------------------------------------------+
| Your app is ready                                         |
| Identity created, profile saved, device mode selected     |
|                                                           |
| sync status card                                          |
| - local node state                                        |
| - data sync progress                                      |
| - note about content loading gradually                    |
|                                                           |
| [ Enter The Feed ] [ See Sync Details ]                   |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Setup completion summary
- Basic sync status indicator
- App-ready decision state

Nice to have later:

- More detailed progress metrics
- Link to advanced network settings after onboarding

Depends on node/backend work:

- Real sync telemetry

## User states

- Ready with sync still in progress
- Ready with sync largely complete
- Setup succeeded but node start failed
- Setup succeeded but sync unavailable

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

This page should set the expectation that app state is derived locally and may continue filling in after the user enters the feed.

## Navigation notes

The user should not be trapped here waiting for perfect sync. Entering the feed should be allowed once the minimum local setup is usable.

## Flutter implementation notes

- Can be built early with stubbed progress values
- Shared component implications: sync status card, app-ready checklist, inline explanation banner

## Open questions

- What exact minimum state should be required before the app can enter the main feed?

## References

- `ARCHITECTURE/TECH_ARCHITECTURE.md`