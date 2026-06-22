---
title: "Document Types Reference & Selection Guide"
status: accepted
---

## Overview

The detailed per-type reference and the "choosing the right type" selection guide for Archcore's 18 document types. The high-level model (three virtual categories, `slug.type.md` naming, statuses, relations) lives in `concepts/core-concepts`; the multi-document flows in `concepts/document-tracks`; the Sources-vs-Specifications layering in `concepts/requirements-layers`. This document is the type-selection detail that all of those depend on. Category is derived from the type suffix, never from the directory.

## Vision types

### Product track (simple)

| Type | Purpose |
|------|---------|
| `prd` | Product requirements — goals, scope, acceptance criteria |
| `idea` | A concept worth exploring — problem, value, rough approach |
| `plan` | A concrete implementation plan with phased tasks |

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
| `spec` | Canonical normative contract — behavior, constraints, invariants, conformance for a specific technical boundary |
| `doc` | Non-behavioral reference — tables, registries, glossaries, component lists |

## Experience types

| Type | Purpose |
|------|---------|
| `task-type` | A proven workflow for a recurring implementation task — steps, examples, pitfalls |
| `cpat` | A code pattern change — how and why a convention changed (was → became) |

## Choosing the right type

- **rule vs doc** — rule prescribes behavior ("Always do X") with enforcement; doc describes what exists (tables, registries). Descriptive, non-behavioral → doc.
- **adr vs rfc** — adr = decision already final; rfc = proposal open for feedback.
- **guide vs doc** — guide has sequential steps to follow; doc is non-sequential reference to look up.
- **spec vs doc** — spec defines a canonical normative contract for a concrete boundary (behavior, constraints, invariants, conformance); doc describes what exists without normative requirements.
- **spec vs rule** — spec is a technical contract for one component; rule is a cross-cutting team standard. Scoped to a named artifact → spec; applied team-wide → rule.
- **spec vs adr** — spec is the living canonical truth (present-tense: "it works this way"); adr is the decision record (past-tense: "we chose this because"). Both may exist for one component.
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
