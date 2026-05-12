# Companion — Personal Governance Sub-Leviathan

> Layer 2 Sub-Leviathan of the [Leviathan Protocol](https://github.com/leviathan-protocol/meta).
> Governs the **personal governance pattern** — individual sovereign identity, on-device data, AI-mediated belief management.

This repository contains the **constitution** of the Companion Sub-Leviathan. It does not contain implementation code; it defines what implementations must satisfy.

## What Companion is

Companion is the Layer 1 Individual governance pattern in the Leviathan federation. Every person who runs a Companion (in any form — mobile app, desktop, bespoke) is running an instance of this Sub-Leviathan's constitution.

Each user is a sovereign sub-instance: their beliefs are their own, their data stays on their devices, their AI mediation is transparent and revocable. The protocol provides the constitutional substrate; users provide the content.

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
│   └── 2-data-on-device.md
├── 10-protocol-mutable/         ← LOCKED: high-bar governance vote required to change
│   ├── transparent-mediation.md
│   └── revocation-right.md
├── 20-mutable-rules/            ← MUTABLE: regular governance vote
│   └── advisory-validator-eligibility.md
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
