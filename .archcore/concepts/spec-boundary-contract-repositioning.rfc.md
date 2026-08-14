---
title: "Reposition spec as a Bidirectional Boundary Contract"
status: accepted
tags:
  - "concepts"
  - "document-types"
---

## Summary

Reposition the existing `spec` type from a downstream, after-the-fact "formalization" artifact to a **bidirectional contract of a depended-on boundary** — written either *after* code (capture the contract of what exists) or *before* it (specify the contract to build). This changes spec's framing and its creation triggers, not its scope: it stays the normative contract of one concrete technical boundary (behavior, constraints, invariants, conformance).

Goal: `spec` should trigger **somewhat** more often — closing a real under-creation gap against `rule`/`adr`/`doc` — without becoming a catch-all. This is a shared-vocabulary change, so the decision lives at the `global` level; per-tool prompt and threshold edits land in cli and plugin once accepted.

## Motivation

`spec` is created far less than `rule`, `adr`, and `doc` across projects. A prompt-level audit of cli and plugin shows this is structural, not incidental — spec sits in the least-triggered quadrant on three axes at once:

1. **No natural trigger event.** Its WHEN-TO-CREATE is an abstraction ("the canonical normative contract … is being formalized"), whereas `adr` fires on "a decision is made", `rule` on "a standard is established", `doc` on "reference material". Those are everyday moments; "formalizing a contract" is a rare, deliberate act with no organic hook in a coding session.
2. **Every disambiguator routes away from spec.** `spec vs doc/rule/adr` each set a high bar for spec and a low-friction fallback to the other type. There is no tie-breaker that routes an ambiguous case *toward* spec.
3. **Highest-effort template.** Spec is the most demanding artifact (normative behavior, invariants, conformance), so under uncertainty agents pick the cheaper `doc`/`adr`.

In the plugin this compounded, on the command surface current when this RFC was written: `capture` and `decide` hard-defaulted to `adr`, spec fired only on a narrow "component contract" signal, and there was no `_shared/spec-contract.md` reinforcement (whereas `adr` had `_shared/adr-contract.md`). That surface was later replaced — see *Per-tool implementation* below.

**Competitive context.** The spec-driven-development movement — GitHub Spec Kit, AWS Kiro, Tessl, BMAD — makes "spec" the *primary, upstream* artifact ("the spec is the artifact, code is a side effect" — Tessl). Specs trigger constantly there because the spec is the entry point of the workflow and carries a vivid value-narrative (stops drift and API hallucination; reported 3–10× first-pass agent success). Archcore's spec is the inverse: an optional terminal formalization with no stated why-now.

**Identity boundary.** Archcore is a context layer, not an SDD codegen pipeline. We adopt SDD's *value-narrative* and its *bidirectional* framing — not its spec-generates-code model, which would duplicate `prd` (requirements) and `plan` (tasks) and shift archcore's identity.

## Detailed Design

### Repositioned definition

`spec` is the **durable contract of a boundary other code or teams build against** — an API, interface, schema, protocol, or component with externally-observable behavior. It exists so that any agent or engineer touching that boundary reads one authoritative description of how it must behave, instead of re-deriving it from drifting code or from an `adr` (which says only *why*).

### Trigger reframe (the core change)

- From: *"The canonical normative contract for a concrete system, component, interface, schema, or protocol is being formalized → spec"*
- To: *"A component, interface, schema, or protocol has externally-observable behavior that other code or teams depend on → spec — capture the contract of what exists, or specify the contract to build."*

Bidirectional: a spec may be written **after** code (descriptive capture) or **before** it (prescriptive). The trigger is the **existence of a depended-on boundary**, not a "formalization" moment.

### Disambiguation: add a tie-breaker toward spec

Keep the existing `spec vs doc / rule / adr` boundaries, and add one positive rule:

> When the subject is a boundary other code depends on (API, interface, schema, protocol), prefer `spec` even if `doc` or `adr` also seems to fit — the `doc`/`adr` links to the spec.

`doc` still owns non-behavioral reference; `adr` still owns the rationale; `rule` still owns team-wide practice.

### Guardrails — what spec is NOT (keeps "more, not much more")

