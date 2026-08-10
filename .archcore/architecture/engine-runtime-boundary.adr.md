---
title: "Engine / Runtime Ownership Boundary"
status: accepted
tags:
  - "architecture"
  - "product"
---

## Context

Archcore ships as two entry points into one context layer (`architecture/one-product-two-entry-points`): the CLI is the engine, the plugin is the runtime over it. Which side owns a given responsibility was decided twice, from two sides and in two repositories — the CLI recorded porting the guardrails into its binary, the plugin recorded deleting its MCP track prompts and ceding hook parity to the CLI. Neither record is reachable from the other repository, so the boundary had no canonical statement and drifted in the ecosystem docs, which still described guardrails as a runtime feature.

Two failure modes followed. A CLI-only user received no write protection and no pre-edit context, because the guardrails were plugin shell scripts wired onto a subset of hosts. And one contract had two owners — the document precision canon existed as prompt text in the plugin and as template code in the CLI — so a change on one side did not reach the check on the other.

## Decision

The **engine owns everything that must reach every MCP-aware agent**; the **runtime owns everything that is prompt work**. Concretely:

| Responsibility | Owner |
|---|---|
| Document storage, scanning, validation, relation graph | Engine |
| MCP tools — the single mutation surface | Engine |
| Lifecycle hook wiring and runtime for every host | Engine |
| Guardrails: write guard, code-alignment injection, post-write validation, staleness advisory | Engine |
| Document templates and the precision canon they are measured against | Engine |
| Host detection, MCP config, and instruction-file wiring | Engine |
| Command surface — `init`, `plan`, `document`, `review` | Runtime |
| Gated tracks, gate records, and interview mechanics | Runtime |
| Type routing and elicitation for a given user request | Runtime |
| Agent (subagent) definitions | Runtime |

A capability that a CLI-only user must have MUST live in the engine. A capability expressible only as model instructions MUST live in the runtime. Neither side reimplements the other's half.

## Alternatives Considered

1. **Runtime owns the guardrails** (the prior shape) — rejected because it strands every CLI-only user and every host without a plugin adapter, and because shell and Go implementations of one predicate drift.
2. **Engine owns the tracks** (tracks as MCP prompts or an `archcore track` command) — rejected because elicitation quality in fixed prompt text caps at a one-sentence confirmation gate, and orchestration logic does not belong in a CRUD server.
3. **Keep both records repo-local and cross-link them** — rejected because a consumer of the shared context (docs site, landing, a new host adapter) reads neither repository's internals and needs one statement of the split.

## Consequences

- One owner per contract; the shell-and-Go duplication of the guardrails collapses.
- Guardrails reach all eight hosts in the roster, not the subset with a plugin adapter.
- CLI-only users lose the runtime's track prompts. Their flow-guidance floor is the type-selection rules the MCP server carries in its instructions.
- The runtime stays swappable: a second runtime over the same engine changes no guardrail.
- Cross-repository release skew becomes a first-class concern — see `architecture/plugin-cli-compatibility`.

## Superseded when

- A host-portable MCP primitive can express the elicitation contract to subagents, which would let the engine own tracks.
- The engine's hook handlers cannot meet the per-event time budgets on a roster host, which would push a guardrail back to the runtime.
