---
title: "Add rnd: a Research document type"
status: draft
---

## Summary

Add `rnd` as a 19th canonical document type in the `vision` category: a single, universal type for focused investigation that ends in a recommendation and a concrete next action. It fills the gap between early exploration (`idea`) and execution (`plan`). One type, one template — no variants.

This is a change to the shared vocabulary, so the proposal lives at the `global` level. Implementation-grade detail (templates, validation, tests) lives with each tool (cli, plugin) once this is accepted.

## Motivation

The vocabulary has `idea` and `plan`, plus the discovery (sources) and specification (ISO) tracks, but no home for recommendation-oriented research. Teams routinely investigate a question *before* committing — "Can we use library X? What's the perf cost? Is approach A or B better?" — and that work has nowhere to live:

- forced into `idea`, which is meant to *propose*, not *investigate*;
- mixed into `plan`, which is meant to *execute* a decided thing;
- buried in an `adr`'s "Alternatives Considered";
- or left outside `.archcore/` in chat threads.

The investigation — the most reusable part, including the dead ends — is the thing most often lost. `rnd` gives it a durable, queryable home and forces a verdict instead of leaving scattered findings.

## Detailed Design

### The type

- **Name:** `rnd` · **Category:** `vision` (decision-support that gates `idea`/`plan`).
- A single universal type. No `variant` field, no sub-types.

### Template

```
Research Goal
Context & Trigger
Questions / Hypotheses
Approach (inputs, options, experiments)
Findings
Implications
Recommendation (proceed / refine / defer / stop)
Next Action
Risks & Unknowns
Related Materials
```

Every `rnd` MUST end with a Recommendation (one of proceed / refine / defer / stop) and a Next Action. A research document without a verdict is incomplete.

### Status lifecycle (reuses the existing 3 statuses)

No new status values are needed:

| Status | Meaning for `rnd` |
| --- | --- |
| `draft` | investigation in progress |
| `accepted` | concluded; recommendation is proceed or refine |
| `rejected` | concluded; recommendation is defer or stop (investigated, decided not to pursue) |

The "we looked into it and decided not to" outcome is first-class without new infrastructure.

### Disambiguation

- **rnd vs idea** — `idea` PROPOSES what to build (concept, value, rough approach). `rnd` INVESTIGATES a question and returns evidence plus a recommendation. Tense test: idea = "we should build X"; rnd = "we investigated X — here is what we found."
- **rnd vs plan** — `plan` is phased execution of an already-decided thing. `rnd` is open investigation that may conclude "do not proceed." `rnd` precedes `plan`.
- **rnd vs adr** — `rnd` is the investigation that PRECEDES and feeds a decision; `adr` records the commitment made. An `rnd` can end in defer/stop; an `adr` commits.
- **rnd vs rfc** — `rfc` is a specific proposal already open for review (a position exists). `rnd` is open-ended investigation where a position may not exist yet.
- **rnd vs sources track (mrd/brd/urd)** — the sources track is multi-document product/market/user discovery. `rnd` is a single, lightweight, recommendation-oriented investigation — typically technical.

### Relations (existing 4 types)

- `idea related rnd` — research associated with a concept.
- `plan depends_on rnd` — a plan whose path depends on research findings.
- `adr depends_on rnd` — a decision informed by an investigation.

Do NOT use `implements` for research — it formalizes a contract/spec, which is not the relationship a plan or decision has to an investigation.

### Placement in tracks

`rnd` is a single document, not a track. It slots into the **Product** track as an optional gate:

```
(rnd) → idea → prd → plan
```

Research before an idea (is this worth exploring?), after an idea (is it feasible?), or before a plan (which approach?). Tracks are guidance, not gates — `rnd` is used only when a question must be resolved first.

### Canonical vocabulary changes on acceptance

`concepts/core-concepts.doc.md`:
- "Document types (18)" → (19); "18 types" → "19 types" in *Simplicity by constraint*.
- Vision category row and the Vision type listing add `rnd` (research).

`concepts/document-tracks.doc.md`:
- Product track notes the optional `(rnd)` research gate.

### Per-tool implementation (lives with each tool)

- cli: add `TypeRnD` mapped to `CategoryVision`, a `generateRnDTemplate`, inclusion in `ValidTypes` / the `create_document` enum, MCP instruction + `list_documents` updates, and tests.
- plugin: surface `rnd` in the matching intent/track skill (no new per-type skill).

## Drawbacks

- **Type proliferation** — a 19th type works against "simplicity by constraint." Mitigated by sharp, tense-based disambiguation (especially rnd vs idea) and by keeping it one template with no variants.
- **rnd vs idea confusion** — habit may pull users to `idea`. Mitigated by the propose-vs-investigate tense test and the mandatory Recommendation / Next Action sections that `idea` lacks.

## Alternatives

- **A `variant: product | technical` field with two templates** (an earlier cli draft). Rejected: it would add a sub-type mechanism no existing type has — extra surface across create/read/update/validate/sync — and the two templates overlapped ~80%. A "product research" variant also duplicates the sources track (`mrd → brd → urd`), which already owns product/market discovery. Technical, code-facing investigation is the unserved gap; `rnd` targets that.
- **Keep using `idea`/`plan`/`adr`.** Rejected: this is the status quo that loses investigations and conflates propose / investigate / execute.
- **Do nothing / keep it in chat.** Rejected: research findings (especially rejections) are durable knowledge worth preserving in-repo.

## Adoption

1. Accept this RFC (vocabulary decision).
2. Tools implement `rnd` (cli templates/validation/tests; plugin skill surfacing).
3. Update the canonical docs (`core-concepts`, `document-tracks`) to reflect 19 types.
4. The earlier cli-local `idea` proposal is superseded by this RFC and removed.
