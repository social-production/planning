# Profile Setup

## Purpose

This page captures the first visible user profile details needed for participation and discovery.

## Primary user

Newly created or newly restored user before entering the app.

## Entry points

- From node setup basics

## Exit points

- Forward to interest selection
- Skip forward if the profile minimum is complete and interests are deferred

## Primary CTA

`Save Profile`

Stores the initial profile details locally and prepares them for later sync.

## Secondary CTAs

- `Skip For Now`
  Defers non-required fields and moves forward
- `Add Profile Picture`
  Opens image selection or capture flow
- `Back`
  Returns to node setup basics

## Layout

- Header explaining why a basic profile matters
- Form with required and optional sections
- Preview area for avatar and display summary
- Bottom CTA row

## Text wireframe

```text
+-----------------------------------------------------------+
| Set up your profile                                       |
| Help other people recognize and work with you             |
|                                                           |
| avatar area                                               |
| display name or username summary                          |
| bio field                                                 |
| optional location field                                   |
| optional website or contact field later                   |
|                                                           |
| [ Save Profile ] [ Skip For Now ]                         |
+-----------------------------------------------------------+
```

## Content and data requirements

Required now:

- Username or display name reference
- Avatar placeholder support
- Bio field

Nice to have later:

- Location controls for local feed relevance
- Website or external contact fields

Depends on node/backend work:

- Asset upload and replication behavior for profile images

## User states

- Empty form
- Partial completion
- Validation error
- Save in progress
- Save success
- Save failed but local retry possible

## Permissions and roles

No role-specific behavior.

## Node and sync considerations

The user should be told when profile changes are saved locally first and may appear to other peers after sync.

## Navigation notes

The user should be allowed to continue with a minimal profile, but the screen should make clear what they are skipping.

## Flutter implementation notes

- Can reuse many form patterns from the legacy profile editing screens as design reference
- Shared component implications: avatar picker, profile summary card, optional field grouping

## Open questions

- Which profile fields are truly required at first launch?
- Is location part of onboarding or better deferred until feed personalization is more mature?

## References

- `web/src/EditProfilePage.tsx`
- `ARCHITECTURE/TECH_ARCHITECTURE.md`