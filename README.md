# Archcore — Global Context

This repository is the **shared, high-level context for the whole Archcore ecosystem**. Other Archcore projects mount it read-only as a global source, so ecosystem-wide truths live in one place instead of being copied into every repo.

## What belongs here

Only **high-level, conceptual, product-wide** knowledge — true for Archcore as a whole, and otherwise duplicated across repos:

- what Archcore is, its principles, positioning, audience, and voice;
- the shared conceptual model (document types, categories, relations, tracks);
- the conceptual architecture and how agents use the context.

## What does NOT belong here

- Implementation specifics — stacks, file paths, internal mechanics, tool contracts.
- Anything about a particular consumer repo. **Global knows nothing about local.**
- Volatile state — roadmaps, host-support status, version specifics.

Implementation contracts and repo-specific decisions stay in each consumer's own `.archcore/`. The relationship is one-directional: consumers reference this global; this global never references a consumer.

## How it is consumed

A consuming repo declares this source in its own `.archcore/settings.json`:

```json
{ "globals": [ { "id": "archcore", "path": "../global/.archcore" } ] }
```

The documents are read-only to consumers and surface through the Archcore MCP read tools.

## Layout

Context lives in `.archcore/` as typed Markdown, edited through the Archcore MCP tools — see `product/`, `concepts/`, and `architecture/`.
