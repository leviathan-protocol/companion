---
slug: data_on_device
element_type: PRINCIPLE
mutability: IMMUTABLE
inline: true
current_version: 1
contentURI: null
---

Personal belief data — journal entries, persona vectors, internal reflection — lives on the user's device. Implementations may store encrypted backups in user-controlled cloud or P2P replicas across user's own devices. Implementations must not transmit unencrypted personal data to any server, including those operated by the protocol itself.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this principle establishes

Concrete residency rule for personal data: it stays on the user's hardware. Sync across user's own devices is allowed (and encouraged); cross-user data leaves only via explicit consent flows (e.g., consent-mediated matching).

## Enforcement mechanisms

1. **On-device storage** — beliefs/persona/journal in local SQLite or equivalent
2. **Encrypted backups** — if backup happens, it goes to user's own cloud (iCloud, Google Drive, etc.) under user's key
3. **P2P sync** — cross-device sync uses encrypted P2P (XMTP, libp2p), no central relay sees plaintext
4. **No telemetry of beliefs** — analytics may exist for crash reports, performance metrics, but never for belief content

## Why immutable

Without this guarantee, identity sovereignty is rhetorical. Server-stored beliefs = surveillance capability, even if "well-intentioned." The protocol commits to architectural impossibility of belief access.

## Implementation notes

- Anima v1 (this week): no server storage at all (no sync). Beliefs on-device only.
- Anima v2: manual export/import (.json file) — user controls
- Anima v3+: encrypted P2P sync between user's own devices

## Related elements

- `identity_sovereignty` — parent principle
- `persona` — the sanitized form that CAN leave the device (consent-gated)
- `transparent_mediation` — any AI seeing belief content must be auditable
