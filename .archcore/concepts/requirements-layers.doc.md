---
title: "Requirements Layers: Sources vs Specifications"
status: accepted
---

## Overview

Archcore's requirements documents form **two distinct layers**. Keeping them separate — and linking them with consistent relations — is what makes requirements traceable from informal discovery through formal specification. This is ecosystem-level model knowledge; for per-type detail see `concepts/document-types-reference`, for the flows see `concepts/document-tracks`.

## The two layers

- **Layer A — Sources** (`mrd`, `brd`, `urd`, `prd`): capture *where* requirements come from — market, business, and user perspectives. Informal, discovery-oriented.
- **Layer B — Specifications** (`brs`, `strs`, `syrs`, `srs`): formalize requirements into ISO 29148-structured specifications. Formal, normative.

**Sources are not specifications.** Do not write formal ISO structure (mission statements, operational concepts, ConOps, verification matrices) into source documents, and do not copy a specification's content back into a source. The formalization direction is **sources → specifications, never the reverse**. Sources may carry acceptance criteria and success metrics for discovery, but those are not normative specifications.

Conflating the layers bloats sources with structure they weren't designed for, strips specifications of their ISO rigor, makes types ambiguous for agents, and breaks traceability.

## Formalization map

| Specification | Formalizes | Relation |
|---------------|------------|----------|
| BRS | MRD (market needs), BRD (business objectives) | `brs implements mrd`, `brs implements brd` |
| StRS | URD (user needs), BRD (stakeholder needs), BRS (cascade) | `strs implements urd`, `strs implements brd`, `strs implements brs` |
| SyRS | StRS (cascade) | `syrs implements strs` |
| SRS | SyRS (cascade) | `srs implements syrs` |
| PRD | ≈ all four ISO levels | link via `related` (see exception) |

## Relation conventions

1. **Cross-layer (sources → specs):** the **specification** is the `implements` *source*; the **source document** is the *target*. "BRS implements BRD" reads as "the BRS implements what the BRD describes."
2. **ISO cascade (within specs):** each level implements the previous — `strs implements brs`, `syrs implements strs`, `srs implements syrs`.
3. **Partial cascades are valid** — `srs implements brs` is fine when intermediate levels are skipped.
4. **Same layer uses `related`, not `implements`** — `mrd related brd`, `brd related urd`.
5. **Direction rule:** always make the **more specific** document the `implements` source and the **more general** one the target.

## The PRD exception

PRD is intentionally a **pragmatic hybrid** that covers aspects of both layers. It belongs to Layer A (Sources) but can substitute for the full ISO cascade on simpler projects. Link PRD to ISO types with `related` (not `implements`) — it is a peer alternative path, not a formalization source.

## Enforcement note

The CLI operationalizes this model in its MCP server type-selection rules, `add_relation` layer hints, and structurally distinct templates (sources have discovery sections; specs have ISO sections). See `cli/.archcore/document-types/`.
