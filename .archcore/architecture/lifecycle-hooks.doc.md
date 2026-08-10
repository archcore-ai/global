---
title: "Lifecycle Hooks and Guardrails"
status: accepted
tags:
  - "architecture"
  - "concepts"
---

## Overview

MCP lets an agent *ask* for context. Lifecycle hooks make context arrive **without being asked** — and stop a write that would corrupt the store. Together they are the second half of the access layer in `architecture/conceptual-architecture`. This document defines the tool-agnostic model: which events exist, what runs on each, and what a host that cannot carry an event loses. The engine owns all of it (`architecture/engine-runtime-boundary`); per-host spellings and wire protocols live in `cli/.archcore/integrations/`.

## The three events

Archcore uses exactly three lifecycle events, in each host's own spelling. The `Stop` and `UserPromptSubmit` families are deliberately unsupported.

| Event | When it fires | What Archcore does |
|-------|---------------|--------------------|
| `SessionStart` | An agent session opens | Injects the session recap: the document index, relations, what is accepted, what is in progress |
| `PreToolUse` | Before a file write or edit | Runs the **write guard** (blocking) and **code-alignment injection** (advisory) |
| `PostToolUse` | After a document mutation | Runs validation, the relation-cascade notice, the precision check, and the staleness advisory (all advisory) |

## Blocking versus advisory

Exactly one guardrail can deny: the **write guard**, which refuses a direct editor write into `.archcore/`. It exists because MCP is the single mutation surface — a path the MCP tools refuse must not be reachable by going around them. The guard and the MCP write tools consult one predicate, so the two verdicts cannot diverge.

Every other guardrail is advisory: it reports and exits successfully. Staleness detection, validation, and precision checks never modify a document and never change a status on their own.

## Why the events map to the jobs

- `SessionStart` serves Job 2 — the agent arrives already knowing what is decided and in flight.
- `PreToolUse` serves Job 1 — the applicable rules, specs, and decisions reach the agent at the moment of the edit, which is why the runtime needs no "load my context" command.
- `PostToolUse` serves Job 3 — a newly recorded decision is validated and linked while it is still being written.

See `product/jobs-to-be-done`.

## Graceful degradation

A host that cannot carry an event loses that event's value and nothing else:

- No `PreToolUse` context payload (a permission-only pre-write event) → the write guard still runs; code-alignment injection does not.
- No lifecycle hooks at all (MCP-only or manual tier) → the agent keeps every MCP tool and loses automatic injection and the write guard.
- Hooks delivered through a host plugin rather than a config file → the same three events reach the same handlers by a different wiring route.

Per-host tiers and known limitations: `architecture/supported-ai-hosts`.

## Duplication

A host can be wired twice — by the runtime's own hook config and by the engine's — and can also read another host's config file. Archcore deduplicates a repeated run rather than assuming a single writer. The cross-repository half of that contract is `architecture/plugin-cli-compatibility`.

## Where the implementation lives

- **Engine** — event wiring, per-host dialects, handlers, and the dedup stamp: `cli/.archcore/integrations/` (`hook-runtime.spec`, `session-start-context.spec`, `cli-hooks-reference.doc`, `hook-guardrails-in-the-cli.adr`).
- **Runtime** — nothing. Guardrails are not runtime responsibilities.
