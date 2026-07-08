---
title: "Positioning vs. Alternatives"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Overview

How Archcore differs from the things teams reach for instead. Archcore is structured, durable, repo-native context — not a bigger pile of text, not search, not a chat feature.

## vs. flat instruction files (CLAUDE.md, .cursorrules, AGENTS.md)

Instruction files are flat memory; Archcore is structured system context. Flat files work for a handful of short-lived rules, then become an unmaintainable wall of text — no types, no links, no lifecycle, copy-pasted per tool. Archcore gives typed documents, an explicit relation graph, a `draft → accepted → rejected` lifecycle, and one setup that serves every agent.

## vs. RAG / semantic search over the codebase

RAG retrieves passages by similarity; it surfaces *what the code says*, not *what was decided and why*. Archcore stores the decisions, rules, and rationale explicitly — typed and linked — the context that is not recoverable from the code itself.

## vs. a bigger context window

A larger window lets the agent read more; it does not tell the agent what is authoritative, current, or relevant. Archcore is selective by design: the agent loads the applicable decisions and rules, not the entire repository.

## vs. hosted "memory" features

Tool-specific memory is volatile, opaque, and locked to one vendor. Archcore is versioned in your Git history, reviewable in PRs, portable across every agent, and owned by you.

## The throughline

Existing options are flat, volatile, or generic. Archcore is **structured, durable, and repo-native** — decisions live next to the code, are reviewed like code, and persist across agents, sessions, and teammates.