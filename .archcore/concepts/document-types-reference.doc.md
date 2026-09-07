---
title: "Document Types Reference & Selection Guide"
status: accepted
tags:
  - "concepts"
  - "document-types"
---

## Overview

The detailed per-type reference and the "choosing the right type" selection guide for Archcore's 21 accepted document types. The high-level model (three virtual categories, `slug.type.md` naming, statuses, relations) lives in `concepts/core-concepts`; the multi-document flows in `concepts/document-tracks`; the Sources-vs-Specifications layering in `concepts/requirements-layers`. This document is the type-selection detail that all of those depend on. Category is derived from the type suffix, never from the directory. The prose profile and the line format each type carries are assigned by `concepts/document-prose-canon`.

The accepted vocabulary includes `research` in vision and `evidence` in knowledge. The CLI release and runtime routing changes remain pending — `concepts/research-and-evidence-types` and `product/research-direction`.

## Vision types

### Product track (simple)

| Type | Purpose |
|------|---------|
| `prd` | Product requirements — goals, scope, acceptance criteria. Covers one unit of product decision at any scale — a whole product or a single feature; size never changes type (a feature-scoped prd is the same sections, compressed; a product-level prd links its feature prds via relations) |
| `idea` | A concept worth exploring — problem, value, rough approach |
| `plan` | A concrete implementation plan with phased tasks |
| `rnd` | Focused investigation that ends in a Recommendation (proceed / refine / defer / stop) and a Next Action — the optional research gate that precedes `idea`/`plan` |
| `research` | Territory investigation closed by coverage of its scope, with dated sources, findings, synthesis, and open gaps |

### Sources track (discovery)

| Type | Purpose |
|------|---------|
| `mrd` | Market analysis — TAM/SAM/SOM, competitive landscape, market needs, timing |
| `brd` | Business justification — objectives, ROI, stakeholders, budget, constraints |
| `urd` | User needs — personas, journeys, usability requirements, acceptance criteria |

Captures **where** requirements come from: MRD (market) → BRD (business) → URD (users).

### ISO 29148 track (decomposition)

| Type | ISO ref | Purpose |
|------|---------|---------|
| `brs` | §9.3 | Business requirements — mission, goals, operational concept, success criteria |
| `strs` | §9.4 | Stakeholder requirements — per-class requirements with ConOps, compliance |
| `syrs` | §9.5 | System requirements — system boundary, interfaces, modes, verification approach |
| `srs` | §9.6 | Software requirements — per-function/per-endpoint specs, verification matrix |

Decomposes through progressively detailed levels: BRS → StRS → SyRS → SRS.

## Knowledge types

| Type | Purpose |
|------|---------|
| `adr` | A technical decision that has been made, with context and alternatives |
| `rfc` | A proposal open for review before a decision is made |
| `rule` | A mandatory standard — imperative statements with good/bad examples |
| `guide` | Step-by-step instructions for completing a task |
| `spec` | Normative behavior contract of something others rely on — one boundary (API, interface, schema, protocol) or one feature/subsystem; captured from existing code or specified ahead of it |
| `doc` | Non-behavioral reference — tables, registries, glossaries, component lists |
| `evidence` | One external material with its locator, access date, extract, and interpretation notes |

### Spec format canon

One form for every spec subject — six sections: **Purpose & Scope** (subject + who depends on it), **Surface** (interface and/or parts, states, field-drivers — referenced, never reproduced), **Normative Behavior**, **Constraints & Invariants**, **Failure Behavior**, **Conformance**. Numbered behavior lines follow EARS clause order with BCP 14 keywords as the modal — `WHEN <trigger>, the <subject> MUST <response>` (also WHILE / IF…THEN / ubiquitous forms); MUST/SHOULD/MAY graded per RFC 2119, uppercase per RFC 8174, MUST kept sparing. Legacy heading pair `Contract Surface` / `Error Handling` reads as `Surface` / `Failure Behavior` — existing specs stay valid; plain `X MUST Y` lines are valid EARS ubiquitous sentences.

## Experience types

| Type | Purpose |
|------|---------|
| `task-type` | A proven workflow for a recurring implementation task — steps, examples, pitfalls |
| `cpat` | A code pattern change — how and why a convention changed (was → became) |

## Choosing the right type

