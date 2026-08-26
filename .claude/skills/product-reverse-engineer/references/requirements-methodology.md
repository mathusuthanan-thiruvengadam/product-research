# Requirements Methodology

This document explains how to convert observed product behavior (gathered
per `exploration-methodology.md`) into structured requirements artifacts:
features, user stories, functional requirements, non-functional
requirements, acceptance criteria, and edge cases. It supports `SKILL.md`
Phase 5 (Synthesis).

## The core rule: evidence before synthesis

Every artifact produced by this methodology must trace back to something
recorded during exploration, tagged OBSERVED, INFERRED, or UNKNOWN as
defined in `SKILL.md`. Synthesis is *organizing and articulating* evidence
already gathered — it is never a license to add plausible-sounding
functionality that wasn't actually found.

Before writing any requirement, ask:
1. What specific evidence supports this? (page, interaction, response,
   screenshot reference)
2. Is this OBSERVED (directly witnessed), INFERRED (a reasonable deduction
   from OBSERVED evidence), or does it require labeling as UNKNOWN?
3. Would a skeptical reader, given only the cited evidence, reach the same
   conclusion?

If the answer to (3) is no, the requirement is too speculative — soften it,
move it to "Open Questions," or drop it.

### Prohibited moves

- Do not fill gaps with "industry standard" assumptions about what a product
  in this category *usually* has, and present them as requirements. If it
  wasn't observed or reasonably inferable from this specific product's
  observed behavior, it belongs in Open Questions or is simply omitted.
- Do not upgrade an INFERRED item to OBSERVED for narrative convenience.
- Do not merge two unrelated observations into a requirement that implies a
  connection that wasn't actually witnessed.
- Do not soften an UNKNOWN into a vague requirement that reads as if it were
  known (e.g. avoid "the system likely supports X" phrased as a requirement
  — that belongs in Open Questions, not Functional Requirements).

---

## Features

A feature is a named capability with a clear purpose, derived from grouping
related observations (UI elements, journeys, forms, actions) discovered
during exploration.

Template:
```
### Feature: <name>
Evidence tier: OBSERVED | INFERRED
Description: <what it does, in one or two sentences>
Evidence: <pages/interactions this is based on>
```

Group at the level a PM would recognize — not so granular that every button
is its own "feature," not so broad that unrelated capabilities get merged.

## User stories

Only write a user story for a feature with at least OBSERVED-level evidence
of its existence (the mechanism to inform *how* it behaves can be INFERRED,
but the feature's existence itself should not rest purely on inference).

Format:
```
As a <observed or clearly implied user role>,
I want to <action, tied to an observed feature>,
so that <benefit — label as INFERRED if the "why" wasn't stated by the
product itself, e.g. in marketing copy>.

Evidence: <source>
```

If the user role itself is unclear from the product (e.g. it's ambiguous
whether this is aimed at individuals or teams), say so rather than picking
one arbitrarily.

## Functional requirements

Phrased as "the system shall..." statements, each directly traceable to one
or more pieces of evidence.

Format:
```
FR-<n>: The system shall <observable behavior>.
Evidence tier: OBSERVED | INFERRED
Evidence: <source(s)>
```

Rules:
- One behavior per requirement — don't bundle multiple behaviors into one
  FR just because they were seen on the same page.
- Prefer precise, testable phrasing over vague phrasing (e.g. "the system
  shall display a validation error when the email field is left blank" is
  better than "the system shall validate the email field").
- If a requirement can only be partially confirmed (e.g. the trigger was
  seen but not the full resulting behavior), say exactly what part is
  OBSERVED and what part is INFERRED within the same entry rather than
  picking one tag for the whole thing.

## Non-functional requirements

Only include an NFR when there is genuine observed evidence for it. Do not
generate a standard NFR checklist (performance, security, scalability,
accessibility) and fill it in with assumptions — an absent NFR category is
better than a fabricated one.

Valid sources of NFR evidence:
- Observed responsive behavior across viewport sizes.
- Observed accessibility attributes (semantic HTML, ARIA labels, visible
  focus states, alt text) actually present in the rendered page.
- Observed performance characteristics (e.g. page load behavior, whether
  content streams in progressively) — only if actually measured/witnessed,
  not guessed.
- Observed security-relevant UI behavior (e.g. password strength meter,
  session timeout messaging) — note only what's UI-visible; do not attempt
  to test actual security properties.

Format matches functional requirements:
```
NFR-<n>: The system shall <observable quality attribute>.
Evidence tier: OBSERVED | INFERRED
Evidence: <source(s)>
```

If no NFR has real evidentiary support, the Non-Functional Requirements
section should say so explicitly rather than being silently omitted or
padded.

## Acceptance criteria

Written per functional requirement, in Given/When/Then form, describing the
observed (or reasonably inferred) behavior precisely enough that someone
could verify it against the real product.

Format:
```
AC for FR-<n>:
Given <observed starting state>,
When <observed action>,
Then <observed or inferred result>.
```

If the "Then" clause is INFERRED rather than OBSERVED, say so inline (e.g.
"Then [INFERRED] a confirmation email is likely sent" ) rather than stating
it as a confirmed outcome.

## Edge cases

Edge cases are boundary conditions *implied by the observed design* — not
new invented features. Derive them by asking, for each OBSERVED behavior,
"what happens at the boundary of this?" (e.g. if pagination was observed,
"what happens on the last page / with exactly one result / with zero
results?").

Format:
```
EC-<n>: <boundary condition>
Related to: FR-<n> / Feature <name>
Evidence tier: INFERRED (edge cases are almost always INFERRED unless the
boundary was actually triggered and witnessed)
Rationale: <why this boundary is implied by the observed behavior>
```

Do not generate edge cases unrelated to anything observed (e.g. don't
speculate about concurrency or race conditions unless there was some
observed hint of multi-user/real-time behavior).

---

## Final self-check before finalizing any requirement

- Can I point to the exact evidence for this? If not, is it correctly
  labeled INFERRED or moved to Open Questions?
- Have I avoided stating an assumption as a fact anywhere in this artifact?
- Would removing my own domain-category assumptions change this
  requirement? If yes, it's not sufficiently evidence-based yet.

See `quality-checklist.md` for the full completeness check to run before
considering the research finished.
