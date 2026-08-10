---
title: "Surface Descriptors: Resolved Copy per Public Surface"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Overview

The resolved canonical string for each named public surface. Where a surface appears here, this entry is the one to copy. The strings it draws from are fixed by `product/canonical-narrative`; the category decision behind them is `product/two-discovery-categories`.

This document does not cover page-level SEO structure. That is `product/seo-information-architecture`.

## Content

### Homepage (archcore.ai)

| Slot | String |
|------|--------|
| `<title>` | Archcore — Spec-Driven Development & Context Engineering |
| Meta description | Spec-driven development and context engineering for AI coding agents. Keep specs, architecture, decisions, rules, and plans versioned with code. |
| OG title | Archcore — Spec-Driven Development & Context Engineering |
| OG description | Git-native project context for AI coding agents. Keep specs, architecture, decisions, rules, and plans in Git, and make them available to every agent. |
| Hero eyebrow | Git-native context layer |
| H1 | Spec-Driven Development & Context Engineering for AI Coding Agents |
| Hero subhead | Archcore keeps specs, architecture, decisions, rules, and plans in Git, and makes the right project context available to AI coding agents as they work. |
| Supporting promise | Stop re-explaining your repo to every AI coding agent. |
| Narrative line | Specs define intent. Context preserves understanding. Agents write the code. |
| Primary CTA | Get started |
| Secondary CTA | View on GitHub |

The `<title>` carries both category phrases literally and stays inside the SERP display width. "AI coding agents" is carried by the H1, the description, and the page body.

The hero subhead uses the comma variant of the expanded definition, per clause 17 of `product/canonical-narrative` and the landing no-em-dash policy.

### Homepage section sequence

| # | Section | Heading |
|---|---------|---------|
| 1 | Category and product | Spec-Driven Development & Context Engineering for AI Coding Agents |
| 2 | Problem | Your code is in Git. Your project understanding should be too. |
| 3 | Spec-driven development | Specs that stay connected to implementation |
| 4 | Context engineering | Engineer the context your coding agents work from |
| 5 | Git-native | Project context belongs in Git |
| 6 | Cross-agent | One project context. Every coding agent. |
| 7 | How it works | Capture → Connect → Apply → Evolve |

Section 2 covers: decisions disappear in chat history; instruction files grow into walls of text; every agent sees a different version of the project; specs become stale handoff artifacts; architecture and conventions are re-explained.

Section 5 covers: reviewable in pull requests; versioned with code; portable across tools; no opaque agent memory; team-owned source of truth.

Section 7 verbs: Capture specs, decisions, rules, plans, and project knowledge. Connect related artifacts into project context. Apply the relevant context while agents work. Evolve context with the codebase through Git.

### GitHub organization

| Slot | String |
|------|--------|
| Display name | Archcore |
| Bio | Spec-driven development and git-native context engineering for AI coding agents. |
| Longer description | Archcore builds git-native context infrastructure and spec-driven development for AI coding agents. Keep specs, architecture, decisions, rules, and plans versioned with code. |
| Profile heading | Spec-Driven Development & Context Engineering for AI Coding Agents |
| Profile intro | Archcore is a git-native context layer for AI coding agents. Keep specs, architecture, decisions, rules, and plans in your repository and make the relevant project context available across Claude Code, Cursor, Codex, GitHub Copilot, Gemini CLI, and other MCP-compatible agents. |

Repository slugs stay `archcore-ai/cli` and `archcore-ai/plugin`. Renaming a repository for SEO is out of scope; titles, descriptions, topics, README headings, and landing pages carry the category language instead.

### Archcore CLI

| Slot | String |
|------|--------|
| README H1 | Archcore CLI — Git-Native Context for AI Coding Agents |
| Repository description | Git-native context engineering CLI and MCP server for AI coding agents. Keep specs, ADRs, rules, plans, and project knowledge in Git. |
| README first block | Archcore is a git-native context layer for AI coding agents.<br><br>The CLI keeps specs, architecture decisions, rules, plans, and project knowledge in `.archcore/`, versioned with your code, and serves the relevant context to coding agents through MCP and integrations.<br><br>Use it for persistent project context across Claude Code, Cursor, Codex, GitHub Copilot, Gemini CLI, and other MCP-compatible agents. |
| `--help` short description | Git-native context for AI coding agents. |
| Long description | Manage structured project context in Git and make specs, architecture decisions, rules, plans, and project knowledge available to AI coding agents through MCP. |
| Docs title | Archcore CLI — Git-Native Context & MCP for AI Coding Agents |
| Docs meta description | Install and use Archcore CLI to manage git-native project context and expose specs, ADRs, rules, plans, and project knowledge to AI coding agents through MCP. |

GitHub topics: `ai-coding`, `ai-agents`, `coding-agents`, `context-engineering`, `spec-driven-development`, `mcp`, `model-context-protocol`, `git-native`, `project-context`, `architecture`, `adr`, `specifications`, `developer-tools`.

The CLI owns: `.archcore/`, typed project documents, git-native storage, the local MCP server, document tools, agent integration setup, hooks and integration infrastructure, portability across agents.

### Archcore Plugin

