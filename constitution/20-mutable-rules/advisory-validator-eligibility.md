---
slug: advisory_validator_eligibility
element_type: RULE
mutability: MUTABLE
inline: true
current_version: 1
contentURI: null
---

A user's Anima device may act as an advisory-tier validator (submitting non-authoritative verdicts on forum proposals) only when all conditions hold: (1) explicit user opt-in via Settings, (2) device on charger, (3) device on WiFi, (4) device idle ≥10 minutes, (5) user has minimum enactment threshold (≥10 manual enactments), (6) submission rate-limited to ≤20 advisory verdicts per device per 24h.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this rule operationalizes

Concrete conditions for the mobile-as-validator pattern described in `specs/architecture-overview.md` §11.5. Constrains auto-contribution so it cannot be weaponized (spam) or accidentally engaged (battery drain).

## Enforcement mechanisms

1. **Settings opt-in** — Anima's Settings shows the toggle prominently with clear explanation
2. **Device state checks** — background task checks charger + WiFi + idle before each submission
3. **Enactment gate** — user must have accumulated ≥10 manual forum enactments (ratified contributions) before auto-mode unlocks
4. **Rate limiting** — implementation enforces ≤20/24h cap; protocol API enforces same cap server-side
5. **Per-Sub-Leviathan opt-in** — user selects which boards (companion, animal-welfare, etc.) to contribute to

## Why mutable

These parameters are operational: charge threshold, idle minutes, enactment gate, rate limit cap — all should be tunable based on real usage data. As more users join and we see actual spam/quality patterns, governance vote can adjust.

## Implementation notes

- Anima v1 (mirrorX Wave 10) — initial parameters as listed above
- v2+ — may add per-board rate limits, time-of-day windows, enactment-weighted limits
- Future ratification-tier validators (with stake) bypass these rules — they're a separate role with separate constraints

## Risk acknowledgement

These parameters won't be perfect at v1 launch. The MUTABLE flag means we can adjust quickly through governance vote based on real usage. Don't lock numbers we may need to tune.

## Related elements

- `transparent_mediation` — auto-contribution is a mediated action, must be auditable
- `revocation_right` — user can revoke any auto-verdict within 24h
- `identity_sovereignty` — auto-mode opt-in is user authority, not protocol authority
