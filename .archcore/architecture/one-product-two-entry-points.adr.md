---
title: "One Product, Two Entry Points (Plugin and CLI)"
status: accepted
---

## Context

Archcore reaches users in two shapes — the **Plugin** (intent workflows and guardrails layered over the engine) and the **CLI** (the engine itself: context store, MCP server, hooks, scripting). Public surfaces repeatedly face the question of how to frame them relative to each other, and the wrong framing fragments the story.

## Decision

Treat the Plugin and CLI as **one product with two entry points into the same context layer** — never as two separate products, and never as primary-vs-fallback.

- Both are equally capable against the same context and the same MCP tools.
- **Recommended path:** "For most teams, start with the Plugin."
- **Direct path:** "Need the core directly? Use the CLI." — a legitimate choice, not a downgrade.
- Mental model: **CLI = the engine, Plugin = the runtime over it.**

## Alternatives

- **Two products** — fragments the narrative, doubles positioning work, confuses entry points.
- **CLI as fallback** — wrongly implies the CLI is lesser; it is the engine the Plugin runs on.

## Consequences

- All public surfaces use one unified narrative with two clearly labeled entry points.
- Install CTAs lead with the Plugin ("Use the Plugin" / "Install Plugin") and offer the CLI as the direct alternative ("Start with CLI" / "Install CLI"), never as a lesser option.
- Any change to the entry-point story is reflected across all public surfaces together.
- This stance governs the ecosystem; surface-specific messaging must align to it (see `product/messaging-and-voice`).