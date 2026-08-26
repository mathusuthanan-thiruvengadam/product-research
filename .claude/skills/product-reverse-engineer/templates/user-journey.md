# Template: User Journey

One instance per end-to-end journey reconstructed during Phase 3. Feeds the
User Journeys section of the final report.

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`, applied
per step where steps differ in evidence quality (a journey can be partly
OBSERVED and partly INFERRED — tag each step, not just the journey as a whole).

---

## Journey: <name>

- **Journey ID:** UJ-<NNN>
- **Actor:** <who undertakes this journey — role/persona>
- **Goal:** <what the actor is trying to accomplish>
- **Preconditions:** <state required before the journey starts — e.g.
  "actor has no existing account">

### Steps

| # | Step (actor action) | System response | Evidence | Classification |
|---|---|---|---|---|
| 1 | <action> | <observed response> | <source> | OBSERVED / INFERRED / UNKNOWN |
| 2 | ... | ... | ... | ... |

### Alternative paths

<branches off the main path that were observed or inferred — e.g. "skip
onboarding," "sign up with Google instead of email">

- **Alt path A:** <description, evidence, classification>

### Failure paths

<what happens when a step fails or is abandoned, to the extent observable>

- **Failure at step <n>:** <what was observed — validation error, dead end,
  timeout, etc.>

- **End state:** <where the actor ends up when the journey completes
  successfully — e.g. "lands on the workspace dashboard with an empty state
  shown">

---

## Example (filled)

- **Journey ID:** UJ-001
- **Actor:** New visitor (no existing account)
- **Goal:** Create an account and reach the main product surface
- **Preconditions:** Not logged in; no existing workspace

### Steps

| # | Step (actor action) | System response | Evidence | Classification |
|---|---|---|---|---|
| 1 | Visit homepage, click "Get started" | Navigates to /signup | homepage screenshot, nav-01 | OBSERVED |
| 2 | Fill email + password, submit | Redirects to /onboarding/welcome | signup-01 | OBSERVED |
| 3 | Complete 2-step onboarding wizard | Redirects to /dashboard | onboarding-01, onboarding-02 | OBSERVED |
| 4 | (implied) Verification email sent | Not directly observed — no test email account used | — | INFERRED |

### Alternative paths

- **Alt path A — Google sign-in:** "Continue with Google" button visible on
  /signup; not exercised (would require a real Google account). Presence of
  the button is OBSERVED; resulting flow is UNKNOWN.

### Failure paths

- **Failure at step 2:** Submitting with a password under 8 characters shows
  inline error "Password must be at least 8 characters." (OBSERVED)

- **End state:** Actor lands on /dashboard showing an empty-state illustration
  and a "Create your first board" call to action. (OBSERVED)
