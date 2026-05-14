---
slug: belief
element_type: TERM
mutability: MUTABLE
inline: true
current_version: 1
contentURI: null
---

A belief is an atomic unit of a user's personal governance — a single value, principle, or rule the user holds. Beliefs are typed (e.g., concept, axiom, directive) and editable; users add, modify, version, and retire their own beliefs over time. A user's full belief set IS their personal constitution.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this term defines

The smallest meaningful unit of personal governance. A belief is more than a journal entry (which is raw, narrative) — it's a structured assertion about how the user thinks/acts/values. Examples:

- A concept: `@autonomy = "the right to define one's own boundaries"`
- An axiom: `#always_revocable = "any delegated authority must be revocable"`
- A directive: `!morning_reflection = "10 minutes journaling before email"`

## Properties of a belief

1. **Typed** — concept (definition), axiom (principle), directive (rule for action)
2. **Versioned** — beliefs evolve; old versions retained for time-travel reflection
3. **Linked** — beliefs reference each other (a directive `!morning_reflection` may reference axioms `#start_intentional`, `#protect_focus`)
4. **Private by default** — beliefs live in `data_on_device` storage; user chooses what (if anything) to expose via persona
5. **Aggregated into persona** — the sanitized persona is derived from the belief set

## Why mutable

Belief typology (the exact set of types: concept/axiom/directive) and linkage rules may evolve as users + the protocol learn what works. Governance vote can refine the schema.

## Related elements

- `persona` — derived sanitized representation
- `data_on_device` — storage residency
- `identity_sovereignty` — beliefs are user-authored, user-owned

## Implementation notes

Anima (mirrorX) implements beliefs as Drift tables (`beliefs`, `belief_versions`, `belief_edges`). The on-device Gemma model interacts with beliefs via the NativeBeliefToolSet (27-tool catalog — see mirrorX/CLAUDE.md Wave 2). Cross-platform sync of beliefs (v3+) uses encrypted P2P per `data_on_device` rule.
