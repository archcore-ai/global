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

**MCP (Model Context Protocol)** — the open protocol agents use to read, search, create, update, and relate documents.

**Session hooks** — automatic injection of relevant context when an agent session starts.

**Engine (CLI)** — the component that stores and serves the context and exposes it over MCP.

**Runtime (Plugin)** — the optional higher-level experience over the engine: intent workflows, guardrails, applied context injection.

**Entry point** — a way into the same context layer; Archcore has two (Plugin and CLI) for one product.

**Shared (global) source** — a context layer mounted read-only by other projects so ecosystem-wide truths live in one place; consumers depend on it, never the reverse.

**Track (cascade)** — a recommended multi-document flow (e.g. idea → prd → plan).