# Product Capability Discovery

This document explains how to find and document **product capabilities** —
meaningful abilities the product gives the user that emerge from *how it
behaves during interaction*, not just from its inventory of pages and UI
elements. It supports `SKILL.md` Phase 2 (exploration) and Phase 3
(synthesis). It does not introduce new permissions or relax the evidence
discipline in `SKILL.md` — every capability still needs an evidence tag.

## The rule this document exists to enforce

> Do not summarize a product only by enumerating its pages, screens, menus,
> UI elements, and obvious features. Analyze how the product behaves during
> user interaction and identify the meaningful capabilities that emerge from
> that behavior. If the product actively assists, guides, interprets,
> recommends, refines, adapts, or provides iterative feedback to the user,
> treat that behavior as a first-class product capability and explicitly
> highlight it in the final report.

A report that lists every page and button but misses this is *incomplete*,
even if every individual observation in it is accurate. Accuracy at the
element level does not substitute for correctness at the capability level.

## Feature vs. capability

These are two different altitudes of description. Both are required; neither
replaces the other.

- **Feature** — what functionality exists. A named, boundable piece of UI or
  functionality: a page, a button, an input, a panel. Answers "what's here?"
- **Capability** — what the product actually *enables the user to do* through
  the interaction of one or more features and the system's behavior around
  them. Answers "what does this let someone accomplish, and how does the
  product help them get there?"

Worked example (the canonical case this document is built around):

| Altitude | Description |
|---|---|
| Feature | Preview page. Text input. Suggestion buttons. |
| Capability | **Interactive requirement refinement** — the product helps the user turn an initial, possibly vague instruction into a clearer, more precise requirement by interpreting the input, offering contextual suggestions, and letting the user iteratively refine it until the live preview reflects what they actually meant. |

The feature-level description is not wrong — it just isn't the important
sentence. The capability-level description is what makes a reader understand
*why this product is good at what it does*. The final report must contain
the second kind of sentence, explicitly, not force the reader to infer it
from three separate feature bullets.

A capability frequently has **no dedicated page of its own**. It emerges from
the interaction between several UI elements and system responses, often
spread across a single flow:

```
user input → system interpretation → suggestions → user refinement →
system feedback → further refinement → result
```

Do not assume a capability must correspond to a named feature, a settings
toggle, or a menu item to count. If you only look for capabilities where the
product has a labeled section for them, you will miss most of them — that is
exactly the failure mode this document exists to prevent.

## What to look for during exploration

While working through `exploration-methodology.md`'s items (especially
Feature discovery, User journeys, Forms, Buttons/actions), keep a second,
parallel question running: **not just "what does this element do," but "does
the product actively do something *for* the user here, beyond executing a
direct command?"**

Watch specifically for the product:

- interpreting user input (parsing free text, inferring intent, structuring
  something unstructured)
- guiding the user (multi-step flows, wizards, "next step" prompts)
- suggesting or recommending something (chips, autocomplete, "you might also
  want," ranked options)
- helping the user formulate or clarify a requirement/goal
- reducing ambiguity (clarifying questions, disambiguation prompts)
- improving or refining what the user already provided
- offering contextual choices that change based on prior input
- adapting its response based on previous interaction (memory within a
  session, personalization, changing UI based on history)
- giving iterative feedback (each round trip narrows toward a result)
- anticipating a need before the user asks (smart defaults, pre-filled
  fields, proactive warnings)
- reducing the user's effort (bulk actions, batch operations, one-click
  flows that would otherwise take many steps)
- helping the user discover functionality they didn't know to look for
  (progressive disclosure, contextual help, empty-state nudges)
- converting vague input into a structured outcome
- running an iterative interaction loop of any kind

This is a general pattern-recognition task, not an AI-product-specific one.
The same lens finds: smart defaults, guided workflows, contextual
recommendations, autocomplete, progressive disclosure, interactive previews,
wizards, intelligent validation, automatic error correction, personalization,
adaptive UI, bulk actions, workflow automation, contextual help,
recommendation systems, conversational interactions, real-time feedback, and
undo/recovery mechanisms — wherever any of these are actually present.
Discover them because they're there; never add one because a similar product
"usually" has it (see Evidence discipline, below).

### Test loops live, don't just note their presence

