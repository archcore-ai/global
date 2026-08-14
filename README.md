# Archcore — Global Context

This repository is the **shared, high-level context for the whole Archcore ecosystem**. Other Archcore projects mount it read-only as a global source, so ecosystem-wide truths live in one place instead of being copied into every repo.

## What belongs here

Only **high-level, conceptual, product-wide** knowledge — true for Archcore as a whole, and otherwise duplicated across repos:

- what Archcore is, its principles, positioning, audience, and voice;
- the shared conceptual model (document types, categories, relations, tracks);
- the conceptual architecture and how agents use the context;
- market and competitive analysis that informs positioning on every surface;
- techniques and rollouts that span more than one repository.

## What does NOT belong here

- Implementation contracts owned by one repo — internal mechanics, tool contracts, per-repo enforcement rules.
- A decision that binds only one consumer repo.
- Volatile per-repo state — release status, version specifics, backlog.

Repo-specific decisions and enforcement stay in each consumer's own `.archcore/`.

## The one-directional invariant

Consumers mount this global read-only; this global never depends on a consumer. The invariant is about the **relation graph and the dependency direction**: no document here carries a relation to a consumer document, and no document here needs a consumer to make sense.

It is not a ban on naming a consumer. An ecosystem-wide document may point at where each repo implements its half — a rollout that coordinates one narrative change across all four repositories (`product/narrative-rollout`), a technique shared by both web properties (`web/og-image-generation`), or a roster reconciling what the CLI and the plugin each support (`architecture/supported-ai-hosts`).

The test is ownership, not vocabulary. A fact that is true for the ecosystem, and would otherwise be copied into several repos, belongs here even when stating it requires a consumer's path.

## How it is consumed

A consuming repo declares this source in its own `.archcore/settings.json`:

```json
{ "globals": [ { "id": "archcore", "path": "../global/.archcore" } ] }
```

The documents are read-only to consumers and surface through the Archcore MCP read tools.

## Layout

Context lives in `.archcore/` as typed Markdown, edited through the Archcore MCP tools — see `product/`, `concepts/`, `architecture/`, `market/`, and `web/`.
