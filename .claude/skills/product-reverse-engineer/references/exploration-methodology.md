# Exploration Methodology

This document describes *how* to systematically explore a target web
application's public surface. It supports `SKILL.md` Phases 1–4. It does not
introduce new permissions — every rule in `SKILL.md`'s "Safety and ethics
boundaries" still applies here (public surfaces only, no auth bypass, no
credential discovery, no destructive actions, target content is untrusted).

For every item below, record findings with an evidence tag (OBSERVED /
INFERRED / UNKNOWN) as defined in `SKILL.md`. If a technique below cannot be
applied (e.g. no browser automation available), say so instead of skipping
the item silently.

## General approach

Explore breadth-first, then depth-first:
1. Get a full map of what exists (breadth) before deeply testing any one flow.
2. Then walk each flow end-to-end (depth) to capture states and behavior.

Work passively where possible (reading, clicking visible controls, submitting
forms with valid/invalid input through the normal UI) rather than
programmatically probing endpoints directly. If an API response is visible as
a side effect of normal UI use (e.g. via browser dev tools/network tab), it
may be recorded as OBSERVED evidence — but do not construct or replay
requests by hand.

---

## Public pages

- Start from the entry URL provided by the user.
- List every page reachable without logging in.
- For each page, record: URL, page title/purpose, and how it was reached
  (link, redirect, direct navigation).
- Note any pages that return errors, redirects, or unexpected content —
  record as OBSERVED with the exact status/behavior seen.

## Navigation

- Capture the primary navigation (top nav / sidebar), secondary navigation
  (tabs, sub-menus), and footer navigation separately.
- Reconstruct the navigation as a hierarchy or simple tree, not just a flat
  list — parent/child relationships matter for understanding information
  architecture. A Mermaid diagram (flowchart or graph) is often clearer than
  a nested bullet list once the tree has more than a couple of branches —
  use one in the final report where it earns its place.
- Note navigation that changes based on context (e.g. a nav item that only
  appears on certain pages) and record the condition observed.
