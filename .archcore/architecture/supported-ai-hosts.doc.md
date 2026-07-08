---
title: "Supported AI Hosts"
status: accepted
tags:
  - "architecture"
  - "product"
---

## Overview

The canonical roster of AI coding hosts (agents/IDEs) that Archcore integrates with — across **both entry points** (the CLI and the plugin). This is the single source of truth for *which* hosts are supported and *at what capability tier*. Per-host wiring details (config paths, manifests, hook formats) live with each tool and must not redefine this list.

Archcore is one product with two entry points (see `architecture/one-product-two-entry-points`). The two entry points reach **different host sets** by design — this document reconciles them.

## Host roster

| Host | ID | CLI tier | Shipped in plugin | Detection marker |
|------|----|----------|-------------------|------------------|
| Claude Code | `claude-code` | Full (hooks + MCP) | Yes | `.claude/` dir |
| Cursor | `cursor` | Full (hooks + MCP) | Yes (MCP user-installed) | `.cursor/` dir |
| Codex CLI | `codex-cli` | MCP-only | Yes | `.codex/` dir |
| Gemini CLI | `gemini-cli` | Full (hooks + MCP) | No | `.gemini/` dir |
| GitHub Copilot | `copilot` | Full (hooks + MCP) | No | `.github/copilot-instructions.md` |
| OpenCode | `opencode` | MCP-only | No | `opencode.json` / `.opencode/` |
| Roo Code | `roo-code` | MCP-only | No | `.roo/` dir |
| Cline | `cline` | Manual (MCP via UI) | No | `.clinerules/` dir |

## CLI integration tiers

- **Full (hooks + MCP)** — Claude Code, Cursor, Gemini CLI, GitHub Copilot. Auto-detected; `archcore init` installs the SessionStart hook and writes MCP config.
- **MCP-only** — OpenCode, Codex CLI, Roo Code. No archcore-compatible lifecycle hook; receive MCP config only.
- **Manual** — Cline. Stores MCP config in VS Code `globalStorage`; the user adds the server via Cline's MCP UI.

Only the `SessionStart` lifecycle event is active across hosts.

## Plugin host coverage

The plugin ships for **three** hosts: **Claude Code, Cursor, Codex CLI**. It rides three open standards — Agent Skills, MCP, and markdown agent definitions — so ~95% of plugin content is host-agnostic; only manifests and hook configs are per-host. Cursor's plugin-MCP is deliberately *not* shipped (cwd handling gap), so Cursor users copy a reference MCP template once.

The plugin set is intentionally narrower than the CLI set: the plugin packages skills/agents/hooks for hosts with a mature plugin surface, while the CLI reaches the long tail of MCP-capable agents directly.

## Industry convergence (context)

The broader market is converging on the same standards the plugin targets — the Agent Skills standard and MCP are adopted by Cursor, Copilot, Codex CLI, Roo Code, Cline, Gemini CLI, Windsurf, JetBrains Junie, OpenHands, and others (plus Amazon Q, Continue.dev, Zed AI for MCP). New hosts therefore tend to be low-cost to add.

## Where the per-host wiring lives

- **CLI** — per-host config paths, hook formats, and the "adding a new agent" recipe: `cli/.archcore/integrations/supported-ai-agents.doc` and `agent-hooks-integration.guide`.
- **Plugin** — shared-core / per-host-adapter layout, marketplace catalogs, stdin normalizer, Cursor-MCP exception: `plugin/.archcore/plugin/multi-host-plugin-architecture.adr`.

Adding or dropping a host updates **this roster first**, then the per-tool wiring docs.
