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
| Claude Code | `claude-code` | Full (hooks + MCP) | Yes (with MCP) | `.claude/` dir |
| Cursor | `cursor` | Full (hooks + MCP) | Yes (MCP user-installed) | `.cursor/` dir |
| Codex CLI | `codex-cli` | Full (hooks + MCP) | Yes (with MCP) | `.codex/` dir |
| GitHub Copilot | `copilot` | Full (hooks + MCP) | Yes (MCP user-installed) | `.github/copilot-instructions.md` |
| Gemini CLI | `gemini-cli` | Full (hooks + MCP) | No | `.gemini/` dir |
| OpenCode | `opencode` | Hooks via host plugin + MCP | Adapter accepted, not shipped | `opencode.json` / `.opencode/` |
| Roo Code | `roo-code` | MCP-only | No | `.roo/` dir |
| Cline | `cline` | Manual (MCP via UI) | No | `.clinerules/` dir |

## CLI integration tiers

- **Full (hooks + MCP)** — Claude Code, Cursor, Codex CLI, GitHub Copilot, Gemini CLI. Auto-detected; `archcore init` installs the lifecycle hooks and writes MCP config.
- **Hooks via host plugin** — OpenCode. The host loads hooks as plugin code, so no declarative hook config exists to write. The CLI ships `archcore hooks opencode <event>` leaves and the Archcore OpenCode adapter calls them; the events are the same three.
- **MCP-only** — Roo Code. Supports `onSave` hooks only, which do not serve lifecycle events.
- **Manual** — Cline. Stores MCP config in VS Code `globalStorage`; the user adds the server via Cline's MCP UI.

Three lifecycle events are active, in each host's own spelling: `SessionStart`, `PreToolUse`, `PostToolUse`. The `Stop` and `UserPromptSubmit` families stay unsupported. The event model and the guardrails carried on those events live in `architecture/lifecycle-hooks`.

## Known host limitations

- **Codex CLI** — hooks sit behind an experimental feature flag that is off by default, do not run on Windows, and load project-local hooks only when the `.codex/` layer is trusted.
- **GitHub Copilot** — the pre-write event carries only a permission decision, so the write guard runs there but code-alignment injection does not. Copilot also reads `.claude/settings.json`, so a repository wired for both hosts can run a hook twice.
- **Gemini CLI** — [assumption] the tool-event wiring follows the published reference and is not confirmed against a running host; its event names, tool names, and timeout unit differ from every other host.

## Plugin host coverage

The plugin ships for **four** hosts: **Claude Code, Cursor, Codex CLI, GitHub Copilot**. It rides three open standards — Agent Skills, MCP, and markdown agent definitions — so ~95% of plugin content is host-agnostic; only manifests and hook configs are per-host.

The plugin ships MCP config to **two** of the four: Claude Code and Codex CLI. Cursor and GitHub Copilot are excluded for the same underlying reason — each launches a plugin's MCP child outside the user's project directory — so their users install the MCP server once from a reference template. A Copilot user therefore always has two install steps; a surface that shows only the plugin install leaves them without document tools.

An OpenCode adapter is an accepted decision (a TypeScript package bridging to the shared hook scripts) and is not yet shipped; adding it makes five.

The plugin set is intentionally narrower than the CLI set: the plugin packages skills/agents/hooks for hosts with a mature plugin surface, while the CLI reaches the long tail of MCP-capable agents directly.

## Industry convergence (context)

The broader market is converging on the same standards the plugin targets — the Agent Skills standard and MCP are adopted by Cursor, Copilot, Codex CLI, Roo Code, Cline, Gemini CLI, Windsurf, JetBrains Junie, OpenHands, and others (plus Amazon Q, Continue.dev, Zed AI for MCP). New hosts therefore tend to be low-cost to add.

## Where the per-host wiring lives

- **CLI** — per-host config paths, hook formats, and the "adding a new agent" recipe: `cli/.archcore/integrations/supported-ai-agents.doc` and `agent-hooks-integration.guide`.
- **Plugin** — shared-core / per-host-adapter layout, marketplace catalogs, stdin normalizer, and the Cursor and Copilot MCP exceptions: `plugin/.archcore/plugin/multi-host-plugin-architecture.adr`.

## Changing the roster

A host tier change fails silently on every public surface — nothing in any build knows which hosts are supported. Adding, dropping, or re-tiering a host updates, in one change: **this roster first**, then the per-tool wiring docs, the docs site host matrices (plugin and CLI pages), the landing host and agent sections, and the repository descriptions. A surface may summarize the roster; it must not contradict it.
