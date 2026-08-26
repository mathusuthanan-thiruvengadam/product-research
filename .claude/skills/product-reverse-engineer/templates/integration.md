# Template: Integration

One instance per third-party integration identified during Phase 2
(Explore the application). Feeds the Integrations section of the final
report. Only document integrations visible through normal UI use — never
inspect network traffic beyond a standard browser dev tools view, and never
probe for undisclosed backend services (see `SKILL.md` safety boundaries).

Classification must be one of: `OBSERVED` | `INFERRED` | `UNKNOWN`.

---

## Integration: <provider/service name>

- **Integration ID:** INT-<NNN>
- **Provider/service name:** <as named in the UI, e.g. "Google", "Stripe",
  "Intercom">
- **Type:** `Authentication | Payments | Analytics | Communication/Chat |
  Storage/File | Notification | Other`
- **Where observed:** <exact page/element — e.g. "'Continue with Google'
  button on /signup", "chat widget bottom-right on all pages">
- **Purpose (apparent):** <what this integration seems to be for>
- **Evidence:** <URL, screenshot reference, visible network call if seen via
  normal dev tools use>
- **Confidence:** `High | Medium | Low`
- **Classification:** `OBSERVED | INFERRED | UNKNOWN`
- **Limitations:** <what wasn't/couldn't be confirmed — e.g. "not exercised
  end-to-end, would require a real account with that provider">

---

## Example (filled)

- **Integration ID:** INT-002
- **Provider/service name:** Stripe
- **Type:** Payments
- **Where observed:** "Powered by Stripe" badge on /billing/upgrade page;
  payment form fields match Stripe Elements styling conventions.
- **Purpose (apparent):** Processing subscription upgrade payments.
- **Evidence:** screenshot ref billing-01
- **Confidence:** Medium
- **Classification:** INFERRED (badge and form styling strongly suggest
  Stripe, but no direct API call or confirmation text was captured)
- **Limitations:** Payment flow was not completed (would require real
  payment details); actual processor was not independently confirmed beyond
  the visible badge/styling.