| Slot | String |
|------|--------|
| README H1 | Archcore Plugin — Spec-Driven Development & Context Engineering for AI Coding Agents |
| Repository description | Spec-driven development and context engineering for Claude Code, Cursor, Codex, and GitHub Copilot — backed by project context in Git. |
| README first block | Make your AI coding agent work like it already knows your repo.<br><br>Archcore brings spec-driven development and automatic project context to Claude Code, Cursor, Codex, and GitHub Copilot. Specs, architecture, decisions, rules, and plans live in Git and are applied as the agent works.<br><br>The plugin pairs with Archcore CLI: the CLI provides the git-native context layer and MCP tools; the plugin adds skills, slash commands, gated tracks, routing, and guardrails. |
| Manifest name | archcore |
| Manifest description | Spec-driven development and context engineering for AI coding agents, backed by project context in Git. |
| Marketplace collection description | Archcore plugins for spec-driven development and context engineering with AI coding agents. |
| Docs title | Archcore Plugin — Spec-Driven AI Development with Project Context |
| Docs meta description | Add spec-driven development and automatic project context to Claude Code, Cursor, Codex, and GitHub Copilot with Archcore. |

GitHub topics: `spec-driven-development`, `context-engineering`, `ai-coding`, `coding-agents`, `claude-code`, `cursor`, `codex`, `github-copilot`, `mcp`, `agent-skills`, `project-context`, `architecture`, `developer-tools`.

The plugin owns: automatic context use, skills, slash commands, intent routing, gated tracks, planning, decision and document capture, review, guardrails, host-native UX.

The host list in the repository description is the plugin's host set, which is smaller than the CLI's. That is a scope statement. It does not rank the two entry points, and no surface may add a recommendation label to either.

### Documentation site

| Slot | String |
|------|--------|
| Site title | Archcore Docs — Spec-Driven Development & Context Engineering |
| Homepage H1 | Build with Specs. Code with Context. |
| Homepage intro | Archcore is a git-native context layer for AI coding agents. Use it to manage specs, architecture, decisions, rules, plans, and project knowledge, and make the right context available throughout spec-driven development and implementation. |

Top-level navigation: Getting Started · Concepts · Spec-Driven Development · Context Engineering · CLI · Plugin · Integrations · Document Types · MCP · Reference.

Concept pages, each with one canonical definition and links back to the product and track pages: Project Context · Context Engineering · Spec-Driven Development · Git-Native Context · Context Graph · Specs · Architecture Decisions (ADRs) · Rules · Plans · Project Knowledge · MCP · Agent Integrations.

### Social and listings

| Surface | String |
|---------|--------|
| X / Bluesky / compact bio | Spec-driven development & git-native context engineering for AI coding agents. |
| LinkedIn tagline | Spec-Driven Development & Context Engineering for AI Coding Agents |
| LinkedIn description | Archcore is a git-native context layer for AI coding agents. We help engineering teams keep specs, architecture, decisions, rules, plans, and project knowledge versioned with code and available across coding agents. |
| Hacker News / launch one-liner | Archcore is a git-native context layer for AI coding agents — specs, architecture, decisions, rules, and plans versioned with code and available through MCP. |
| Directory listing, short | Git-native context engineering and spec-driven development for AI coding agents. |
| Directory listing, medium | Archcore keeps specs, architecture, decisions, rules, and plans in Git and makes the relevant project context available to AI coding agents through MCP, integrations, and spec-driven development. |
| Launch headline | Archcore: Spec-Driven Development & Context Engineering for AI Coding Agents |
| Editorial launch headline | Build with Specs. Code with Context. |

A launch does not get its own tagline. Use one of the two headlines above.

### Proof points

Prefer concrete nouns: specs in Git · ADRs in Git · rules in Git · plans in Git · local MCP server · works across coding agents · automatic context · review context changes in PRs · typed Markdown documents · project-owned source of truth.

Weak when used alone: smarter AI · better context · AI-native · agentic platform · intelligent workflows · next-generation developer experience.

**"Workflow" is banned in positioning copy** (`product/messaging-and-voice`). Name the concrete thing instead: skills, slash commands, gated tracks, hooks, review, guardrails.

### Competitive framing

| Alternative | Line |
|-------------|------|
| Methodology and SDD tools | Methodology tools define a development process. Archcore keeps the resulting project knowledge alive, connected, versioned, and available to agents throughout implementation. |
| Memory tools | Memory remembers what happened in previous sessions. Archcore stores what the project says is true. |
| Flat instruction files | Instruction files are useful entry points. Archcore adds typed documents, relations, lifecycle, selective retrieval, and cross-agent portability. |
| RAG and larger context windows | Retrieval can tell an agent what the code says. Archcore makes decisions, constraints, intent, and rationale explicit. |
| Generic documentation | Documentation is written to be read. Archcore project context is structured to be applied by coding agents while they work. |

## Examples

**Good** — a plugin manifest description that matches the table: `"description": "Spec-driven development and context engineering for AI coding agents, backed by project context in Git."`

**Good** — a CLI `--help` line that shortens rather than reinvents: `Git-native context for AI coding agents.`

**Bad** — `"description": "Make your AI agent code with your project's architecture, rules, and decisions."` — the pre-decision string; it carries no category term and appears in five manifests at once.

**Bad** — `<title>Archcore Plugin — repo memory for AI coding agents</title>` — retired category term.

**Bad** — inventing a launch tagline for a release announcement instead of reusing one of the two headlines.
