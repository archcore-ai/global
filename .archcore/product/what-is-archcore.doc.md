---
title: "What Archcore Is"
status: accepted
tags:
  - "product"
---

## Overview

**Archcore is git-native context for AI coding agents.** It turns a repository into typed, structured, machine-readable context — decisions, rules, plans, specs, and patterns stored as Markdown in `.archcore/` — that coding agents discover, read, and follow automatically across every session.

> The agent stops guessing and starts following the system.

> Git ships your code. CI/CD ships your delivery. Archcore ships your understanding.

## The problem

AI coding agents read your *code* but not the *architecture, decisions, and conventions* behind it. Every session starts from zero. Without durable context, agents:

- drop files where they don't belong and reinvent patterns you already standardized
- re-litigate decisions the team already made
- need the same constraints re-explained in every chat
- lose project truth the moment the session ends

Teams patch this with scattered `CLAUDE.md`, `.cursorrules`, `/docs`, and tribal knowledge — flat memory that doesn't scale, isn't typed, and isn't reusable across tools.

## The solution

Archcore stores project knowledge as **typed documents** with YAML frontmatter, versioned in Git inside `.archcore/`, and exposes them to any agent through **MCP (Model Context Protocol)** plus session hooks. One setup works across every MCP-aware agent.

- **Structured, not flat** — typed documents (ADR, rule, spec, plan, …) with templates, statuses, and a relation graph, instead of an ever-growing wall of text.
- **Durable** — context survives sessions, agents, branches, and teammates; reviewed in PRs.
- **Repo-native** — lives next to the code it describes; no database, no external service.
- **Tool-agnostic** — one context layer serves every MCP-aware coding agent.

## What it is NOT

- Not a chatbot, code generator, or IDE replacement.
- Not "just another docs tool", and not a generic knowledge base / RAG layer.
- Not "AI magic" — it is infrastructure for repo-aware agents.

## Why it matters

> Instruction files tell the agent *what you want*. Archcore tells the agent *how your system works* — so the agent can follow your system instead of guessing it.

See `concepts/core-concepts` for the shared vocabulary and `product/design-principles` for the principles behind the product.