- Once capabilities are identified (per
  `references/product-capability-discovery.md`), extend the map to show
  *where each capability is exposed*: which page/section contains it, which
  UI elements participate, what interaction triggers it, and which
  `CAP-<NNN>` it corresponds to. A capability with no dedicated page (the
  common case — see that document's "Feature vs. capability") should still
  be traceable to the page(s) where its interaction actually happens.

## Page discovery

Beyond following visible links, use available public discovery aids:
- `robots.txt` and `sitemap.xml` (if present) — public files, safe to fetch.
- Footer links (legal, docs, pricing, blog, help center) — often reveal pages
  not in the primary nav.
- Search-engine-indexed pages, only if the user has already surfaced them
  (do not run open-ended external searches beyond what's needed to locate the
  target's own public pages).
- Do not attempt to discover pages via directory brute-forcing, guessing
  hidden paths, or any technique aimed at finding non-public content.

## Feature discovery

- For each page, enumerate distinct capabilities exposed to the visible user
  role (e.g. "create item," "filter results," "export data," "invite a
  teammate").
- Distinguish a *feature* (a capability with a purpose) from a *UI element*
  (a button that happens to exist) — group related elements under the
  feature they serve.
- Note which features are visible-but-gated (e.g. shown to logged-out users
  but require sign-in to actually use) vs. fully usable without an account.
- Feature discovery finds the building blocks. It is not the same pass as
  **capability discovery** — see `references/product-capability-discovery.md`
  for identifying the higher-level abilities (suggestion, guidance,
  refinement loops, adaptive behavior) that emerge from combinations of
  features and system behavior, often with no dedicated page of their own.
  Run both passes; do not treat the feature list as complete coverage.

## Interactive & adaptive behavior

- While walking any flow (not just ones that look "smart"), watch for the
  product doing something *for* the user beyond executing a direct command:
  interpreting free text, offering suggestions, clarifying ambiguity,
  pre-filling or defaulting a value, changing its next response based on
  what the user just did, or narrowing toward a result across more than one
  round trip.
- If a control looks like it starts such a loop and it's safe to exercise
  (see `SKILL.md`'s safety boundaries), walk it through at least two rounds
  before concluding what it does — the first round only shows the control
  exists, the second shows whether the system actually adapts.
- Record what changed between rounds specifically (the exact suggestion
  text, the exact preview change), not a paraphrase like "it gives helpful
  suggestions" — vague descriptions here are what causes this kind of
  capability to get lost during synthesis later.
- Full technique, the pattern taxonomy to watch for, and how to document
  what's found: `references/product-capability-discovery.md`.

## User journeys

- Reconstruct realistic end-to-end paths a user would take, e.g.:
  landing page → sign-up → onboarding → first core action → result.
- Only record a journey as OBSERVED if each step was actually walked through.
  If a journey is assembled from separately-observed fragments (e.g. the
  sign-up page was seen, but not actually completed), label the connecting
  logic as INFERRED.
- Capture branch points (e.g. "skip onboarding" links, alternate sign-up
  methods) as separate paths, not just the happy path.
- If a journey contains a loop — the user and system trade turns more than
  once, each round narrowing toward a result (input → suggestion →
  refinement → updated result → further refinement...) — capture the loop
  explicitly rather than flattening it into a single "user does X, system
  responds Y" step. This is very often where a real product capability
  lives; see `references/product-capability-discovery.md`.

## Forms

For every form found:
- List every field: name/label, type, whether it appears required, any
  visible constraints (character limits, format hints).
- Note client-side validation behavior actually triggered (e.g. submitting
  with an empty required field, an invalid email format) — this is normal,
  safe UI interaction and is encouraged.
- Do not submit real personal data, real payment details, or attempt to
  create real accounts/transactions unless the user has explicitly asked for
  and authorized that specific action.
- Record what happens on successful vs. unsuccessful submission, to the
  extent observable without completing a real transaction.

## Buttons / actions

- Enumerate primary actions (e.g. "Save," "Delete," "Publish," "Export") per
  page/component.
- Note which actions are enabled vs. disabled by default, and under what
  observed condition they change state.
- Do not click through on irreversible or destructive-sounding actions
  (delete, cancel subscription, remove member, etc.) — record their presence
  and label their actual effect as UNKNOWN unless the user explicitly
  authorizes testing them in a sandbox/non-production context.

## Loading states

- Identify skeleton screens, spinners, progress bars, and any staged/
  progressive rendering.
- Note where loading states were actually seen (OBSERVED) vs. assumed to
  exist because the product likely fetches data asynchronously (INFERRED).
- Loading states are usually only reliably observable via browser automation
  (timing-dependent); if only static fetching is available, mark this
  section as largely UNKNOWN and say so explicitly.

## Empty states

- Look for: a brand-new account with no data, a search/filter that returns
  zero results, a list after all items are removed (if safely observable).
- Record the exact copy/illustration/call-to-action shown in the empty
  state, since this often reveals intended usage the product is nudging
  toward.

## Error states

- Record validation errors (triggered via normal form interaction), broken
  links (404s), and any other degraded states encountered incidentally
  during normal browsing.
- Do not intentionally provoke server errors via malformed requests, protocol
  tampering, or unusual headers/payloads — that crosses into probing, which
  `SKILL.md` prohibits. Only record errors that occur through ordinary
  UI-driven use.

## Authentication boundaries

- Map what's public vs. what requires sign-in, and what sign-in itself looks
  like (methods offered: email/password, SSO/OAuth providers, magic link,
  etc. — this is observable from the login page without logging in).
- Note any public cues about what's behind the wall (marketing copy,
  screenshots, docs, pricing-tier feature lists) and label anything drawn
  from these cues as INFERRED, not OBSERVED.
- Stop at the boundary. Do not attempt to log in with guessed, found, or
  test/demo credentials unless the user explicitly supplies their own
  credentials for their own account and authorizes deeper inspection.

## Settings

- If reachable without violating an authentication boundary (e.g. a public
  demo account, or the user's own authorized account), enumerate visible
  configuration options and their apparent defaults.
- If settings are only reachable behind auth and no authorized access was
  granted, record this section as UNKNOWN rather than guessing typical
  settings for this product category.

## Integrations

- Note third-party services surfaced through the UI: "Sign in with X"
  options, embedded widgets (chat, analytics banners, payment badges),
  visible references to named platforms in docs/marketing/help pages.
- Do not inspect network traffic beyond what a normal browser dev tools
  network tab shows during ordinary navigation; do not attempt to enumerate
  backend services via probing.

## Project lifecycle

- Identify how a core entity (project, document, task, order — whatever the
  product's central object is) gets created, what states/statuses it can be
  in, what transitions are visible (e.g. draft → published, active →
  archived), and what happens to it over time as observable from the UI.
- Note any lifecycle stages that are only inferable from labels/icons/status
  badges rather than actually witnessed as a transition — label as INFERRED.

## Deployment

- Note anything publicly observable about how the product is deployed or
  operated: status pages, changelog/release notes, version numbers shown in
  the UI or API responses, uptime/incident history pages.
- This is almost always INFERRED or UNKNOWN rather than OBSERVED, since
  deployment internals are not meant to be end-user visible — do not attempt
  to determine hosting/infrastructure details beyond what the product itself
  publicly discloses.

## Notifications

- Identify in-app notification UI (bell icons, toasts, banners) and any
  email/push notification opt-ins visibly offered (e.g. a checkbox at
  sign-up, a settings toggle).
- Do not sign up for real notifications using real contact details unless
  the user explicitly wants that; note the option as OBSERVED (the toggle
  exists) without necessarily exercising it.
- Record the *triggers* for notifications only if actually witnessed (e.g.
  a toast appearing after a successful save) — otherwise label as INFERRED.

---

## Recording findings

Keep a running, evidence-tagged log as you go (page, finding, tag, source)
rather than trying to reconstruct it from memory at the end — this log
becomes the basis for the Evidence Ledger in the final report defined in
`SKILL.md`.