- requirements / what is needed → `prd` / `syrs`
- task breakdown / execution → `plan`
- rationale / why we chose → `adr`
- non-normative reference (tables, registries, glossaries) → `doc`
- team-wide human practice → `rule`
- every file → no; only boundaries with **external consumers**

Spec stays **one subject per document**. The widening is strictly the trigger ("a depended-on boundary exists"); the five neighbouring types remain barriers against over-creation.

## Drawbacks

- Widening any trigger risks over-creation. Mitigated by the explicit NOT-list, the "depended-on boundary" gate, and measuring creation rates on `bench/` before and after.
- Borrowing "stop drift / hallucination" language risks implying archcore generates code from specs. The framing must stay descriptive/contractual, never generative.

## Alternatives

- **(A) Descriptive-only + value-narrative (minimal).** Keep the after-the-fact framing; only de-jargon it and attach a why-now. *Rejected:* leaves the core "no trigger until someone decides to formalize" gap; smallest movement.
- **(C) Full SDD spec-first generative.** Spec drives code generation, Kiro/Spec-Kit style. *Rejected:* duplicates `prd` (requirements) and `plan` (tasks) and shifts archcore from context layer to SDD pipeline.
- **(B) Bidirectional boundary contract — chosen.** Widens the trigger to "a depended-on boundary exists" while preserving the `prd`/`plan`/`adr`/`doc` boundaries.

## Canonical vocabulary changes on acceptance

`concepts/document-types-reference.doc.md`:
- Knowledge-types `spec` row → reframe to boundary contract + bidirectional: "Contract of a depended-on boundary — behavior, constraints, invariants, conformance; captured from existing code or specified ahead of it."
- "Choosing the right type" → augment `spec vs doc` and `spec vs adr` with the tie-breaker toward spec for depended-on boundaries; add one NOT-list line (spec is not requirements/tasks/reference).
- No new type, no category change, no type-count change (stays within the existing knowledge types).

`concepts/core-concepts.doc.md`:
- If it carries a one-line spec gloss, align it with the boundary-contract framing.

Both changes are current — landed in `concepts/document-types-reference` and `concepts/core-concepts`.

## Per-tool implementation (lives with each tool, on acceptance)

**cli**
- `internal/mcp/server.go` — rewrite the WHEN-TO-CREATE spec line (event-based + bidirectional); add the TYPE-SELECTION tie-breaker toward spec; optionally add the NOT-list.
- `internal/mcp/tools/create_document.go` — align the spec catalog one-liner.
- Templates unchanged — the spec template is already boundary-structured (Purpose/Scope/Contract Surface/Normative Behavior/Conformance). That legacy heading pair now reads as `Surface` / `Failure Behavior` under the spec format canon in `concepts/document-types-reference`.

**plugin**
- The `capture` and `decide` skills this RFC originally targeted are deprecated. The plugin surface collapsed to four commands — `init`, `plan`, `document`, `review` — with gated tracks beneath them (`concepts/gated-tracks`). Both verbs were absorbed into `document`.
- `skills/_shared/tracks/describe.md` — widen the spec routing signal beyond "component contract or interface"; for a depended-on boundary, default to `spec` rather than `doc`.
- `skills/_shared/tracks/decision.md` — offer `spec` whenever a decision establishes or changes a boundary contract, not only on the explicit "and formalize the contract" phrase.
- `skills/_shared/spec-contract.md` — current: the file ships, at parity with `adr-contract.md`.

## Adoption

1. Accept this RFC (vocabulary decision).
2. Update the canonical docs (`document-types-reference`, `core-concepts`).
3. Tools implement the prompt/threshold edits (cli, plugin).
4. Measure on `bench/` — confirm spec creation rises modestly (not ~2×) without cannibalizing `doc`/`adr`.

## Prior art

GitHub Spec Kit (Specify → Plan → Tasks), AWS Kiro (`requirements.md` / `design.md` / `tasks.md`, spec-first generative), Tessl (spec-as-primary-artifact, bidirectional spec↔code, spec registry), BMAD (documentation-first PRD + architecture). Archcore borrows their bidirectional framing and value-narrative while keeping spec descriptive/contractual rather than code-generating.
