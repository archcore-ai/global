---
title: "Add research and evidence: Two Types and Three Relations for Stored Investigations"
status: accepted
tags:
  - "concepts"
  - "document-types"
  - "vocabulary"
---

## Summary

Add `research` in vision, `evidence` in knowledge, and three relation types, `supports`, `contradicts`, and `supersedes`. `research` records an open investigation of a territory that closes on coverage, not on a verdict; `evidence` records one external material — a report, a page, a dataset, an interview — with its locator, its access date, and the extract a document relies on. `rnd` stays the investigation that ends in a recommendation. The change is vocabulary only: types, templates, relation names, and conventions; how an investigation is conducted stays with the host and the user (`architecture/store-not-method-engine`).

## Motivation

Two gaps in the stored vocabulary surface as soon as a repository holds a real investigation.

- A market landscape, a state-of-the-art review, or a competitor watch has no verdict to end on. `rnd` requires one of four recommendations and marks a document without it incomplete (`concepts/rnd-research-document-type`). Today such work lands as `doc` — `market/competitive-landscape` in this repository is one — and loses its questions, its coverage, and its gaps.
- A source that two documents rely on, a source that another source contradicts, or a source that a newer one replaces has no node in the graph. The four relation types name structure (`implements`, `extends`, `depends_on`, `related`) and cannot say "this material supports that finding" or "this newer report replaces that one" (`concepts/relation-conventions`).

Both gaps are storage gaps. Neither needs the tool to run an investigation, and this RFC adds no process.

## Detailed Design

### Two types

| | `rnd` | `research` |
|---|---|---|
| What closes it | one recommendation of four | coverage of the declared scope |
| Bound to | one question or one decision | a territory with no single decision behind it |
| Re-entry | rare, on an explicit request | expected: the document is revised as the territory changes |
| Required sections | Goal, Questions, Approach, Findings, Recommendation, Next Action | Goal, Scope, Coverage, Sources, Findings, Synthesis, Open Gaps |
| `accepted` means | concluded; recommendation is proceed or refine | the synthesis is current as of its last revision |
| `rejected` means | concluded; recommendation is defer or stop | abandoned, or fully replaced through `supersedes` |
| Tense test | "we investigated X to decide Y" | "we are mapping X" |

`rnd` keeps its category (vision) and its scope. Its RFC's line "typically technical" stays true: the investigation under a decision is what `rnd` serves.

`evidence` records one material. Required sections: Locator, Extract, Notes. The Locator section holds fixed first lines — address, access date, publication date when known, publisher when known. Frontmatter stays `title`, `status`, `tags`; no field is added (`concepts/core-concepts`). The class of the material travels as a tag: `source:primary`, `source:secondary`, `source:measurement`, `source:interview`, `source:dataset`.

Statuses of `evidence` reuse the three existing values: `draft` — recorded by whoever found it; `accepted` — a second reader confirmed that the material exists and that the extract is in it; `rejected` — retracted or found unreliable.

### Category

`research` belongs to **vision** as territory discovery, alongside `rnd` and `mrd`. `evidence` belongs to **knowledge** as a reusable record of one material. `rnd` remains in vision. The accepted vocabulary has 21 types: 12 vision, 7 knowledge, and 2 experience.

The category decision was revised on 2026-09-07 before the CLI release. This revision replaces the earlier assignment of both new types to knowledge. CLI v0.8.3 (2026-09-07) ships both types and the three relations; plugin v0.8.3 (2026-09-07) ships the runtime routes.

### Three relations

| Relation | Axis | Direction | Examples |
|---|---|---|---|
| `supports` | evidential | from the material to the statement it backs | `evidence supports research`; `evidence supports rnd`; `rnd supports research` when the rnd carries a measurement |
| `contradicts` | evidential | from the challenger to the statement it disputes | `evidence contradicts research`; `adr contradicts adr` when two accepted decisions conflict |
| `supersedes` | temporal | from the newer document to the older one it replaces | `evidence supersedes evidence`; `adr supersedes adr` |

The relation vocabulary stays one language for every type. No relation is bound to a category; which pair takes which edge is a convention (`concepts/relation-conventions`), not an engine constraint. Relation count becomes 7. `contradicts` is read in both directions by a reviewer; the stored direction records who challenged whom.

Research is never `implements` and never `extends`. `rnd depends_on research` is the canonical link from a decision-bound investigation to the territory it draws on.

### Conventions

