---
slug: persona
element_type: TERM
mutability: MUTABLE
inline: true
current_version: 1
contentURI: null
---

A persona is a sanitized, exportable representation of a user's belief system suitable for consent-mediated cross-user interaction. It encodes values, principle priorities, and behavioral preferences as a vector or structured object — not as raw journal content. The persona is derived from user beliefs by an on-device sanitization process; raw journal entries never become part of the persona.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this term defines

The distinction between **journal** (raw private content) and **persona** (sanitized exportable surface) is foundational. Personas can leave the device for matching/discovery (with consent); journals cannot.

## Properties of a persona

1. **Derived, not duplicated** — generated from beliefs by a sanitization process; not a copy of raw data
2. **Vector-shaped (typically)** — embedding vectors enable similarity matching without revealing content
3. **Domain-decomposed** — separate vectors per domain (@autonomy, @honesty, @evidence_standards) for transparent overlap analysis
4. **Versioned** — persona evolves as user's beliefs evolve; old versions retained for time-travel reflection
5. **Consent-gated for sharing** — persona is shared cross-user only when user explicitly opts into a matching flow

## Sanitization invariants

The sanitization process must:
- Strip all proper nouns (names, places, dates) from journal content before embedding
- Aggregate at the principle level, not the event level
- Be deterministic (same beliefs → same persona, given same model version)
- Be on-device (sanitization itself happens before any export)

## Why mutable

Persona schema details (vector dimensionality, domain decomposition, similarity threshold defaults) are technical parameters that evolve. The CONCEPT of persona is stable; the SHAPE is tunable.

## Related elements

- `belief` — atomic unit personas are derived from
- `data_on_device` — journal raw data residency rule
- `identity_sovereignty` — persona sharing is user authority
- `story_match_protocol` (future, v8.2) — uses personas for matching
