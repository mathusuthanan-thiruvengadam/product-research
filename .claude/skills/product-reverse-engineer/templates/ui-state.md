# Template: UI State

One instance per distinct UI state identified during Phase 2 (Explore the
application) — loading, empty, error, or other meaningfully distinct states
of a view/component. Feeds the UI States section of the final report.

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`.

---

## UI State: <name>

- **UI State ID:** UI-<NNN>
- **Related feature/page:** <Feature ID and/or page/URL this state belongs to>
- **State type:** `Loading | Empty | Error | Default | Success | Disabled | Other`
- **Trigger/condition:** <what causes this state — e.g. "page load before
  data resolves", "zero search results", "required field left blank on
  submit">
- **Visual description:** <what is shown — copy, iconography, layout changes>
- **Evidence:** <URL, screenshot reference, exact interaction>
- **Confidence:** `High | Medium | Low`
- **Classification:** `OBSERVED | INFERRED | UNKNOWN`
- **Notes:** <anything relevant — e.g. "only observable via browser
  automation; not confirmed under static fetch">

---

## Example (filled)

- **UI State ID:** UI-004
- **Related feature/page:** FEAT-003 (Invite teammate), /settings/team
- **State type:** Loading
- **Trigger/condition:** Clicking "Send invite" while the request is in
  flight.
- **Visual description:** Button label changes to a spinner icon and the
  button is disabled until the request resolves.
- **Evidence:** screenshot ref invite-loading-01 (captured via browser
  automation)
- **Confidence:** High
- **Classification:** OBSERVED
- **Notes:** Duration of loading state not measured; only its presence was
  confirmed.

## Example (Empty state, filled)

- **UI State ID:** UI-009
- **Related feature/page:** FEAT-001 (Create workspace), /dashboard
- **State type:** Empty
- **Trigger/condition:** A newly created workspace with no boards yet.
- **Visual description:** Illustration with the text "No boards yet" and a
  primary button "Create your first board."
- **Evidence:** screenshot ref dashboard-empty-01
- **Confidence:** High
- **Classification:** OBSERVED
