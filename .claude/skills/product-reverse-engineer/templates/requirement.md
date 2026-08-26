# Template: Requirement

One instance per functional or non-functional requirement, produced in
Phase 4 (Generate requirements) per `references/requirements-methodology.md`.
Feeds the Functional Requirements / Non-Functional Requirements sections of
the final report.

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`. A
requirement should generally not be written at all if its classification
would be `UNKNOWN` — route those to Open Questions instead.

---

## Requirement: <short title>

- **Requirement ID:** REQ-<NNN>
- **Type:** `Functional | Non-Functional`
- **Requirement:** <"the system shall..." — one behavior, testable, precise>
- **Priority:** `Must | Should | Could` <MoSCoW, based on how central this
  appears to the product's core value — note this is a judgment call>
- **Evidence:** <URL(s), screenshot reference(s), exact interaction(s)>
- **Classification:** `OBSERVED | INFERRED`
- **Confidence:** `High | Medium | Low`
- **Acceptance criteria:**
  - Given <observed starting state>,
    When <observed action>,
    Then <observed or inferred result — mark inline as [INFERRED] if the
    "Then" clause was not directly witnessed>.

---

## Example (filled)

- **Requirement ID:** REQ-012
- **Type:** Functional
- **Requirement:** The system shall display an inline validation error when
  the invite-teammate form is submitted with an invalid email address.
- **Priority:** Should
- **Evidence:** /settings/team page, screenshot ref invite-02
- **Classification:** OBSERVED
- **Confidence:** High
- **Acceptance criteria:**
  - Given the "Invite" form is open on the team settings page,
    When the user submits with an email missing an "@" symbol,
    Then an inline error reading "Enter a valid email address" is shown
    beneath the field and the form is not submitted.

## Example (Non-Functional, filled)

- **Requirement ID:** REQ-021
- **Type:** Non-Functional
- **Requirement:** The system shall render the marketing homepage layout
  responsively across desktop and mobile viewport widths.
- **Priority:** Should
- **Evidence:** Homepage observed at 1440px and 375px viewport widths;
  layout reflows to a single column with a collapsed nav menu below 768px.
- **Classification:** OBSERVED
- **Confidence:** Medium
- **Acceptance criteria:**
  - Given the homepage is loaded at a viewport width below 768px,
    When the page renders,
    Then the primary navigation collapses into a menu icon and page content
    reflows to a single column.
