# Template: Product Capability

One instance per meaningful product capability identified during Phase 3
(Analyze features, capabilities, and user journeys), per
`references/product-capability-discovery.md`. Feeds the **Key Product
Capabilities** section of the final report — a capability documented here
must also get its own entry in that section, not just a mention inside a
Feature or User Journey.

A capability is not the same thing as a feature (see
`product-capability-discovery.md`'s "Feature vs. capability"). Use
`templates/feature.md` for the UI-level building blocks and this template
for the higher-level ability those building blocks combine to produce.

Classification must be one of: `Observed` | `Inferred` | `Assumed` |
`Unknown` (note: this is a four-tier scale, wider than the core three-tier
OBSERVED/INFERRED/UNKNOWN used elsewhere in the report — see
`product-capability-discovery.md`'s "Confidence tiers for capabilities" for
why).

---

## Capability: <name — a short noun phrase naming the ability, not the UI>

- **Capability ID:** CAP-<NNN>
- **User goal:** <what the user is fundamentally trying to accomplish>
- **What the product enables:** <the ability itself, stated plainly — "helps
  the user turn a vague instruction into a precise, actionable requirement,"
  not "has a preview page">
- **Initial user input:** <what the user starts with — often informal,
  partial, or ambiguous>
- **System interpretation:** <what the product does with that input before
  responding — parsing, inferring intent, structuring>
- **Suggestions / guidance provided:** <concrete suggestions, recommendations,
  or guidance the system actually offered — quote real copy/labels where
  possible, not a paraphrase>
- **User interaction with suggestions:** <how the user acts on what the
  system offered — select, edit, reject, combine>
- **Refinement loop:** <how the input evolves across rounds — describe at
  least one full round-trip: input → system response → user refinement →
  updated response. Note how many rounds were actually observed vs. assumed
  to continue similarly>
- **System feedback on refinement:** <what changes in response to the
  refined input — a changed preview, an updated suggestion set, a narrowed
  set of options>
- **Final result / output:** <what the user ends up with, and how it differs
  from the initial input>
- **Supporting UI/features:** <the Feature IDs and/or pages/elements that
  participate — this capability is built from them, not identical to any one
  of them>
- **UX significance:** <what this behavior does for the user experience —
  reduces ambiguity, lowers effort, teaches the product, builds trust,
  prevents a dead end, etc.>
- **Why it's important / differentiating:** <why this is worth calling out
  specifically — what would using the product be like without it>
- **Evidence:** <URL(s), screenshot reference(s), transcript/history
  reference(s), exact interaction(s) this is based on>
- **Confidence:** `High | Medium | Low`
- **Classification:** `Observed | Inferred | Assumed | Unknown`

---

## Example (filled — the canonical case)

- **Capability ID:** CAP-002
- **User goal:** Turn a one-line, informal idea into a working result without
  having to fully specify it up front.
- **What the product enables:** Interactive requirement refinement — the
  product helps the user turn an initial, often vague instruction into a
  clearer, more precise requirement through interpretation, contextual
  suggestions, and iterative refinement, with the live preview reflecting
  each round.
- **Initial user input:** A single free-text prompt, e.g. "Create a web app
  for an ecommerce site for costumes."
- **System interpretation:** The product parses the prompt for intent (here:
  commerce), and visibly discloses its reasoning before acting (e.g. "I'll
  set up Shopify as the backend for product catalog, inventory, and
  checkout").
- **Suggestions / guidance provided:** An inline actionable step surfaced as
  a button in the response itself ("Set up Shopify store"), followed by a
  set of low-friction next-step suggestions after the first build completes
  (e.g. "Add costume catalog," "Build checkout flow").
- **User interaction with suggestions:** The user can tap a suggested next
  step directly instead of typing a new instruction, or ignore the
  suggestions and type a free-form refinement instead.
- **Refinement loop:** Round 1 — initial prompt produces a working but
  incomplete result (storefront with no products) and the system proactively
  names the gap and asks a clarifying question. Round 2 (available, not
  directly walked this session) — the user answers or taps a suggestion chip,
  and the system updates the live preview accordingly. Only round 1 was
  directly observed; round 2's mechanics are INFERRED from the consistent
  chat-driven update pattern seen throughout the transcript.
- **System feedback on refinement:** The live preview updates in place after
  each accepted step, and the assistant explicitly states what was verified
  ("...are all working, and the build passes") before naming the next gap.
- **Final result / output:** A working, previewable application whose scope
  and shape were arrived at through several rounds of prompt → build →
  gap-identification → refinement, rather than fully specified up front.
- **Supporting UI/features:** FEAT-001 (Conversational app generation),
  FEAT-002 (Live editable preview), the chat's inline action buttons, the
  next-step suggestion chips.
- **UX significance:** Removes the burden of writing a complete spec before
  getting a result; keeps the user in a tight, low-effort loop of "look at
  what happened → decide what's next," which lowers the cognitive load of
  going from vague intent to a concrete outcome.
- **Why it's important / differentiating:** This loop — not the existence of
  a chat box by itself — is the product's core value proposition. A version
  of this product without the interpret/suggest/refine loop would just be a
  one-shot code generator; the loop is what makes it usable by someone who
  doesn't yet know exactly what they want.
- **Evidence:** Project workspace chat history (screenshot/transcript refs
  chat-01 through chat-06); suggestion chips observed in the same transcript.
- **Confidence:** Medium (round 1 fully observed; later rounds inferred from
  a consistent pattern, not independently walked)
- **Classification:** Inferred
