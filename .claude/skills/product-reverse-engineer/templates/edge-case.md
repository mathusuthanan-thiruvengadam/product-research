# Template: Edge Case

One instance per boundary condition identified during Phase 4 (Generate
requirements) per `references/requirements-methodology.md`. Edge cases must
be derived from an observed behavior's boundary — never invented
independently of anything actually seen.

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`. Edge
cases are almost always `INFERRED` unless the boundary itself was actually
triggered and witnessed.

---

## Edge Case: <short description>

- **Edge Case ID:** EC-<NNN>
- **Related feature/requirement:** <Feature ID and/or Requirement ID this
  boundary relates to>
- **Boundary condition:** <the specific edge — e.g. "zero results", "maximum
  field length", "last item in a paginated list", "duplicate submission">
- **Expected/observed behavior:** <what happens at this boundary — state
  clearly whether this was witnessed or is a deduction>
- **Rationale:** <why this boundary is implied by the observed design — e.g.
  "pagination was observed, so a last-page boundary must exist">
- **Evidence:** <source, if the boundary was actually triggered>
- **Confidence:** `High | Medium | Low`
- **Classification:** `OBSERVED | INFERRED | UNKNOWN`

---

## Example (filled)

- **Edge Case ID:** EC-005
- **Related feature/requirement:** FEAT-003 (Invite teammate), REQ-012
- **Boundary condition:** Inviting an email address that is already a
  member of the workspace.
- **Expected/observed behavior:** Not witnessed directly; inferred that the
  system likely rejects or deduplicates the invite given that the "Pending
  invites" list did not allow duplicate entries when the same email was
  entered twice in a row during testing.
- **Rationale:** Observed that submitting the same email twice in immediate
  succession only produced one entry in "Pending invites," suggesting
  server-side deduplication logic exists.
- **Evidence:** screenshot ref invite-dup-01 (showing single resulting entry
  after two submissions)
- **Confidence:** Medium
- **Classification:** INFERRED
