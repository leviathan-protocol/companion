# Companion — Personal Governance Sub-Leviathan

> Layer 2 Sub-Leviathan of the [Leviathan Protocol](https://github.com/leviathan-protocol/meta).
> Governs the **personal governance pattern** — individual sovereign identity, on-device data, AI-mediated belief management.

This repository contains the **constitution** of the Companion Sub-Leviathan. It does not contain implementation code; it defines what implementations must satisfy.

## What Companion is

Companion is the Layer 1 Individual governance pattern in the Leviathan federation. Every person who runs a Companion (in any form — mobile app, desktop, bespoke) is running an instance of this Sub-Leviathan's constitution.

Each user is a sovereign sub-instance: their beliefs are their own, their data stays on their devices, their AI mediation is transparent and revocable. The protocol provides the constitutional substrate; users provide the content.

## The two-constitution model (Witness Mandate)

Every Companion implementation exposes **two parallel constitutions** to the user:

- **User Constitution** — the user's own beliefs (concepts, principles, rules) — their POS
- **The Witness** — the AI's behavioral constitution — how it observes, speaks, responds

Both are editable in the same UI. Both are versioned. Both are visible. The user can read exactly what beliefs and rules shape the AI's responses to them — no hidden system prompts.

The Witness inherits a **Locked Framework** (honesty over flattery, memory ethics, crisis grounding, no silent override, constitution transparency, meta-rule lock) that cannot be edited by user or AI. Users may add, edit, or delete any non-locked rule; the floor is constitutional, the ceiling is sovereign.

See `00-immutable-core/3-witness-mandate.md` for the mandate, `10-protocol-mutable/witness-locked-framework.md` for the locked rules, and `20-mutable-rules/witness-default-seed.md` for the first-run defaults.

## Implementations bound to this Sub-Leviathan

| Implementation | Type | Repository | Status |
|----------------|------|-----------|--------|
| **Anima** | Cross-platform Flutter app (PC + iOS + Android) | [`mirrorX`](https://github.com/leviathan-protocol/mirrorX) (TBD) | v1 in development (target ship 2026-05) |
| **Founder's Companion** | Bespoke (Claude Code + markdown) | Private | Active |

Multiple implementations CAN bind to the same Sub-Leviathan. The constitution defines what they must satisfy; each chooses its own architecture, language, and shipping mechanism.

## Constitution structure

```
constitution/
├── 00-immutable-core/          ← IMMUTABLE: fork-only-changeable foundational guarantees
│   ├── 1-identity-sovereignty.md
│   ├── 2-data-on-device.md
│   └── 3-witness-mandate.md      ← two-constitution structure for AI behavior (2026-05-13)
├── 10-protocol-mutable/         ← LOCKED: high-bar governance vote required to change
│   ├── transparent-mediation.md
│   ├── revocation-right.md
│   └── witness-locked-framework.md  ← 6 locked rules every Witness inherits
├── 20-mutable-rules/            ← MUTABLE: regular governance vote
│   ├── advisory-validator-eligibility.md
│   └── witness-default-seed.md      ← Witness Constitution default v1.0
└── 30-shared-terms/             ← MUTABLE: terminology used across all Companion implementations
    ├── persona.md
    └── belief.md
```

## File format

Each element is Markdown + YAML frontmatter. Constitutional content sits above an `<hr>` separator; editorial context (reasoning, examples, implementation notes) below.

See [`element-format.md` in the public coordination repo](https://github.com/leviathan-protocol/public/blob/main/specs/element-format.md) for the full spec.

## How constitutional changes work

1. **Draft:** Edit `.md` file in this repo (any contributor, via PR)
2. **Discussion:** PR opens forum thread on `leviathan.life/forum/companion`
3. **Vote:** Community vote per mutability level (IMMUTABLE requires fork; LOCKED + MUTABLE via governance)
4. **Validator alignment check:** specialized validator LLMs check against locked principles
5. **Ratification:** if approved + aligned, on-chain `ConstitutionalRegistry.ratifyNewVersion(...)` records the change

The on-chain Registry is canonical. This repo is the **editing surface**.

## Inheritance

Companion inherits from the Federation Kernel in [`leviathan-protocol/meta`](https://github.com/leviathan-protocol/meta). Kernel invariants (4-layer structure, hash anchoring, fork freedom, falsifiability) apply implicitly to every element here.

## User forking (advanced)

Power users may fork this repo (e.g., `alice/companion`) to personalize constitutional elements with their own values. Casual users use the canonical Companion via Anima with default settings.

Fork-binding is an advanced v2+ feature; v1 ships with canonical-only.

## License

CC BY-SA 4.0. Fork freedom is built into the protocol — see `00-immutable-core/`.

## Related

- [`leviathan-protocol/meta`](https://github.com/leviathan-protocol/meta) — Federation Leviathan (parent kernel)
- [`leviathan-protocol/public`](https://github.com/leviathan-protocol/public) — Cross-repo coordination, ADRs, plans
- [`leviathan.life`](https://leviathan.life) — Public website + forum
