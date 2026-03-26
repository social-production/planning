# Identity And Keys

## Purpose

This page creates or restores the user identity used by the application. It replaces the assumptions of a normal centralized signup flow with a screen that clearly handles persistent local credentials.

## Primary user

First-time user or returning user restoring access.

## Entry points

- From welcome via `Set Up My App`
- From welcome via `Restore Existing Setup`

## Exit points

- Forward to node setup basics after successful identity creation or restore
- Back to welcome if the user cancels before creating anything

## Primary CTA

`Create Identity`

Creates a new user identity and stores the required credentials locally.

## Secondary CTAs

- `Restore Identity`
  Switches the page into restore mode for importing or recovering an existing identity
- `Continue`
  Enabled after success and moves the user to node setup basics
- `Back`
  Returns to welcome before identity creation is complete

## Layout

- Header that explains why identity matters
- Mode selector for create versus restore
- Form or recovery panel
- Bottom area for status and CTAs

## Text wireframe

```text
+-----------------------------------------------------------+
| Create or restore your Social Production identity         |
| Your identity is used for participation, membership,      |
| voting, and signing actions across devices                |
|                                                           |
| [ Create ] [ Restore ]                                    |
|                                                           |
| create mode:                                              |
|   username field                                          |
|   password or local protection field if needed            |
|                                                           |
| restore mode:                                             |
|   recovery/import input                                   |
|                                                           |
| status area                                               |
| [ Create Identity ] [ Continue ]                          |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Username entry or identity label rules
- Credential creation or restore logic, even if stubbed locally
- Clear success and failure messaging

Nice to have later:

- Device naming support
- Recovery education panel

Depends on node/backend work:

- Final identity storage and cross-device transfer behavior

## User states

- Create mode default
- Restore mode
- Validation error
- Identity creation in progress
- Identity created successfully
- Restore failed
- Restore succeeded

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

This page must align with the architecture distinction between `user_id` and `node_id`. The user should not be told that a device identity is the same thing as their permanent user identity.

## Navigation notes

The user should not advance until identity creation or restore has completed successfully.

## Flutter implementation notes

- Likely one page with create and restore modes rather than two separate screens in the first implementation
- Can be stubbed with local secure storage until real contracts exist
- Shared component implications: segmented mode switcher, credential status box, validation summary

## Open questions

- What exact first-run recovery mechanism will be used for restore in the earliest version?
- What language should be used to describe keys without making the screen too technical?

## References

- `ARCHITECTURE/TECH_ARCHITECTURE.md`
- `web/src/AuthPage.jsx`