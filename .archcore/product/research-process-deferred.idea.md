---
title: "Research Process Items Deferred Until Stored Investigations Exist"
status: draft
tags:
  - "document-types"
  - "product"
---

## Idea

Record every process item from the September 2026 research design that `architecture/store-not-method-engine` deferred, so that none is lost and none re-enters by accident. Each item enters only when a real investigation stored with `concepts/research-and-evidence-types` shows the gap it would close. This document is the parking lot, not a roadmap.

The origin of the design is the working note `archcore-research-architecture-overview.md` at the repository root (untracked at the time of writing) [assumption].

## Value

The items below were designed against an imagined investigation, not a stored one. Keeping them out of the vocabulary release keeps the release small (two types, three relations) and keeps the runtime a filler of documents, not a research method. Keeping them written keeps the reasoning available when a stored investigation asks for one of them.

## Possible Implementation

Each item names its trigger — the observation in a stored `research` or `rnd` that would justify it.

| Item | What it would add | Enters when |
|---|---|---|
| Five-stage protocol (`frame`, `gather`, `challenge`, `synthesize`, `close`) | a `challenge` gate between gather and conclude with a Counter-evidence exit check | stored investigations show recommendations with no recorded counter-evidence |
| Coverage units | the Coverage section keyed by questions, topics, hypotheses, checklist items, or entities, with a declared stop condition | investigations of different kinds fail to express what "covered" means in one table |
| Depth profile (`quick` / `deep`) | declared minimums: sources per unit, independent sources, source classes | investigations that look complete rest on one source per finding |
| Researcher agent | a read-only agent per coverage unit on hosts with subagents | gather in the main thread proves too slow or too shallow |
| Adversarial reader | a read-only agent that seeks what contradicts each load-bearing finding | `contradicts` edges stay rare while findings later prove wrong |
| Second-reader verification | `evidence` stays `draft` until a second pass confirms the extract | fabricated or misquoted sources appear in accepted evidence |
| `fetch_evidence(url)` engine primitive | host-independent fetch with snapshot, hash, and access date | second-reader verification is not enough, or hosts without web tools block real users |
| Import of an external report through `/archcore:document` | a path that files a ready report as `research` with `draft` evidence | users paste external reports into `doc` instead of `research` |
| Re-entry verbs (`refresh`, `extend`, `challenge`) | named ways to re-enter a closed `research` | users re-run research from scratch instead of revising |
| Freshness threshold | a per-document review horizon and a check against it | stale sources are found under accepted decisions |
| `review research` | structural checks: findings without evidence, unresolved `contradicts`, `research` without Synthesis | the auditor's existing orphan and consistency checks miss research-specific failures |
| Non-intrusion rules | lookup vs. research distinction; `world` needs offered once and declined into `[assumption]` | the research instrument engages on requests that only wanted to build |
| De-escalation `world` → `machine` | an accepted `rnd` or `research` satisfies a `world` need at Derivation | the conductor re-researches a territory the repository already holds |
| Spawn, not convert | an `rnd` that outgrows its question spawns a `research`; a `research` that yields a decision spawns an `rnd` | users ask to retype documents and lose relations doing it by hand |
| Relation at creation | an `evidence` document and its first edge are written together, not at gate close | interrupted sessions leave `evidence` documents without edges |
| Cost caps | a maximum of sources per unit and a timebox per session | a deep investigation consumes more than the user intended |
| `claim` type | a statement promoted to its own document when a document outside the investigation depends on it | decisions cite findings that later move or vanish inside a revised `research` |
| `superseded_by` in tool responses | the engine annotates a document with its incoming `supersedes` edge | readers act on superseded documents because relations are not listed |

## Risks

- The list reads as a roadmap and pulls work forward. The trigger column is the guard: an item without an observed trigger stays here.
- Some items have no cheap test of their trigger; "findings later prove wrong" needs a reviewer to notice. Accepted: a parking lot records reasoning, it does not enforce order.
- The origin note may be deleted or moved; the reasoning it holds is summarized in the rows above, so the loss is bounded.
