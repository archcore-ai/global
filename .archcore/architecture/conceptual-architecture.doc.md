---
title: "Conceptual Architecture"
status: accepted
---

## Overview

Archcore is layered: durable context at the base, an engine that serves it, an optional runtime above, and a tool-agnostic access path. This is the conceptual model — it names roles, not implementations.

## Layers

**1. Context layer — the substance.** Typed Markdown documents in `.archcore/`, versioned in Git. The durable truth: decisions, rules, plans, specs, guides, and patterns. Everything else exists to produce, serve, or consume it.

**2. Engine — serves the context.** Stores documents, answers queries and searches, maintains the relation graph, and injects relevant context when an agent session starts. It exposes the context to agents through MCP and is the single mutation surface — context is created and changed through the engine, never by ad-hoc file edits.

**3. Runtime — guides the work (optional).** A higher-level experience over the engine that adds intent-based workflows, guardrails, and applied context injection before edits. It makes the engine effortless to use but is never required: any MCP-aware agent can use the engine directly.

**4. Access — tool-agnostic.** Agents reach the context two ways: **MCP** (read, search, create, update, relate) and **session hooks** (context injected when a session starts). One context layer serves every agent through the same open standards.

## Why layered

- The context outlives any tool — it is plain files in Git.
- The engine makes one context layer reusable across every agent, with no per-tool duplication.
- The runtime can evolve the experience without changing the stored context.
- Separation keeps the substance (documents) independent of how it is produced or consumed.

## Shared context

A context layer can also be mounted **read-only** by other projects as a shared, higher-level source — so ecosystem-wide truths live in one place instead of being copied into every repo. The relationship is one-directional: a project may read a shared source; a shared source never depends on its consumers.