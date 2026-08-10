---
title: "Glossary"
status: accepted
tags:
  - "concepts"
  - "vocabulary"
---

## Overview

Canonical definitions of Archcore terms. Use these consistently across the ecosystem.

## Terms

**Archcore** — git-native context for AI coding agents: typed, structured documents in a repository that agents read and follow.

**Document** — a Markdown file with YAML frontmatter, named `slug.type.md`, stored in `.archcore/`.

**Document type** — the kind of a document (e.g. adr, rule, spec, plan), encoded in the filename suffix. Determines the template and the virtual category.

**Virtual category** — `vision`, `knowledge`, or `experience`; derived from the document type, not from any directory.

**Vision / Knowledge / Experience** — what to build & why / how the system works / what we learned.

**Frontmatter** — the YAML header of a document: `title`, `status`, optional `tags`.

**Status** — a document's lifecycle state: `draft`, `accepted`, or `rejected`.

**Relation** — a directed link between two documents: `implements`, `extends`, `depends_on`, or `related`.

**Relation graph** — the network formed by relations; lets an agent load a whole chain of related context.

**MCP (Model Context Protocol)** — the open protocol agents use to read, search, create, update, and relate documents. The single mutation surface.

**Lifecycle hooks** — the three events Archcore runs on: `SessionStart` (context injection), `PreToolUse` (write guard and code-alignment injection), `PostToolUse` (validation and advisories). See `architecture/lifecycle-hooks`.

**Guardrail** — a check carried on a lifecycle hook. Exactly one is blocking (the write guard); the rest report and never modify a document.

**Write guard** — the blocking guardrail that refuses a direct editor write into `.archcore/`, so MCP stays the only mutation surface.

**Code-alignment injection** — delivery of the rules, specs, and decisions that apply to a file, at the moment the agent edits it.

**Engine (CLI)** — the component that stores and serves the context, exposes it over MCP, and runs the lifecycle hooks and guardrails.

**Runtime (Plugin)** — the optional higher-level experience over the engine: the command surface and the gated tracks beneath it.

**Entry point** — a way into the same context layer; Archcore has two (Plugin and CLI) for one product.

**Shared (global) source** — a context layer mounted read-only by other projects so ecosystem-wide truths live in one place; consumers depend on it, never the reverse.

**Document track (cascade)** — a recommended multi-document flow of *types*, e.g. `idea → prd → plan`. See `concepts/document-tracks`.

**Gated track** — a runtime flow of *gates* beneath a command, which produces documents and resumes across sessions. Distinct from a document track; see `concepts/gated-tracks`.

**Gate** — one stage of a gated track: entry conditions, a bounded question budget, the document it produces, and its exit checks.

## A note on numbered layers

`architecture/conceptual-architecture` numbers four **architectural roles** — context, engine, runtime, access. Tool repositories number their own internal layers, and the two schemes do not line up. Across repository boundaries, name the role rather than a number.
