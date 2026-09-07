---
title: "Research Direction: Ship the Stored Vocabulary First"
status: accepted
tags:
  - "document-types"
  - "product"
---

## Goal

Ship research support as stored vocabulary: two types (`research`, `evidence`), three relations (`supports`, `contradicts`, `supersedes`), and their conventions, in one CLI release, with the runtime, the shared context, and the docs site following. Then run one real investigation on the new vocabulary and record what it lacked. No stage adds a research method; `architecture/store-not-method-engine` governs the scope.

Hours are human-plus-AI estimates [assumption]. Stages 1–5 sum to 34–50 hours with one CLI release.

## Status

Decided 2026-09-07; this plan replaces the staged rollout of 2026-09-03.

1. `research` is added as a vision type; `rnd` stays as decision-bound investigation. `evidence` is added as a knowledge type for one external material. Vocabulary in `concepts/research-and-evidence-types`.
2. Three relations join the four: `supports`, `contradicts`, `supersedes`. No relation is bound to a category.
3. No frontmatter field is added. Provenance lives in the fixed Locator lines of the `evidence` template. The engine fix that stops `update_document` from erasing keys a human added stays as a defect fix, unrelated to research.
4. In the planned runtime update, the `research` expert path of `/archcore:plan` resolves to the `research` type; `rnd` is invoked by its name. Announced as a breaking change.
5. `superseded_by` annotations in tool responses, second-reader verification, `fetch_evidence`, and every other process item are deferred to `product/research-process-deferred`.
6. The command palette stays at four (`architecture/one-product-two-entry-points`).

The user revised the category decision on 2026-09-07: `research` belongs to vision and `evidence` belongs to knowledge. The accepted vocabulary has 21 types: 12 vision, 7 knowledge, and 2 experience. The shared category references are updated before the engine release; release publication, runtime routing, and docs-site delivery remain pending.

## Tasks

### Stage 1 — engine: types, relations, defect fix (cli, 16–22 h)

Pre-implementation baseline, recorded 2026-09-07: 19 types in `@cli/templates/templates.go`; required sections per type in `@cli/templates/precision.go`; the relation enum in `@cli/internal/sync/manifest.go` holds four values; `update_document` rebuilds frontmatter from three fields in `@cli/internal/mcp/tools/common.go` and drops any other key; a test asserts the drop in `@cli/templates/templates_test.go`.

- [ ] Map `TypeResearch` to vision and `TypeEvidence` to knowledge; templates with the required sections of `concepts/research-and-evidence-types`; entries in `RequiredSections`; ISO profile assignment.
- [ ] Add both types to the `create_document` enum, the `list_documents` type list, and the server instructions (type catalog and selection rules: verdict closes `rnd`, coverage closes `research`; a material is `evidence`, a statement is not).
- [ ] Add `supports`, `contradicts`, `supersedes` to the relation enum, the `add_relation` schema and description, and the manifest validation; keep the enum open to every type pair.
- [ ] Preserve unknown frontmatter keys in `buildDocumentFile` on update; replace the drop assertion with a preservation assertion.
- [ ] Tests for templates, required sections, enums, manifest validation, and preservation; `archcore doctor` accepts the new relation values.
- [ ] CLI changelog entry; release.

Detailed plan: the `cli` repository's `.archcore/document-types/research-and-evidence-vocabulary.plan.md`.

### Stage 2 — runtime: produce the new types (plugin, 4–6 h)

- [ ] `research.frame` produces `research` or `rnd` by the closing test; the state block records which.
- [ ] `research.gather` may create an `evidence` document; the document and its first `supports` or `contradicts` edge are written in the same step.
- [ ] Expert invocation map: `research` resolves to the producing instrument of the `research` type; `rnd` resolves by its name.
- [ ] `/archcore:document` routes the type names `research` and `evidence` to their producing gates, so an existing report can be filed.
- [ ] Minimum engine version gate for the new enums (`architecture/plugin-cli-compatibility`); goldens and routing fixtures; `command-surface-v2.spec` and `track-layer.spec` amended; plugin changelog entry marks the alias change as breaking.

Detailed plan: the `plugin` repository's `.archcore/plugin/research-and-evidence-in-tracks.plan.md`.

### Stage 3 — shared context (global, 4–6 h)

