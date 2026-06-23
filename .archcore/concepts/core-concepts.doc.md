---
title: "Core Concepts & Vocabulary"
status: accepted
---

## Overview

The shared vocabulary of Archcore. Every project in the ecosystem uses the same document types, categories, naming convention, statuses, and relation types. This is the canonical conceptual reference; detailed, implementation-grade type guidance lives with each tool.

## Documents

A document is a Markdown file with YAML frontmatter, stored in `.archcore/`.

- **Naming:** `<slug>.<type>.md` — e.g. `jwt-strategy.adr.md`, `error-wrapping.rule.md`. The type lives in the filename.
- **Frontmatter:** `title`, `status`, optional `tags`.
- **Directory layout is free-form** — organize by domain, feature, or team. Subdirectories carry no meaning; the `.type` suffix does.

## Virtual categories

Categories are *derived from the document type*, not from directories:

| Category | Means | Types |
|----------|-------|-------|
| **vision** | what to build & why | prd, idea, plan · mrd, brd, urd · brs, strs, syrs, srs |
| **knowledge** | how the system works | adr, rfc, rule, guide, doc, spec |
| **experience** | what we learned | task-type, cpat |

## Document types (18)

**Knowledge** — `adr` (final decision), `rfc` (open proposal), `rule` (team standard), `guide` (step-by-step), `doc` (reference material), `spec` (boundary contract).

**Vision** — `prd` (product requirements), `idea` (concept to explore), `plan` (phased tasks); *sources track*: `mrd` (market), `brd` (business), `urd` (user); *ISO 29148 track*: `brs → strs → syrs → srs` (formal requirements cascade).

**Experience** — `task-type` (reusable workflow for a recurring task), `cpat` (code-pattern change / incident learning).

## Statuses (3)

`draft` → `accepted` → `rejected`. That's the whole lifecycle — intentionally minimal.

## Relations (4)

Directed edges between documents, stored in the sync manifest, not in the document files:

- **implements** — source fulfills what target specifies (plan implements prd)
- **extends** — source builds upon target (rfc extends an adr)
- **depends_on** — source requires target to proceed (plan depends_on adr)
- **related** — general association

Documents linked into recurring flows form *tracks* — see `concepts/document-tracks`.

## Storage & access

- **Git-native:** everything is Markdown in `.archcore/`, reviewed in PRs, versioned with code.
- **MCP is the mutation surface:** agents create, read, update, and search documents and relations through MCP tools, rather than editing context by hand.
- **Session hooks** inject relevant context at the start of an agent session.

## Simplicity by constraint

3 statuses · 18 types · 4 relation types · 1 naming convention. Few rules to learn, easy to enforce.