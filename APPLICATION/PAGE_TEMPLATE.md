# Page Template

Use this template for every new application page file in this planning section.

---

# [Page Name]

## Purpose

Explain what this screen exists to do in one short paragraph.

## Primary user

State who this page is primarily for.

Examples:

- First-time user
- Returning logged-in user
- Project manager
- Moderator

## Entry points

List how a user reaches this page.

- App launch
- Back navigation from another page
- CTA from another page
- Notification or alert
- Deep link

## Exit points

List where the user goes next.

## Primary CTA

State the main action on the page and exactly what it does.

## Secondary CTAs

List the supporting actions and what each one does.

## Layout

Describe the screen in zones from top to bottom.

Suggested format:

- Top bar
- Main content
- Supporting panel or footer

## Text wireframe

Use simple text blocks to describe the visual structure.

Example:

```text
+---------------------------------------------------+
| Top bar                                           |
+---------------------------------------------------+
| Heading                                           |
| Supporting text                                   |
| Primary CTA                                       |
| Secondary CTA                                     |
+---------------------------------------------------+
```

## Content and data requirements

List the minimum data needed to render the page.

Separate these when useful:

- Required now
- Nice to have later
- Depends on node/backend work

## User states

List all meaningful states.

Typical examples:

- Default
- Loading
- Empty
- Validation error
- Network error
- Offline
- Syncing
- Success

## Permissions and roles

State whether the page changes by role, membership, or account status.

## Node and sync considerations

State what the page needs to know about:

- User identity
- Node mode
- Local database state
- Sync freshness
- Asset availability

## Navigation notes

State any special navigation rules, such as preventing the user from leaving before a critical step is complete.

## Flutter implementation notes

Describe how this page could be grouped or built in the app.

Useful topics:

- Suggested feature/module ownership
- Stub-first implementation options
- Local mock data needs
- Shared components implied by this page

## Open questions

List unresolved questions that affect this page.

## References

List the planning and prototype documents that informed the page.