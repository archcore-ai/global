---
title: "Archcore Stores Knowledge and Does Not Execute a Method"
status: accepted
tags:
  - "architecture"
  - "concepts"
  - "product"
---

## Context

Archcore's identity is stated in fragments. The narrative rule forbids defining it as a methodology kit or as a workflow (`product/canonical-narrative` rules 5 and 24); the jobs document separates it from spec pipelines (`product/jobs-to-be-done`); the spec RFC calls it a context layer, not a codegen pipeline (`concepts/spec-boundary-contract-repositioning`); the surface descriptors say that methodology tools define a process while Archcore keeps the resulting knowledge alive (`product/surface-descriptors`). None of these states the positive rule: what Archcore does with a piece of work, and what it leaves to the host.

The question became concrete while scoping research support in September 2026. The first design grew a five-stage protocol, depth profiles, a verifier agent, intrusion rules, and a fetch primitive — a research method — before any of it had a stored artifact to serve. A measurement of the product as shipped showed where its weight lies:

- 19 document types; 16 store a state, 3 (`plan`, `guide`, `task-type`) store a procedure; 0 are executed by the tool — `@cli/templates/templates.go`.
- Engine code: about 8,600 lines serve storage and retrieval (MCP tools, templates, documents, relations, configuration); about 3,500 lines serve advisory behavior (hooks, agents, wiring); the rest is command plumbing — counted over `@cli/internal/` and `@cli/templates/` on 2026-09-07.
- Runtime: 8 tracks, 34 gates, about 3,800 lines of prompt text; every gate is a contract of what a document must contain to pass, and none is a method for producing it — `@plugin/plugins/archcore/skills/_shared/tracks/`.

Every type Archcore ships was added the same way: a template, required sections, a place in the categories and in the relation conventions. No type came with a method for producing its content. An `adr` has no decision procedure, a `spec` has no design procedure, an `mrd` has no market-research procedure. The gated tracks fill documents and check their shape (`concepts/gated-tracks`); they do not run the discipline behind them.

## Decision

Archcore stores knowledge in typed documents and relations. It does not execute the method that produces that knowledge.

- A new capability enters Archcore as vocabulary first: document types, templates, required sections, relation types, and conventions. This is the part every host receives (`architecture/engine-runtime-boundary`).
- The runtime may add gates that fill and check the documents of a capability. A gate states what a document must contain; it does not state how to obtain it.
- The method — how to decide, how to investigate, how to gather sources, which tools to use — stays with the host and the user. A template records the method that was used; it never prescribes one.
- Process for a capability is added only after stored artifacts of that capability exist in real repositories and show what the process must protect.

## Alternatives Considered

- **Archcore as a method engine for selected disciplines** (research first, others later). Rejected: the engine would tie a discipline to one host's tools, break portability across the eight hosts, and grow a second product inside the first. The research design of September 2026 reached 19 process items against 14 storage items before this decision stopped it.
- **Method as optional plugin packs** (an `archcore-research` plugin). Rejected earlier for fragmentation of the MCP namespace and of `.archcore/` ownership (`architecture/one-product-two-entry-points`).
- **Leave the stance implicit** in the narrative rules. Rejected: the narrative rules govern public copy, not design decisions, and the research scoping showed that an implicit stance does not stop a design from drifting.

## Consequences

- Research support ships as two types, three relations, and conventions (`concepts/research-and-evidence-types`); the deferred process items are recorded separately (`product/research-process-deferred`) and enter only on demonstrated need.
- A gate that names a tool, a search strategy, or an agent role is out of contract in the runtime; a gate names document content only.
- The docs site and the landing describe tracks as document filling with checks, never as methodologies. `architecture/conceptual-architecture` keeps "guides the work" for the runtime; that phrase means filling and checking, and this record is where a reader resolves it.
- The measurement above is the test for future proposals: a proposal whose items are mostly process, for a capability with no stored artifact yet, is reordered to ship the vocabulary first.
- `product/design-principles` gains the principle "Store, don't execute".
