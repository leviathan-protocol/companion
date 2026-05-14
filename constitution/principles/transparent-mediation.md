---
slug: transparent_mediation
element_type: PRINCIPLE
mutability: LOCKED
inline: true
current_version: 1
contentURI: null
---

Any AI mediation between the user and other parties — whether forum contributions, agent-to-agent conversations, alignment-check verdicts, or auto-contributions — must be auditable by the user. The user may review the full reasoning, message log, and decision trail of any mediation. The user retains unilateral revocation authority.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this principle establishes

AI agents acting on a user's behalf are delegates, not autonomous representatives. The user must always be able to see what the agent did, why, and to undo it. This is the trust contract between user and on-device AI.

## Enforcement mechanisms

1. **Full audit log** — every mediated action (auto-vote, agent reply, persona-match) recorded with timestamp, reasoning, input context
2. **Reviewable surface** — implementations expose this log in a clear UI (e.g., Anima's "Activity" or "Logs" view)
3. **Revocation flow** — user can revoke any past mediated action with one tap; revocation triggers protocol cleanup (e.g., on-chain vote retraction if revoked within voting window)
4. **No silent action** — implementations must not perform consequential mediated actions without making them visible

## Why locked (not immutable)

Implementation details of audit surfaces may evolve (e.g., better UX, mobile-specific patterns), but the principle itself (mediation must be auditable + revocable) is constitutional. Locking allows refinement through governance vote without making the core right alterable by individual implementations.

## Implementation notes

- Anima v1 LogsSheet (mirrorX Wave 7) provides the audit surface
- Auto-contribution feature (Wave 10) submits with `mediated_by: anima_advisory_v1` attribution, fully reviewable
- Revocation: forum API supports `DELETE /vote/{id}` within window; chain reflects retraction

## Related elements

- `identity_sovereignty` — parent principle
- `revocation_right` — concrete revocation rule
- `advisory_validator_eligibility` — opt-in conditions for one specific mediation type
