---
title: "Conceptual Architecture"
status: accepted
tags:
  - "architecture"
---

## Overview

Archcore is layered: durable context at the base, an engine that serves and guards it, an optional runtime above, and a tool-agnostic access path. This is the conceptual model — it names roles, not implementations. Which component owns which responsibility is fixed by `architecture/engine-runtime-boundary`.

## Layers

**1. Context layer — the substance.** Typed Markdown documents in `.archcore/`, versioned in Git. The durable truth: decisions, rules, plans, specs, guides, and patterns. Everything else exists to produce, serve, or consume it.

**2. Engine — serves and guards the context.** Stores documents, answers queries and searches, maintains the relation graph, and runs the lifecycle hooks: session context injection, the write guard, code-alignment injection before an edit, and post-write validation. It exposes the context to agents through MCP and is the single mutation surface — context is created and changed through the engine, never by ad-hoc file edits.

**3. Runtime — guides the work (optional).** A higher-level experience over the engine: a small command surface and the gated tracks beneath it (see `concepts/gated-tracks`), which interview the user only where evidence is missing and produce linked typed documents. It makes the engine effortless to use but is never required: any MCP-aware agent can use the engine directly, and every guardrail reaches that agent through the engine's hooks.

**4. Access — tool-agnostic.** Agents reach the context two ways: **MCP** (read, search, create, update, relate) and **lifecycle hooks** (context injected at session start and before an edit; validation after a write). One context layer serves every agent through the same open standards.

## Why layered

- The context outlives any tool — it is plain files in Git.
- The engine makes one context layer reusable across every agent, with no per-tool duplication.
- The runtime can evolve the experience without changing the stored context.
- Separation keeps the substance (documents) independent of how it is produced or consumed.

## A note on the word "layer"

This model numbers **architectural roles**. Tool repositories also number their own internal layers, and the numbering does not line up — the plugin's "layer 1" is its command surface and its "layers 4–5" are the engine's MCP and hook surfaces. When a document refers to a layer across repository boundaries, it names the role (context, engine, runtime, access) rather than a number.

## Shared context

A context layer can also be mounted **read-only** by other projects as a shared, higher-level source — so ecosystem-wide truths live in one place instead of being copied into every repo. The relationship is one-directional: a project may read a shared source; a shared source never depends on its consumers. See `concepts/global-sources`.