- **A source is a row first and a file second.** A source is recorded as a row in the Sources section of the `research` or `rnd` that uses it. It gets its own `evidence` file only when two documents rely on it, when a `contradicts` edge involves it, or when a newer material supersedes it. Most sources stay rows.
- **A contradiction is resolved in prose.** A `contradicts` edge stays until the body of the disputed document carries one line that names both materials and states the resolution. A reader treats an edge without such a line as unresolved.
- **Raw material lives outside `.archcore/`.** An `evidence` document carries the address and the extract, never the file. A snapshot, when kept, lives outside the repository or in an ignored directory.
- **Method is recorded, not prescribed.** The Approach section of an `rnd` and the Scope section of a `research` name how and where the material was gathered. No template names a tool, a search, or an agent.
- **A statement becomes a document only on demand.** A finding inside a `research` or an `rnd` gets its own document only when a document outside the investigation depends on it. That threshold is recorded here so a later `claim` type has a starting rule; no `claim` type ships with this RFC.

### Command surface

`/archcore:plan` exposes one research path, `research`. It names the research instrument, not a type: the instrument selects `rnd` when the request names a pending decision or a set of candidates to choose between, and `research` for any other investigation. `/archcore:document research` files a ready report by the same test — a report that ends in a recommendation is an `rnd`. `/archcore:document evidence` files one external material. Neither `rnd` nor `evidence` is an entry on `/archcore:plan`, and no command treats a bare registry type name as an entry; the argument hint of a command is its complete expert surface (`plugin/.archcore/plugin/command-surface-v2.spec`, `plugin/.archcore/plugin/research-runtime-category-and-evidence-entry.adr`).

Revised on 2026-09-07 from the first cut, which resolved the `research` path to the `research` type and reached `rnd` by its own name through a type-name catch-all. That cut shipped as plugin v0.8.2 and was rejected the same day: it made the user choose the closing test before the investigation existed, and the catch-all exposed entries the argument hint did not show. Plugin v0.8.3 removes `plan rnd` and `plan evidence` and marks the removal as breaking in its release notes. The `research` path keeps its name, so users of v0.8.1 and earlier see no surface change; what changes is the document the path can produce.

### Known limitations, accepted on 2026-09-07

- Authenticity of an `evidence` document is the word of whoever set `accepted`. The engine does not fetch, hash, or snapshot a source. A second reader is a convention, not a check.
- A reader who opens a superseded document sees the replacement only by listing its relations. The engine adds no `superseded_by` annotation to tool responses in this change.
- Coverage and freshness are body content. No tool filters by date. No frontmatter field is added for provenance: no reader exists for one, and the fixed Locator lines carry the same content.

### Out of this RFC

- Any process: gates beyond filling the templates, depth profiles, verification passes, freshness thresholds, intrusion rules. These are listed in `product/research-process-deferred` and enter only after real investigations show the need.
- A `claim` type, per the threshold above.

## Drawbacks

- Two more types against "simplicity by constraint". Mitigated by the closing test: a verdict closes an `rnd`, coverage closes a `research`; a material is an `evidence`, a statement is not.
- `research` and `doc` can overlap in subject despite their different categories. A `research` records an investigation with scope, dated sources, coverage, and gaps; a `doc` records reference information. The line stays soft for rosters of external things [assumption].
- Three more relation names to learn. Mitigated by the three axes: structural, evidential, temporal.
- The `research` path of `/archcore:plan` can now produce an `rnd`; a user who wants an `rnd` for a request with no named decision must phrase the decision or the candidates, since `plan` has no type override.

## Alternatives

- **Widen `rnd` to cover open investigations.** Rejected: it removes the mandatory recommendation that makes `rnd` useful under a decision, and "refine forever" is not a verdict.
- **A `source` type instead of `evidence`.** Rejected: `sources` already names the acquisition path of `/archcore:plan` and the Sources document track; the collision is public. `source` remains possible if that path is ever renamed.
- **`fact`, `finding`, `result`.** Rejected: each names a statement, not a material. One material yields many statements; a file per statement is the file explosion the row-first convention exists to prevent.
- **`informs` and `derived_from` relations.** Rejected: `depends_on` in the decision-to-research direction already says "informs"; `extends` already says "derived from".
- **Provenance in frontmatter fields.** Rejected for now; see the limitations above.

## Adoption

1. Accept this RFC (vocabulary decision) — done 2026-09-07.
2. Engine: templates, required sections, relation enum, server instructions, tests — the `cli` repository's plan.
3. Runtime: the research track produces `research` or `rnd` by the closing test; the gather gate may create `evidence` with an edge; the `research` path of `/archcore:plan` names the instrument; `/archcore:document` accepts `research` and `evidence` — shipped in plugin v0.8.3 (2026-09-07).
4. Shared context: record the revised category decision before the engine release, as requested on 2026-09-07 — done. Complete the remaining handoff after the release: `concepts/core-concepts`, `concepts/document-types-reference`, `concepts/relation-conventions`, `concepts/document-prose-canon`, `concepts/glossary`, and every count of types and relations updated; `concepts/evidence-conventions` added from the conventions above.
5. Docs site: types page, relations page, plan command pages, precision checks, MCP tools reference, changelog — per `product/research-direction`.
