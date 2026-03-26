# Personalized Main Feed

## Purpose

This variant shows a feed shaped by the user’s selected interests, followed channels, and later participation patterns.

## Primary user

Returning user who has chosen interests or followed channels.

## Entry points

- From main feed tabs such as `My Feed`
- From app launch into a personalized default view later

## Exit points

- Thread detail
- Project detail
- Channel detail
- Interest settings later

## Primary CTA

`Adjust Feed Preferences`

Lets the user refine what appears here if the personalization feels weak.

## Secondary CTAs

- `Open Project`
- `Open Thread`
- `Follow Channel`
- `Unfollow Channel`

## Layout

- Same general feed shell as the canonical feed
- Clear tab state showing this is a personalized view
- Optional explanation when the feed is using preferences strongly

## Text wireframe

```text
+------------------------------------------------------------------+
| tabs: Home | My Feed | Local                                     |
| note: shaped by your interests and follows                       |
+------------------------------------------------------------------+
| personalized feed cards                                          |
| personalized feed cards                                          |
| personalized feed cards                                          |
+------------------------------------------------------------------+
```

## Content and data requirements

Required now:

- Followed channels or selected interests
- Feed ranking input from local preference state

Nice to have later:

- Explanations for why a result appears

Depends on node/backend work:

- Better recommendation and ranking logic

## User states

- Healthy personalized feed
- Weakly personalized feed
- No preference data available, fallback to broad home feed

## Permissions and roles

Logged-in user required.

## Node and sync considerations

If preference-backed content is not yet available locally, this view should degrade gracefully to a broader feed instead of appearing broken.

## Navigation notes

If this tab is empty, the user should be offered a direct path to adjust interests or follow channels.

## Flutter implementation notes

- Should likely be a tab state inside the feed module rather than a separate route in the first version
- Shared component implications: explain-why banner, preference adjustment entry point

## Open questions

- What is the minimum signal required before `My Feed` becomes meaningfully different from `Home`?

## References

- `web/docs/wireframes/00-index.md`
- `web/src/App.jsx`