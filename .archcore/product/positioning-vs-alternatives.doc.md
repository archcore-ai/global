---
title: "Positioning vs. Alternatives"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Overview

How Archcore differs from the things teams reach for instead. The defensible claim is four properties held together — **typed documents, an explicit relation graph, a status lifecycle, and human authorship** — readable by any host. Each property alone is matched somewhere in the landscape; the combination is not (`market/moat-parity-and-gaps`).

## What no longer differentiates

Two claims this document previously led with are now table stakes across the nine closest competitors, verified 2026-08-12 (`market/moat-parity-and-gaps`).

| Retired claim | Why it stopped working |
|---|---|
| "It lives in Git" | Nine of nine store plain files in the repository, versioned and reviewed in pull requests |
| "It works with any agent" | Host-agnostic setup comes free with `AGENTS.md`-compatible tooling |

Both remain true, and both remain useful as supporting proof. Neither carries a comparison on its own.

## vs. flat instruction files (CLAUDE.md, .cursorrules, AGENTS.md)

Instruction files are flat memory; Archcore is structured system context. Flat files work for a handful of short-lived rules, then become an unmaintainable wall of text — no types, no links, no lifecycle, copy-pasted per tool. Archcore gives typed documents, an explicit relation graph, and a `draft → accepted → rejected` lifecycle, so an agent loads the applicable chain rather than the whole file.

This is the largest competitor by adoption: `AGENTS.md` is stewarded by the Linux Foundation's Agentic AI Foundation and present in more than 60,000 repositories (`market/competitive-landscape`).

## vs. repo-native structured artifacts (Kiro, OpenSpec, Spec Kitty, Spec Kit, Tessl)

The nearest neighbours, and the cluster where the four properties do the work. Each stores explicit human-authored intent inside the repository, and each holds part of the set: Kiro has the richest feature surface and gives up portability; OpenSpec has the lifecycle and gives up typing and relations; Spec Kit owns the spec-driven narrative and the distribution without a relation graph.

Archcore's type set spans decisions, rules, specs, guides, requirements cascades, and experience patterns, where competitors ship three to five artifact shapes — usually requirements, design, and tasks (`market/moat-parity-and-gaps`).

## vs. RAG / semantic search over the codebase

RAG retrieves passages by similarity; it surfaces *what the code says*, not *what was decided and why*. Inferred context reproduces what the code already contains — it cannot recover a rejected alternative, an unwritten constraint, or a decision that was never executed. Archcore stores those explicitly, typed and linked.

## vs. a bigger context window

A larger window lets the agent read more; it does not tell the agent what is authoritative, current, or relevant. Archcore is selective by design: the agent loads the applicable decisions and rules, not the entire repository.

## vs. hosted "memory" features

Memory records what happened in previous sessions; Archcore records what the project says is true. That distinction is *authored versus captured*, and it is the one that does not commoditize as managed memory services mature (`market/commoditization-and-bundling-risks`). Tool-specific memory is also volatile and opaque, and it carries no status a reviewer can challenge.

## The throughline

Existing options are flat, inferred, volatile, or partially typed. Archcore is **typed, related, lifecycle-governed, and human-authored** — four properties held together, in files any host can read.
