---
title: "Core Concepts & Vocabulary"
status: accepted
tags:
  - "concepts"
  - "vocabulary"
---

## Overview

The shared vocabulary of Archcore. Every project in the ecosystem uses the same document types, categories, naming convention, statuses, and relation types. This is the canonical conceptual reference; detailed, implementation-grade type guidance lives with each tool.

The accepted vocabulary includes `research` in vision and `evidence` in knowledge. The CLI release and runtime routing changes remain pending — `concepts/research-and-evidence-types` and `product/research-direction`.

## Documents

A document is a Markdown file with YAML frontmatter, stored in `.archcore/`.

- **Naming:** `<slug>.<type>.md` — e.g. `jwt-strategy.adr.md`, `error-wrapping.rule.md`. The type lives in the filename.
- **Frontmatter:** `title`, `status`, optional `tags`.
- **Directory layout is free-form** — organize by domain, feature, or team. Subdirectories carry no meaning; the `.type` suffix does.

## Virtual categories

Categories are *derived from the document type*, not from directories:

| Category | Means | Types |
|----------|-------|-------|
| **vision** | what to build & why | prd, idea, plan, rnd, research · mrd, brd, urd · brs, strs, syrs, srs |
| **knowledge** | how the system works | adr, rfc, rule, guide, doc, spec, evidence |
| **experience** | what we learned | task-type, cpat |

Vision includes territory discovery; knowledge includes reusable materials. These assignments follow `concepts/research-and-evidence-types`.

## Accepted document types (21)

**Knowledge** — `adr` (final decision), `rfc` (open proposal), `rule` (team standard), `guide` (step-by-step), `doc` (reference material), `spec` (contract of a depended-on boundary, captured after code or specified ahead of it), `evidence` (one material with its locator and extract).

**Vision** — `prd` (product requirements), `idea` (concept to explore), `plan` (phased tasks), `rnd` (recommendation-oriented research), `research` (territory discovery closed by coverage); *sources track*: `mrd` (market), `brd` (business), `urd` (user); *ISO 29148 track*: `brs → strs → syrs → srs` (formal requirements cascade).

**Experience** — `task-type` (reusable workflow for a recurring task), `cpat` (code-pattern change / incident learning).

## Statuses (3)

`draft` → `accepted` → `rejected`. That's the whole lifecycle — intentionally minimal. A document is created as a draft; promotion is an explicit act, never a side effect of a hook or an automated check.

## Accepted relations (7)

Directed edges between documents, stored in the sync manifest, not in the document files:

- **implements** — source fulfills what target specifies (plan implements prd)
- **extends** — source builds upon target (rfc extends an adr)
- **depends_on** — source requires target to proceed (plan depends_on adr)
- **related** — general association
- **supports** — material points to the statement it backs
- **contradicts** — challenger points to the statement it disputes
- **supersedes** — newer document points to the older document it replaces

Documents linked into recurring flows form *document tracks* — see `concepts/document-tracks`, and `concepts/gated-tracks` for the runtime flows that walk them.

## Storage & access

- **Git-native:** everything is Markdown in `.archcore/`, reviewed in PRs, versioned with code.
- **MCP is the mutation surface:** agents create, read, update, and search documents and relations through MCP tools, rather than editing context by hand. A direct editor write into `.archcore/` is refused.
- **Lifecycle hooks** inject context at session start and before an edit, and validate after a write — see `architecture/lifecycle-hooks`.

## Simplicity by constraint

Accepted vocabulary: 3 statuses · 21 types (12 vision, 7 knowledge, 2 experience) · 7 relation types · 1 naming convention. Few rules to learn, easy to enforce.
