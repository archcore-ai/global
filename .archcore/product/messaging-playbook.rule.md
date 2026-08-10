---
title: "Messaging Playbook: Hierarchy, Mechanism & Channels"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Rule

The operational playbook for outward-facing Archcore copy — how the canonical strings are ordered and which one leads on each channel. The strings themselves are fixed by `product/canonical-narrative`; the stance, voice, and vocabulary by `product/messaging-and-voice`; the resolved per-surface copy by `product/surface-descriptors`. This playbook *sequences* them and must not restate them.

### Messaging hierarchy

| Order | Role | Phrase |
|-------|------|--------|
| First | Category (discovery surfaces) | Spec-Driven Development & Context Engineering for AI Coding Agents |
| First | Benefit (product surfaces) | Git-native context for AI coding agents |
| Second | Product definition | Archcore is a git-native context layer for AI coding agents |
| Third | Mechanism (delivery) | CLI and local MCP server |
| Fourth | Value explanation | Archcore keeps specs, architecture, decisions, rules, and plans in Git and makes the right project context available to AI coding agents as they work |

The two "First" entries are not competing. A surface leads with the **category line** when its job is discovery (page titles, SEO-critical headings, pillar and category pages, organization profiles). It leads with the **benefit phrase** when its job is explanation to a reader already in the funnel (README first line, CLI `--help`, compact bios).

Mechanism never leads. **Category or benefit first, mechanism second.**

### Mechanism phrasing (delivery)

Archcore ships as a CLI and a local stdio MCP server. The phrase **"CLI and local MCP server"** (or **"CLI and local stdio MCP server"** when technical precision matters) may follow the leading phrase in repository descriptions, README sublines, MCP directory listings, and channel bios where space allows.

Do not lead with the mechanism phrase, replace the leading phrase with it, or use it as an H1. A statement that Archcore is an MCP server must name the CLI as the component that serves MCP.

### Channel-specific framing

| Channel | Lead with |
|---------|-----------|
| Website home and pillar pages | Category line as H1 |
| Website product pages | Benefit phrase, then the product definition |
| README (CLI) | `Archcore CLI — Git-Native Context for AI Coding Agents`, then the product definition, then the delivery subline |
| README (Plugin) | `Archcore Plugin — Spec-Driven Development & Context Engineering for AI Coding Agents`, then the command-surface framing |
| Repository description | Category-bearing description from `product/surface-descriptors` |
| Docs | Clarity first — "Archcore is a git-native context layer for AI coding agents", then what to do with it |
| Social | Shortest clear phrase — compact bio from `product/surface-descriptors` |
| Author bio | What you are building — "Building Archcore — git-native context for AI coding agents." |

### Standard copy blocks

**1-line:** Archcore is a git-native context layer for AI coding agents.

**2-line:** Archcore is a git-native context layer for AI coding agents. It ships as a CLI and a local stdio MCP server, so any MCP-compatible agent can read and write your project context through standard tools.

**3-line:** Archcore is a git-native context layer for AI coding agents. It keeps specs, architecture, decisions, rules, and plans in Git, next to the code they describe. The result is the right project context across sessions, tools, and agents.

**Repo description with mechanism:** Git-native context for AI coding agents — CLI and local MCP server.

## Rationale

Consistent sequencing prevents drift across channels and contributors. The split between category-led and benefit-led surfaces exists because the two do different jobs: a `<title>` competes for a query, a README first line answers a reader who already clicked. Forcing one phrase into both roles previously produced titles with no category term and headings that read like keyword strings.

The mechanism clause stays secondary so the leading message is product-focused, not protocol-focused, while still qualifying Archcore for MCP directory listings (mcpservers.org, Glama, Smithery).

## Examples

### Good

- "Archcore is a git-native context layer for AI coding agents."
- "Git-native context for AI coding agents — CLI and local MCP server."
- "Archcore ships as a CLI and a local stdio MCP server, so any MCP-compatible coding agent can read and write your project context through standard tools."
- `<title>Archcore — Spec-Driven Development & Context Engineering</title>` — category-led, because a title's job is discovery.
- README H1 `Archcore CLI — Git-Native Context for AI Coding Agents`, first line "Archcore is a git-native context layer for AI coding agents."

### Bad

- "Archcore is a shared architectural memory for AI coding agents." — retired framing.
- "Archcore is a context engineering platform." — the category term is correct; "platform" is not.
- "Archcore is an MCP server for repo context." — mechanism first, and it omits the CLI.
- "A local stdio MCP server for AI coding agents." — mechanism-first, drops the leading phrase.
- An H1 reading "Git-native context for AI coding agents — CLI and local MCP server" — the mechanism clause belongs below the fold, not in the H1.

## Enforcement

Content review. When editing a README, docs, website copy, a repository description, a manifest description, or any public-facing text, verify that the lead matches the channel table, that the string itself comes from `product/surface-descriptors` where that surface is listed, and that the vocabulary matches `product/messaging-and-voice`.
