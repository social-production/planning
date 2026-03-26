# First-Use Main Feed

## Purpose

This variant handles the moment immediately after onboarding when the user has just entered the app and may have little or no personalized local state.

## Primary user

New user entering the feed for the first time.

## Entry points

- From onboarding `Enter The Feed`

## Exit points

- Project detail
- Thread detail
- Create project
- Create thread
- Personalization follow-up later

## Primary CTA

`Explore Projects`

Pushes the user toward the most materially useful content on the platform during their first session.

## Secondary CTAs

- `Create Project`
- `Create Thread`
- `Refine Interests`
  Returns to or opens interest selection settings later

## Layout

- A lightweight welcome banner above the normal feed layout
- Same basic feed structure as the canonical feed
- Slightly stronger discovery guidance and orientation text

## Text wireframe

```text
+------------------------------------------------------------------+
| welcome banner: your setup is complete                           |
| tip: start by exploring active projects or follow topics         |
+------------------------------------------------------------------+
| tabs, filters, sort, and create actions                          |
+------------------------------------------------------------------+
| starter feed cards                                               |
| starter feed cards                                               |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- New-user marker from onboarding
- Starter feed content or broad home feed fallback

Nice to have later:

- Contextual tips based on interest selection

Depends on node/backend work:

- Real recommendation quality

## User states

- Starter content available
- Very low-content state
- Sync still filling feed

## Permissions and roles

Logged-in user required.

## Node and sync considerations

This screen should reduce confusion if the feed is still sparse because the node is new and sync is incomplete.

## Navigation notes

The welcome banner should be dismissible after the first session.

## Flutter implementation notes

- Best implemented as the canonical feed plus a transient onboarding-complete banner state
- Shared component implications: onboarding completion banner, starter guidance card

## Open questions

- Should the first-use feed default to projects-only for the first session, or show mixed content immediately?

## References

- `DRAFTS/OPERATIONS_MODEL.md`
- `web/src/App.jsx`