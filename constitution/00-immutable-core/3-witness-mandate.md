---
slug: witness_mandate
element_type: PRINCIPLE
mutability: IMMUTABLE
inline: true
current_version: 1
contentURI: null
---

Every Companion implementation MUST expose two parallel constitutions to the user: the **User Constitution** (the user's own beliefs, principles, and rules — their POS) and the **Witness Constitution** (the AI's behavioral constitution — how it observes, speaks, and responds). Both constitutions are editable by the user through the same UI, both versioned, both visible. The Witness Constitution inherits a **Locked Framework** of foundational rules that cannot be edited by user prompt or by the AI itself; these locked rules are defined by `witness_locked_framework` (protocol-mutable) and bind every implementation.

<!-- BELOW THIS LINE: editorial context. Not stored on-chain. -->

---

## What this principle establishes

Personal AI behavior cannot be hidden in implementation code. Just as the user defines their own constitution (POS), the user must also be able to read and edit the constitution that governs the AI in front of them.

This is the [Witness Principle](https://github.com/leviathan-protocol/meta/blob/main/constitution/00-immutable-core/6-witness-principle.md) applied to the user–AI relationship: the AI **witnesses** the user (observes, mirrors, reflects); it does not pass verdicts hidden in system prompts. The user can see exactly what beliefs, principles, and rules shape the AI's responses — and edit them.

## Structural requirements

Every implementation bound to Companion MUST:

1. **Expose two constitutions** — both visible in the user's settings/identity surface:
   - User Constitution (existing POS / belief layer)
   - Witness Constitution (AI's behavioral layer)
2. **Use the same edit UI** — symmetric design: same field types (concepts, principles, rules), same versioning, same export/import flow. The user does not need to learn two separate editors.
3. **Inherit the Locked Framework** — the rules defined in `witness_locked_framework` are inherited verbatim. They appear in the UI as read-only with explicit "Locked — inherited from Companion L2" annotation. They cannot be deleted, edited, or overridden by user-added rules.
4. **Inject both in prompt context** — at every AI call, the prompt builder must include both constitutions (Witness + User), labeled distinctly. The AI must respond under both simultaneously.
5. **Forbid AI self-modification** — the AI MUST NOT have tools or affordances that let it modify the Witness Constitution. Edits are user-only through UI. (Tools like `add_term`, `add_rule` always write to User Constitution scope.)
6. **Default to a good Witness** — first-run users receive a default Witness seed (`witness_default_seed`, mutable) so the AI is honest, warm, and safe without configuration. Configuration is for users who want to tune.

## Why immutable

Without this mandate, AI behavior reverts to opaque system prompts written by implementers. That recreates the very pattern Leviathan exists to abolish: hidden rules that govern users without their consent.

The two-constitution structure + locked framework is the constitutional substrate that makes the user–AI relationship sovereign. Removing it would mean a Companion implementation could secretly steer users while claiming to honor sovereignty — a structural betrayal. Fork to escape this guarantee, not amend it.

## Naming

The working name for the AI's constitutional layer is **The Witness** (mirroring Federation §6 Witness Principle). Implementations MUST use this canonical name in user-facing surfaces. Branding skins (app names like Anima, mirrorX) are independent of the AI layer's name.

Final naming is pending ratification at the L2 forum (`leviathan.life/forum/companion`). If the community ratifies a different canonical name, this element will be updated; the structural mandate is unchanged.

## What implementations are free to choose

The mandate defines structure, not aesthetics. Implementations have freedom in:

- UI presentation (toggle, tabs, split-screen, modal — implementer's choice)
- Default Witness seed v1.0 tonal variation (Anima might emphasize warmth, mirrorX austerity — both must honor the locked framework and structural mandate)
- Persona-override modeling (global Witness + persona overrides is recommended pattern; not required at L2 level)
- Onboarding flow (opinionated default vs. guided customization — implementer's choice)
- Storage backend (Drift, SQLite, IndexedDB — any compliant store)

## Enforcement & verification

1. **Schema-level** — implementations MUST persist Witness Constitution rows distinct from User Constitution (e.g., scope column = `'witness'` vs `'user'`). Mixing storage scopes is a constitutional violation.
2. **UI-level** — the Witness Constitution edit surface MUST be reachable from the same settings entry as User Constitution edit. Hiding it = violation.
3. **Prompt-level** — verifiable via prompt logs. The AI's effective system prompt MUST be reconstructible from (Locked Framework + Witness Constitution + User Constitution + user message). No silent additions.
4. **Validator check** — Companion-aligned validator LLMs may audit implementations for compliance; failure flags via `transparent_mediation` audit logs.

## Reasoning trail

- Direct application of Federation Kernel `witness-principle` (§6, IMMUTABLE) — the protocol witnesses, it does not accuse. At the individual scale, the AI witnesses, it does not flatter.
- Closes the loop on `transparent_mediation` (LOCKED): mediation is auditable, AND the constitution that governs mediation is also visible and editable.
- Aligned with Anthropic's Constitutional AI inverted: each user writes their AI's constitution rather than the AI company writing one centrally. Personal Constitutional AI = federated, fork-able.
- Solves the sycophancy lock-in: the Locked Framework prevents users from accidentally configuring an AI that only flatters them. Honesty is structurally protected.
- Establishes Companion L2 as the abstraction layer; mirrorX and Anima are L3 implementations bound by this mandate.

## Related elements

- `witness_locked_framework` (protocol-mutable) — the specific locked rules every Witness Constitution inherits
- `witness_default_seed` (mutable) — first-run Witness v1.0 body
- `identity_sovereignty` (immutable) — user owns identity; here we extend: user also owns AI behavior visibility
- `transparent_mediation` (locked) — audit log requirement complements constitution visibility
- Federation `witness-principle` (kernel immutable) — parent principle

## Implementation reference (informative, not binding)

```
schema:
  beliefs:
    scope: enum('user', 'witness')  ← required column
    # all existing belief fields unchanged

prompt_builder:
  === LOCKED FRAMEWORK ===
  { inherited from witness_locked_framework, immutable }

  === WITNESS (how I behave) ===
  { scope='witness' beliefs }

  === USER (who you are) ===
  { scope='user' beliefs }

  === USER MESSAGE ===
  { current prompt }

ui:
  settings/identity:
    [ My Constitution ] [ The Witness ]   ← toggle
    (same edit components, scoped to selection)
```

This pattern is non-binding architectural guidance. Implementations may choose different storage, prompt structure, or UI as long as the structural mandate is satisfied.