If you find a control that looks like it starts an iterative or adaptive
interaction (a suggestion chip, a "refine" action, an autocomplete dropdown,
a wizard step), and exercising it is safe (no destructive/real-money/
real-communication action, per `SKILL.md`'s safety boundaries), walk it
through **at least two rounds**, not one. A single round only tells you the
control exists. A second round is what shows you whether the system actually
adapts — whether the second suggestion set differs based on the first
choice, whether the preview genuinely updates, whether the loop converges.
That difference is the evidence a capability claim needs to be OBSERVED
rather than INFERRED.

If exercising the loop isn't safely possible (e.g. it would consume a paid
credit, send a real message, or requires data you don't have), reconstruct
what you can from any existing evidence available to you (e.g. a persisted
chat/history transcript, a completed example already in the product) and
label the reconstruction INFERRED, per the worked example this methodology
is drawn from — but still name and describe the capability explicitly. A
capability being INFERRED rather than OBSERVED is not a reason to omit it or
demote it to a passing mention inside a feature bullet.

## Documenting a capability

Use `templates/capability.md` for every capability identified. Give each one
an ID (`CAP-<NNN>`) so it can be cross-referenced from the Feature Inventory,
User Journeys, Functional Requirements, and Navigation Mapping sections —
capabilities are a synthesis layer that sits *above* those, not a replacement
for them.

A capability entry must answer, specifically:

- What does the user initially provide?
- What does the application do with it (interpretation, not just storage)?
- What suggestions/guidance/feedback does it provide, concretely (actual copy
  or behavior seen, not a paraphrase of "helpful suggestions")?
- How does the user interact with those suggestions?
- How does the user refine their input, and how does the system respond to
  the refinement?
- What is the final result, and how does it differ from what the user
  started with?
- Why does this matter — what would using the product be like *without* this
  behavior (i.e. what is the counterfactual: manual entry with no help, a
  single-shot command with no iteration, a dead end with no guidance)?

### Confidence tiers for capabilities

Capabilities use a fourth tier beyond `SKILL.md`'s core three, because a
capability claim has two separable parts: *that the behavior exists* and
*why it matters*. The behavior itself follows the normal OBSERVED / INFERRED
/ UNKNOWN discipline. The significance judgment (UX impact, why it's
differentiating) is sometimes a reasonable interpretation grounded in
observed behavior but not itself something you can point a screenshot at —
that judgment gets tagged `ASSUMED`.

| Tag | Meaning |
|---|---|
| **Observed** | The interaction loop (or at least two full rounds of it) was directly witnessed. |
| **Inferred** | The capability's existence is a reasonable deduction from OBSERVED fragments (e.g. reconstructed from a persisted transcript, or a single round witnessed with the rest implied by consistent UI affordances). |
| **Assumed** | Not directly evidenced, but reasonably assumed given a strong contextual signal (e.g. marketing copy explicitly describing the behavior, a UI affordance whose only plausible purpose is this capability) — used sparingly, and always said aloud as an assumption, never silently upgraded. |
| **Unknown** | A UI affordance suggests a capability might exist, but there isn't enough to say anything concrete about it. |

Never invent a capability because it would be typical for the product
category. Every capability entry must trace to something actually seen —
`ASSUMED` narrows the gap between OBSERVED and pure speculation; it does not
license speculation.

## How capabilities connect to the rest of the report

- **Key Product Capabilities section** — every documented capability is
  listed here explicitly, per `SKILL.md`'s Output structure. This is the
  section a reader should be able to open and immediately see the product's
  meaningful behaviors, without assembling them from scattered feature
  bullets. See `## Anti-burial rule` below.
- **User Journeys** — when a journey contains an iterative/refinement loop,
  represent the loop explicitly (see the "Iteration / refinement loop"
  guidance in `templates/user-journey.md`) and cross-reference the relevant
  `CAP-<NNN>`.
- **Feature Inventory** — features that participate in a capability should
  note which capability they support (e.g. "supports CAP-002") rather than
  being described as if they were self-contained.
- **Navigation Mapping** — the site map should be able to answer "where is
  this capability exposed, and what UI elements/pages participate in it?" —
  see the navigation-mapping guidance in `exploration-methodology.md`.
- **Functional Requirements** — write at least one FR describing the
  capability's overall behavior (e.g. "the system shall let the user
  iteratively refine an initial input via contextual suggestions until the
  preview reflects the refined intent"), in addition to, not instead of, the
  granular per-step FRs. Cross-reference the `CAP-<NNN>` in the FR's
  evidence.

## Anti-burial rule

A capability must never be reduced, in the final report, to a single
sentence embedded inside a generic feature or use-case description (e.g.
"Preview page allows the user to enter instructions and see the result" when
what was actually observed is an interpret → suggest → refine → update loop).
If a capability is significant enough to document with the template, it is
significant enough to have its own entry in the Key Product Capabilities
section that a reader can find without inferring it from prose elsewhere.

## Capability-discovery checkpoint (run before finalizing the report)

Before Phase 6 (final output), verify:

- [ ] Have all major user-facing capabilities been identified, not just
      pages/screens/features?
- [ ] Did I identify capabilities beyond individual pages/UI elements —
      ones that emerge from interaction between several elements?
- [ ] Did I identify interactive/iterative behaviors specifically (loops,
      not just single request/response pairs)?
- [ ] Did I identify suggestion/recommendation mechanisms, wherever present?
- [ ] Did I identify places where the product actively assists, guides, or
      interprets, rather than just executing direct commands?
- [ ] Did I identify behaviors that reduce user effort or cognitive load?
- [ ] Did I identify differentiating UX/product capabilities — the ones that
      would make someone choose this product over a bare-bones equivalent?
- [ ] Did I accidentally describe any of the above only as a page or UI
      element, without naming the capability itself?
- [ ] Are any important capabilities buried inside a generic feature or
      use-case description instead of surfaced in Key Product Capabilities?

If something important surfaced during research but isn't represented
explicitly in the final report, add it before calling the research done —
per `quality-checklist.md`'s rule that no surfaced gap is silently dropped.
