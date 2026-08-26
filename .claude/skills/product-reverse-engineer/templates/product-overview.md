# Template: Product Overview

One instance per research run. This is the top-level summary that opens the
final report (`SKILL.md` Output Structure, section 1: Executive Summary, and
section 2: Scope & Method).

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`.

---

## Product Overview

- **Product name:** <as observed on the site — from title, header, or logo alt text>
- **Entry URL(s):** <the URL(s) research started from>
- **One-line summary:** <what the product appears to do, in one sentence>
- **Apparent target user(s):** <who this seems built for>
  - Classification: `OBSERVED | INFERRED | UNKNOWN`
  - Evidence: <marketing copy, pricing page language, persona cues, etc.>
- **Apparent core value proposition:** <the main problem it claims to solve>
  - Classification: `OBSERVED | INFERRED | UNKNOWN`
  - Evidence: <source>
- **Product category (best guess):** <e.g. "project management SaaS", "e-commerce storefront">
  - Classification: `INFERRED` (this is almost always a judgment call, not a direct observation)

## Scope & Method

- **Research date/window:** <when this investigation was conducted>
- **Tooling used:** <browser automation (e.g. claude-in-chrome) | static fetch (WebFetch/WebSearch) | mixed>
- **Effect of tooling on evidence quality:** <note any resulting gaps, e.g. "no JS-rendered content or loading states observed because only static fetching was available">
- **Access level:** <public/unauthenticated only | authenticated with user-supplied, user-owned credentials>
- **Explicit out-of-scope items:** <anything the user asked to exclude, or that was excluded per SKILL.md's safety boundaries>
- **Pages/sections not reached:** <and why — auth wall, out of scope, time-boxed, etc.>

## Confidence summary

A quick roll-up so a reader can gauge overall reliability before reading the
full report.

| Evidence tier | Approx. count of findings |
|---|---|
| OBSERVED | <n> |
| INFERRED | <n> |
| UNKNOWN | <n> |

---

## Example (filled)

- **Product name:** Acme Boards
- **Entry URL(s):** https://acmeboards.example.com
- **One-line summary:** A kanban-style task board for small teams.
- **Apparent target user(s):** Small teams / startups managing shared task lists.
  - Classification: INFERRED
  - Evidence: Homepage hero copy: "Built for teams of 2–20."
- **Apparent core value proposition:** Faster, simpler task tracking than
  heavier PM tools.
  - Classification: INFERRED
  - Evidence: Comparison table on /pricing contrasting "Acme Boards" vs.
    "legacy PM tools" on setup time.
- **Product category (best guess):** Lightweight project/task management SaaS.
  - Classification: INFERRED
