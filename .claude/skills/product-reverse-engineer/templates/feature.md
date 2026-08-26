# Template: Feature

One instance per distinct feature identified during Phase 3 (Analyze
features and user journeys). Feeds the Feature Inventory section of the
final report.

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`.

---

## Feature: <name>

- **Feature ID:** FEAT-<NNN>
- **Feature name:** <short, PM-recognizable name>
- **Description:** <what it does, 1–3 sentences>
- **Actor:** <who performs/uses this — e.g. "logged-in user", "admin", "visitor">
- **Preconditions:** <what must be true before this feature can be used —
  e.g. "user has an active account", "at least one project exists">
- **Trigger:** <what starts this — a click, a navigation, a scheduled event>
- **Inputs:** <data/parameters the user or system provides — form fields,
  selections, uploaded files>
- **Behavior:** <what observably happens when triggered — the core logic as
  seen from outside>
- **Outputs:** <what results — a new record, a UI update, a downloaded file,
  a notification>
- **Dependencies:** <other features/systems this relies on — e.g. "requires
  an integration with X", "depends on Feature FEAT-002">
- **UI states:** <related UI State template IDs — loading/empty/error states
  tied to this feature, e.g. UI-004, UI-005>
- **Error states:** <what errors are observable for this feature specifically>
- **Evidence:** <URL(s), screenshot reference(s), exact interaction(s) this
  is based on>
- **Confidence:** `High | Medium | Low`
- **Classification:** `OBSERVED | INFERRED | UNKNOWN`

---

## Example (filled)

- **Feature ID:** FEAT-003
- **Feature name:** Invite teammate
- **Description:** Lets a workspace owner invite another person to join the
  workspace via email.
- **Actor:** Workspace owner (role observed as required — invite control was
  not visible when browsing a non-owner demo view).
- **Preconditions:** User is logged in and is the workspace owner.
- **Trigger:** Clicking "Invite" in the workspace settings page.
- **Inputs:** Email address (required, validated as email format), optional
  role selection (dropdown: "Member" / "Admin").
- **Behavior:** Submitting the form shows a success toast: "Invite sent to
  {email}." The invited email then appears in a "Pending invites" list.
- **Outputs:** New row added to Pending invites list; success toast shown.
- **Dependencies:** Requires the workspace to exist (FEAT-001: Create
  workspace).
- **UI states:** UI-007 (loading spinner on submit), UI-008 (inline
  validation error on invalid email)
- **Error states:** Inline error "Enter a valid email address" observed when
  submitting a malformed email.
- **Evidence:** /settings/team page, screenshot ref invite-01, invite-02
- **Confidence:** High
- **Classification:** OBSERVED