The category decision and vocabulary references move before the engine release. Remaining handoff work follows the release.

- [ ] `concepts/core-concepts` — 21 accepted types and 7 accepted relations; research in vision and evidence in knowledge; 12 vision, 7 knowledge, 2 experience.
- [ ] `concepts/document-types-reference` — rows for `research` and `evidence`; disambiguators `research vs rnd`, `research vs doc`, `evidence vs doc`.
- [ ] `concepts/relation-conventions` — the three relations with axis and direction; research patterns (`rnd depends_on research`, `evidence supports`, `evidence contradicts`, `supersedes`).
- [ ] `concepts/document-prose-canon` — assignment rows for both types.
- [ ] `concepts/evidence-conventions` — new `doc` from the conventions section of the RFC: row first, file second; class as tag; contradiction resolved in prose; raw material outside `.archcore/`.
- [ ] `concepts/glossary`, `concepts/document-tracks`, `concepts/gated-tracks`, `concepts/naming-and-layout`, `architecture/system-map`, `market/moat-parity-and-gaps` — update current vocabulary claims; preserve dated baseline measurements and distinguish pending runtime support.
- [ ] `concepts/rnd-research-document-type` — one line: `research` added by the new RFC; `rnd` scope unchanged.

### Stage 4 — docs site (docs, 4–6 h)

Pages by path under `docs/src/content/docs/`:

- [ ] `concepts/document-types.md` — two sections and the decision tree; the `rnd` block gains the closing test.
- [ ] `concepts/relations.md` — three rows, three axes, direction rules.
- [ ] `reference/precision-checks.md` — required sections of both types.
- [ ] `reference/mcp-tools.md` — enums of `create_document` and `add_relation`.
- [ ] `cli/mcp-server.mdx` — type catalog.
- [ ] `plugin/skills.mdx` and `reference/skills.mdx` — the `research` path resolves to the `research` type; `rnd` by name.
- [ ] `concepts/what-is-archcore.mdx` or `concepts/mental-model.mdx` — one paragraph from `architecture/store-not-method-engine`: tracks fill and check documents; the method stays with the host.
- [ ] Changelog entries: one for the CLI release, one for the plugin release with the alias change marked breaking.

Detailed plan: the `docs` repository's `.archcore/research-and-evidence-docs.plan.md`.

### Stage 5 — one real investigation (global, 6–10 h)

- [ ] Re-file `market/competitive-landscape` as a `research` with Scope, Coverage, Sources, and Open Gaps; promote the sources two documents rely on to `evidence` with `supports` edges.
- [ ] Record in an `rnd` what the vocabulary lacked, item by item, against the trigger column of `product/research-process-deferred`.
- [ ] Stop-point: an item enters the next plan only with an observed trigger.

## Acceptance Criteria

1. Stage 1: `create_document` accepts `research` and `evidence`; `add_relation` accepts the three new values; a document whose frontmatter carried a key outside `title`, `status`, `tags` keeps it after `update_document`.
2. Stage 2: `/archcore:plan research <topic>` produces a `research` draft; `/archcore:plan rnd <topic>` produces an `rnd` draft; `research.gather` writes an `evidence` document and its edge in one step.
3. Stage 3: current vocabulary references state 21 accepted types and seven accepted relations; dated baseline measurements retain their original counts.
4. Stage 4: every docs page listed above names both types and all seven relations; the changelog marks the alias change breaking.
5. Stage 5: `market/competitive-landscape` exists as a `research` with at least one `evidence` document and one `supports` edge; an `rnd` records the gaps.

## Dependencies

- `architecture/store-not-method-engine` — the scope rule: vocabulary first, process on demonstrated need.
- `concepts/research-and-evidence-types` — the vocabulary this plan ships.
- `concepts/rnd-research-document-type` — the type that stays.
- `architecture/engine-runtime-boundary` — stage 1 is engine; stage 2 is runtime.
- `architecture/plugin-cli-compatibility` — stage 2 gates on the stage 1 release.
- `architecture/one-product-two-entry-points` — four-command palette; no fifth command.
- `product/research-process-deferred` — the parking lot stage 5 reads against.
- Stage 3 category and vocabulary references precede the stage 1 release by the user's 2026-09-07 decision. Remaining stage 3 handoff and stage 4 delivery follow that release.
