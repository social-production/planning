# Canonical Main Feed

## Purpose

This is the standard logged-in home screen for the app after onboarding. It is the baseline feed experience that other feed variants inherit from.

## Primary user

Returning logged-in user with a usable local app state.

## Entry points

- From onboarding completion
- From app launch when already set up
- From top-level app navigation

## Exit points

- Thread detail
- Project detail
- Create thread
- Create project
- Notifications or alerts
- Search results later

## Primary CTA

`Create Project`

Opens the project creation flow. This is the highest-value creation action because the platform centers collective production, not only discussion.

## Secondary CTAs

- `Create Thread`
  Opens a discussion post flow
- `Open Project`
  Goes to project detail
- `Open Thread`
  Goes to thread detail
- `Join Project`
  Starts or requests project membership depending on the final membership model
- `Open Notifications`
  Opens the alerts or notifications surface

## Layout

- Top bar with branding, search entry point, alerts, notifications, and user utilities
- Main feed header with feed tabs and filter/sort controls
- Feed content area with thread and project cards
- Optional side panels or compact supporting sections depending on device size

## Text wireframe

```text
+------------------------------------------------------------------+
| logo | search | alerts | notifications | user menu               |
+------------------------------------------------------------------+
| feed tabs: Home | My Feed | Local      filters   sort            |
+------------------------------------------------------------------+
| create actions: [ Create Thread ] [ Create Project ]             |
+------------------------------------------------------------------+
| feed card                                                        |
| feed card                                                        |
| feed card                                                        |
| ...                                                              |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- Feed tab state
- Filter state for thread versus project or all content
- Sort state such as Top and Latest
- Feed item list with enough data for cards
- Notification and alert count placeholders

Nice to have later:

- Search suggestions
- Events sidebar or upcoming activity panel

Depends on node/backend work:

- Real local database-backed feed hydration
- Freshness and sync metadata

## User states

- Default populated feed
- Mixed thread and project feed
- Filtered projects-only feed
- Filtered threads-only feed
- Latest sort
- Top sort

## Permissions and roles

Logged-in user required. Creation actions may differ later by account readiness, moderation restrictions, or node health, but not by ordinary role in the first version.

## Node and sync considerations

This screen should indicate that content is locally available and may continue updating as sync progresses. Asset-heavy cards should tolerate delayed media availability.

## Navigation notes

Returning from detail pages should restore scroll position and filter state where practical.

## Flutter implementation notes

- Strong candidate for a dedicated `feed` feature module
- Card models should be stable enough to mock before the backend is finished
- Shared component implications: top app bar, tab selector, sort/filter controls, thread card, project card, sync banner

## Open questions

- Should `Create Project` always be more visually prominent than `Create Thread`, or should that depend on the active tab?
- Should a three-column layout survive on desktop in Flutter, or should supporting panels collapse into drawers or sections?

## References

- `web/src/App.jsx`
- `web/docs/wireframes/01-layout.md`
- `DRAFTS/OPERATIONS_MODEL.md`