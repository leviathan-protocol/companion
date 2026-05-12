---
slug: revocation_right
element_type: RULE
mutability: LOCKED
inline: true
current_version: 1
contentURI: null
---

User may revoke any mediated action (auto-vote, agent-issued message, persona-match exposure, delegated authority) within 24 hours of the action. Revocation requested via the implementation's audit surface triggers: (1) cleanup of the action's downstream effects where reversible, (2) flagging of the action as revoked in immutable logs, (3) protocol-level retraction (e.g., on-chain vote retraction within voting window).

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this rule operationalizes

Concrete implementation of the revocation guarantee in `identity_sovereignty` and `transparent_mediation`. The 24-hour window balances:
- User has time to wake, review, decide
- Protocol can make commitments stable for downstream consumers (after 24h, an action is "finalized")
- Voting windows are typically multi-day, so on-chain effects can still be retracted

## Enforcement mechanisms

1. **Audit log includes revocation status** — every mediated action's record carries a `revocable_until` timestamp
2. **Revocation API** — implementations provide a `revoke(action_id, reason?)` flow
3. **Downstream propagation** — if the action was already submitted on-chain or to forum, revocation triggers the appropriate retraction API
4. **Immutable record of revocation** — the original action stays in the log (not deleted), marked as revoked, with timestamp + optional reason

## Edge cases

- **Past 24-hour window:** revocation no longer reverses effects, but user can still flag the record (for future audit + standing impact on agent)
- **Already-finalized vote:** if voting window has closed and the proposal is now in validator alignment check phase, retraction triggers a "vote count amendment" event (rare; voting window is usually shorter than 24h)
- **Multi-party action:** if the action involved another user (e.g., Companion-to-Companion conversation), revocation invalidates the user's contribution but doesn't necessarily delete the other party's record

## Why locked

The 24-hour window may need adjustment based on user feedback or empirical voting window analysis. Locking allows governance vote to tune the window without making the underlying guarantee alterable.

## Related elements

- `identity_sovereignty` — parent principle establishing right
- `transparent_mediation` — parent principle establishing audit-ability
- `advisory_validator_eligibility` — auto-contribution is one specific class of revocable mediation
