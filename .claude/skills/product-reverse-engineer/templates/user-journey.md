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

If the actor and system trade turns more than once, with each round
narrowing toward a result — e.g. the system suggests, the actor refines, the
system updates its response, the actor refines again — do not flatten this
into one row. Either repeat the relevant step numbers as separate rows per
round (2a, 2b, 2c...) or add an explicit "Iteration / refinement loop"
subsection below describing the loop and how many rounds were actually
observed vs. assumed to continue similarly. This is very often where a real
product capability lives — see `references/product-capability-discovery.md`
— and if this journey demonstrates one, cross-reference its `CAP-<NNN>` here
rather than leaving the loop implicit in the steps table.

### Iteration / refinement loop (if applicable)

- **Related capability:** CAP-<NNN> (if this journey demonstrates a
  documented capability)
- **What starts the loop:** <the actor's initial input>
- **What the system offers each round:** <suggestions/guidance/feedback —
  concrete, not paraphrased>
- **How the actor responds each round:** <accept, edit, reject, refine>
- **Rounds actually observed:** <n> — <what changed between them,
  specifically>
- **How the loop ends:** <actor satisfied, actor abandons, system reaches a
  terminal state>

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
