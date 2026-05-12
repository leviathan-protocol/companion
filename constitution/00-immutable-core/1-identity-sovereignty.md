---
slug: identity_sovereignty
element_type: PRINCIPLE
mutability: IMMUTABLE
inline: true
current_version: 1
contentURI: null
---

The user owns their identity, values, beliefs, and persona. No implementation, protocol, validator, or third party may access unencrypted personal data without explicit consent. Identity authority is rooted in the user's keys (wallet or passkey); revocation is always possible and always honored.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this principle establishes

Personal governance starts with personal sovereignty. The user is the sole authoritative source of their own identity, beliefs, and persona. Any system that mediates between the user and the world — Anima, Companion, the forum, validators — operates with delegated authority, never primary authority.

## Enforcement mechanisms

1. **Keys are user-held** — wallet keys / passkeys never leave user's device. No server-side custody.
2. **Encrypted-at-rest** — any data stored on user's device is encrypted with user-controlled key.
3. **No plaintext server storage** — implementations bound to this Sub-Leviathan must not store user belief data unencrypted anywhere outside the user's device.
4. **Revocation always honored** — user can revoke any delegated authority (auto-contribution, agent mediation, third-party access) at any time; revocation triggers protocol-level cleanup.

## Why immutable

Without identity sovereignty, every other principle collapses. If the protocol can access user beliefs, governance becomes surveillance. This is the foundational guarantee — changing it would mean a different protocol, not an amended Leviathan.

## Reasoning trail

- Echoes Federation Kernel's user-sovereignty principle (`leviathan-protocol/meta/kernel/`).
- Particularly load-bearing for Companion because personal POS data is the most sensitive category of belief.
- Aligned with crypto-native identity practices (self-custody, key-based auth) and privacy-first design (no plaintext server data).

## Related elements

- `data_on_device` — concrete data residency rule
- `transparent_mediation` — any AI mediation must be auditable + revocable
- `revocation_right` — operational implementation of "revocation always honored"
