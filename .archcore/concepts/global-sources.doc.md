---
title: "Global Sources (Shared Org-Wide Context)"
status: accepted
tags:
  - "architecture"
  - "concepts"
---

## Overview

A **global source** is shared, org-wide Archcore context that a repository mounts **read-only** alongside its own `.archcore/`. It is how knowledge that is true for the whole ecosystem — product positioning, architecture, concepts, cross-cutting rules — lives in one place (e.g. this `global` repo) and is consumed by every project without copy-paste.

This is the mechanism that powers a single source of truth across many repos. This document defines the *model* every consumer must honor, tool-agnostically; the CLI implementation lives in `cli/.archcore/globals/`.

## The model

- **Read-only mount.** A consumer references a global source; it can read but never write it. Global documents are surfaced by `list_documents` / `search_documents` alongside local ones, tagged `source_kind: "global"`.
- **Local overrides global (precedence).** When a local document and a global document cover the same ground, the local one is authoritative. The global doc is a default the local can override.
- **One-directional invariant (`local → global`).** A global may be referenced *by* a local, never the reverse. A shared global must not accumulate back-references to the repos that consume it, and must not reference another global (no transitive globals).
- **One writable primary.** A repo writes only to its own local `.archcore/`; every mounted global is read-only.
- **Mandatory, fail-loud.** A declared global source that cannot be resolved is an error surfaced loudly, not silently skipped — so missing shared context never degrades quietly.

## Reading convention for agents

- Treat global documents as **defaults a local document can override**.
- Both local and global results appear in search; the agent disambiguates via `source_kind`.
- **Never edit, delete, or add relations to a global document** from a consumer repo. Change shared context in the source repo itself.

## Why it matters

Without global sources, ecosystem-wide knowledge (positioning, the host roster, the document model) gets duplicated into every repo and drifts. Global sources make that knowledge **write-once, read-everywhere** — the backbone of the Teams / multi-repo story.

## Implementation

- Declared per-repo in `.archcore/settings.json` under `globals[]` (`{ "id", "path" }`).
- Full CLI contract, enforcement, and operational guides: `cli/.archcore/globals/` (`global-sources.spec`, `globals-are-mandatory.adr`, `local-overrides-global.rule`, `globals-are-read-only-everywhere.rule`, `declaring-global-sources.rule`, `vendoring-a-global.guide`).
