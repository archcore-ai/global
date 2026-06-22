---
title: "Messaging Playbook: Hierarchy, Mechanism & Channels"
status: accepted
---

## Rule

The operational playbook for outward-facing Archcore copy — the positioning hierarchy, mechanism phrasing, channel-specific framing, and standard copy blocks. The ecosystem stance, voice, and the preferred/avoid vocabulary are governed by `product/messaging-and-voice`; this playbook *applies* them. Surface-specific docs (e.g. the landing `messaging-alignment` rule) hold each surface's own canonical phrasing and must align to both.

### Primary positioning

1. The primary phrase is **"Git-native context for AI coding agents"** — the default tagline, title suffix, and first descriptor.
2. The expanded explanation is: **"Archcore helps teams turn scattered repo knowledge into structured context that AI coding agents can find, reuse, and follow."**

### Mechanism phrasing (delivery)

Archcore ships as a CLI and a local stdio MCP server. The mechanism phrase **"CLI and local MCP server"** (or **"CLI and local stdio MCP server"** when technical precision matters) may be used as a supporting clause after the primary phrase — in repo descriptions (GitHub, package registries, MCP directories), README sublines, and channel bios where space allows.

Do NOT lead with the mechanism phrase, replace the primary phrase with it, or use it as the H1. The hierarchy stays: **benefit first, mechanism second.**

### Messaging hierarchy

| Order | Role | Phrase |
|-------|------|--------|
| First | Benefit | Git-native context for AI coding agents |
| Second | Mechanism (delivery) | CLI and local MCP server |
| Third | Value explanation | Archcore helps teams turn scattered repo knowledge into structured context that AI coding agents can find, reuse, and follow |

### Channel-specific framing

| Channel | Lead with |
|---------|-----------|
| Website | Benefit first — primary phrase as H1 |
| README | Product + mechanism — "Archcore is a git-native context layer for AI coding agents." Add a subline on the CLI + local MCP server delivery. |
| Repo description (GitHub, registries) | Primary phrase + delivery clause — "Git-native context for AI coding agents — CLI and local MCP server" |
| Docs | Clarity + ease — "Archcore is a git-native way to structure project context for AI coding agents." |
| Social | Shortest clear phrase — primary phrase |
| Author bio | What you are building — "Building Archcore — git-native context for AI coding agents." |

### Mechanism vocabulary

Additions to the preferred set for delivery phrasing: "local MCP server", "local stdio MCP server", "MCP-compatible agent". The full preferred set and the avoid-list live in `product/messaging-and-voice`.

### Standard copy blocks

**Repo description (1-line with mechanism):** Git-native context for AI coding agents — CLI and local MCP server.

**1-line:** Archcore is a git-native context layer for AI coding agents.

**2-line:** Archcore is a git-native context layer for AI coding agents. It ships as a CLI and a local stdio MCP server, so any MCP-compatible agent can read and write your repo context through standard tools.

**3-line:** Archcore is a git-native context layer for AI coding agents. It helps teams structure decisions, rules, plans, and guides inside the repository. The result is stronger project context across sessions, tools, and workflows.

## Rationale

Consistent positioning prevents messaging drift across channels and contributors. The mechanism clause "CLI and local MCP server" is included as an explicit secondary because it explains how Archcore integrates across many agents without a hosted service or bespoke plugins, and prepares the project for submissions to MCP server directories (mcpservers.org, Glama, Smithery). It must remain secondary to keep the leading message product-focused, not protocol-focused.

## Examples

### Good

- "Archcore is a git-native context layer for AI coding agents."
- "Git-native context for AI coding agents — CLI and local MCP server."
- "Archcore ships as a CLI and a local stdio MCP server — any MCP-compatible coding agent can read and write your repo context through standard tools."
- "Structure decisions, rules, plans, and guides in your repo so agents work with stronger project context."

### Bad

- "Archcore is a shared architectural memory for AI coding agents." — uses avoided primary framing
- "Archcore is a context engineering platform." — uses avoided framing
- "Archcore gives your repo a durable architectural memory layer." — uses old positioning
- "Archcore is an MCP server for repo context." — leads with mechanism instead of benefit
- "A local stdio MCP server for AI coding agents." — mechanism-first, drops the primary benefit phrase

## Enforcement

Content review. When editing README, docs, website copy, repo descriptions, or any public-facing text, verify the lead aligns with the hierarchy above and the vocabulary in `product/messaging-and-voice`.
