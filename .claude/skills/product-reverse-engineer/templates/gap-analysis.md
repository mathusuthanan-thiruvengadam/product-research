# Template: Gap Analysis

Produced in Phase 5 (Perform gap analysis and quality review) after working
through `references/quality-checklist.md`. One instance per gap; the
collection feeds the Gap Analysis section of the final report, alongside a
short overall summary.

Classification here describes *the gap itself*, not a finding — a gap is by
definition where evidence is thin or absent, so most gaps are UNKNOWN or
straddle INFERRED/UNKNOWN. Use it to record confidence in what's missing.

---

## Gap: <short description>

- **Gap ID:** GAP-<NNN>
- **Area:** <which report section/topic this gap affects — e.g. "Settings",
  "Authentication Boundaries", "Non-Functional Requirements">
- **Description:** <what is incomplete, ambiguous, or unresolved>
- **Why the evidence is missing:** <e.g. "blocked by authentication wall",
  "feature not exercised to avoid a destructive action", "only reachable via
  browser automation, which was unavailable">
- **Impact:** <what this gap means for the usefulness/completeness of the
  requirements — e.g. "MVP candidate may be missing a core admin capability
  that exists but wasn't visible without an account">
- **Related open question(s):** <the specific, answerable-in-principle
  question(s) that would close this gap>
- **Suggested next step:** <what access, tooling, or action would resolve
  this — e.g. "re-run with user-authorized test account access">

---

## Overall gap-analysis summary (one per report)

- **Total gaps identified:** <n>
- **Gaps by area:** <short breakdown, e.g. "Settings: 3, Integrations: 2">
- **Most significant gap:** <the single gap most likely to affect the
  accuracy of the MVP candidate or core requirements, and why>
- **Overall research completeness:** `High | Medium | Low` <judgment call —
  should reflect the OBSERVED vs. INFERRED vs. UNKNOWN mix from the Product
  Overview confidence summary>

---

## Example (filled)

- **Gap ID:** GAP-002
- **Area:** Settings
- **Description:** Only workspace-level settings were observed; user-level
  account settings (notification preferences, profile fields) were not
  reachable because the demo session did not expose a "My account" page.
- **Why the evidence is missing:** No authenticated user-owned account was
  available beyond a shared/demo login state with limited settings surface.
- **Impact:** Any notification-preference or profile-related requirements
  are absent from this report, even though a user-level settings area likely
  exists.
- **Related open question(s):** "Does the product expose per-user
  notification preferences separate from workspace settings, and if so, what
  options are available?"
- **Suggested next step:** Re-run this investigation with the user's own,
  explicitly authorized account credentials to reach account-level settings.
