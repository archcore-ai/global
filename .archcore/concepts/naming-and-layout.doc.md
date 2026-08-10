---
title: "Naming and Directory Layout"
status: accepted
tags:
  - "concepts"
  - "vocabulary"
---

## Overview

The filename is the schema. `concepts/core-concepts` states the convention in one line; this document is the full contract every tool implements and every consumer may rely on — what a valid name is, what the scanner does with an invalid one, and what a directory does and does not mean.

## The filename

```
<slug>.<type>.md
```

- **Slug** — lowercase alphanumeric segments separated by single hyphens, matching `^[a-z0-9]+(-[a-z0-9]+)*$`.
- **Type** — one of the 19 valid types. It selects the template, the section contract, and the virtual category.
- **Extension** — always `.md`.

Valid: `jwt-strategy.adr.md`, `api-error-format.rule.md`, `callbacks-to-async.cpat.md`.

Invalid slugs: `JWT_Strategy` (uppercase, underscore), `use postgres` (space), `my.decision` (dot inside the slug — the dot is the type separator).

A file with no recognized type segment is not rejected. The scanner keeps it and categorizes it as **knowledge**. Silence, not an error: an unreadable name costs the document its type, not its existence.

## Directories mean nothing

Layout inside `.archcore/` is free-form. Organize by domain, feature, team, or not at all.

- The virtual category is derived from the **type suffix**, never from the path. Moving a file between directories never changes its category.
- Nesting depth is unlimited, and directory names carry no constraints (lowercase with hyphens reads best).
- Hidden directories — those starting with `.` — are skipped by the scan.
- The legacy `vision/` `knowledge/` `experience/` layout still works. Those are ordinary directories with no special meaning, so no migration is needed and none is offered.

This is the property that makes the store cheap to reorganize: a folder move is never a semantic change.

## Layout guidance

Start flat. A repository with fewer than about ten documents gains nothing from a tree, and a tree designed before the documents exist is designed against a guess.

Group into subdirectories when finding a document starts costing a scan of the list — usually by domain (`auth/`, `payments/`, `api/`), sometimes by team. Mixed approaches are fine: cross-cutting rules at the root, domain documents below.

## Reserved files

| File | Purpose |
|------|---------|
| `settings.json` | Repository configuration: sync mode and mounted global sources |
| `.sync-state.json` | Tool-managed: the relation graph and sync hashes. Tracked in Git so the graph is shared |

Both are skipped when scanning for documents, and both are managed by the engine. Editing `.sync-state.json` by hand is how a relation graph gets corrupted; change relations through the MCP tools (`concepts/relation-conventions`).
