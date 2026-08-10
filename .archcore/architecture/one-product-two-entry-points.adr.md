---
title: "One Product, Two Entry Points (Plugin and CLI)"
status: accepted
tags:
  - "architecture"
  - "product"
---

## Context

Archcore reaches users in two shapes — the **Plugin** (the command surface and gated tracks over the engine) and the **CLI** (the engine itself: context store, MCP server, hooks, guardrails, scripting). Public surfaces repeatedly face the question of how to frame them relative to each other, and the wrong framing fragments the story.

The original framing named the Plugin the recommended path. That proved wrong in practice for one reason: a user cannot act on a recommendation they are ineligible for. The Plugin runs on four hosts; the CLI reaches all eight. A visitor running Gemini CLI who is told to "start with the Plugin" has been given advice they cannot take, and a recommendation label makes the CLI read as the consolation prize it is not.

## Decision

Treat the Plugin and CLI as **one product with two entry points into the same context layer** — never as two separate products, never as primary-vs-fallback, and **never as recommended-vs-alternative**.

- Both are equally capable against the same context and the same MCP tools.
- **Frame the choice by the host the user runs, not by our preference.** Plugin — for the hosts in its coverage set. CLI — for every other MCP-aware agent, and for CI and scripting.
- **No "(recommended)" labels on any surface.** Both install paths are presented as peers.
- Gentle emphasis is allowed: the Plugin may describe itself as the most polished experience *on the hosts it supports*. That is a scope statement, not a ranking.
- Mental model: **CLI = the engine, Plugin = the runtime over it** (`architecture/engine-runtime-boundary`).

## Alternatives

- **Two products** — fragments the narrative, doubles positioning work, confuses entry points.
- **CLI as fallback** — wrongly implies the CLI is lesser; it is the engine the Plugin runs on.
- **Plugin as the recommended path** — the original framing, retired on 2026-07-06. It routes users by our preference rather than by their eligibility, and it mislabels the CLI for the majority of hosts.

## Consequences

- All public surfaces use one unified narrative with two peer entry points, chosen by host.
- Install CTAs present both paths without ranking language. A surface that must pick a default tab picks the one that works everywhere.
- Any change to the entry-point story is reflected across all public surfaces together.
- This stance governs the ecosystem; surface-specific messaging must align to it (see `product/messaging-and-voice`). The landing site's `messaging-alignment` rule holds the per-surface enforcement, including which copy layers must change together.