- **rule vs doc** — rule prescribes behavior ("Always do X") with enforcement; doc describes what exists (tables, registries). Descriptive, non-behavioral → doc.
- **adr vs rfc** — adr = decision already final; rfc = proposal open for feedback.
- **guide vs doc** — guide has sequential steps to follow; doc is non-sequential reference to look up.
- **spec vs doc** — spec defines a canonical normative behavior contract for a concrete subject — a boundary or a feature/subsystem others rely on (behavior, constraints, invariants, conformance); doc describes what exists without normative requirements. When others depend on how the subject behaves (observable behavior, external consumers), prefer spec even if doc also fits — the doc links to the spec.
- **spec vs rule** — spec is a technical contract for one component; rule is a cross-cutting team standard. Scoped to a named artifact → spec; applied team-wide → rule.
- **spec vs adr** — spec is the living canonical truth (present-tense: "it works this way"); adr is the decision record (past-tense: "we chose this because"). Both may exist for one component. A spec may be written after code (capture the existing contract) or before it (specify the contract to build).
- **spec vs prd** — the routing gate: if the document answers *what should we build and why* (user stories, priorities, success metrics), it is a prd (or ISO `syrs`/`srs`); if it answers *what behavior can consumers rely on right now*, it is a spec.
- **spec is not** — requirements (use `prd`/`syrs`), task breakdown (use `plan`), rationale (use `adr`), or non-normative reference (use `doc`). It covers only normative behavior others rely on right now.
- **research vs rnd** — coverage of the declared scope closes `research`; a recommendation closes `rnd`. Both belong to vision.
- **research vs doc** — `research` records an investigation with questions, dated sources, coverage, and gaps; `doc` records reference information.
- **evidence vs doc** — `evidence` records one material and its extract; `doc` records reference information that may combine several materials.
- **evidence vs statement** — one material is an `evidence`; one statement within a material is not a separate type.
- **rnd vs idea** — `idea` PROPOSES what to build (concept, value, rough approach); `rnd` INVESTIGATES a question and returns evidence plus a recommendation. Tense test: idea = "we should build X"; rnd = "we investigated X — here is what we found."
- **rnd vs plan** — `plan` is phased execution of an already-decided thing; `rnd` is open investigation that may conclude "do not proceed." `rnd` precedes `plan`.
- **rnd vs adr** — `rnd` is the investigation that PRECEDES and feeds a decision (and may end in defer/stop); `adr` records the commitment made.
- **rnd vs rfc** — `rfc` is a specific proposal already open for review (a position exists); `rnd` is open-ended investigation where a position may not exist yet.
- **task-type vs guide** — task-type is a reusable pattern for a class of tasks; guide is instructions for a specific one-time procedure.
- **cpat vs adr** — cpat focuses on a code pattern change with before/after; adr records a broader architectural decision with alternatives and consequences.
- **mrd vs prd** — MRD analyzes the MARKET without proposing a solution; PRD proposes a PRODUCT with requirements.
- **brd vs prd** — BRD focuses on BUSINESS JUSTIFICATION (ROI, budget); PRD on PRODUCT DEFINITION (features, user stories).
- **urd vs prd** — URD captures user needs via PERSONAS and JOURNEYS; PRD defines requirements with acceptance criteria.
- **mrd vs brd** — MRD is external MARKET ANALYSIS; BRD is internal BUSINESS JUSTIFICATION.
- **brd vs urd** — BRD captures ORGANIZATIONAL needs; URD captures END-USER needs.
- **brs vs brd** — BRS is the ISO SPECIFICATION (formalized); BRD is the INFORMAL SOURCE it formalizes.
- **strs vs urd** — StRS is the ISO SPECIFICATION (per-class, ConOps); URD is the INFORMAL SOURCE it formalizes.
- **brs vs strs** — BRS = WHY (business outcomes, technology-agnostic); StRS = WHAT stakeholders need (operational scenarios, solution-aware).
- **syrs vs srs** — SyRS = WHOLE SYSTEM boundary; SRS = SINGLE COMPONENT's detailed behavior.
- **syrs vs adr** — SyRS defines the whole system boundary with interface contracts and verification; ADR records a single decision.

## Choosing the right requirements track

| Track | Documents | Best for |
|-------|-----------|----------|
| Product (simple) | `prd` | Individual features, small teams, rapid prototyping, internal tools |
| Sources (discovery) | `mrd` → `brd` → `urd` | Discovery, stakeholder alignment, business analysis |
| ISO (decomposition) | `brs` → `strs` → `syrs` → `srs` | Regulated systems, multi-team or complex distributed systems |

All tracks can coexist. Start simple (PRD), add sources when you need stakeholder alignment, add ISO when you need formal traceability.
