---
title: "One Product, Two Entry Points (Plugin and CLI)"
status: accepted
tags:
  - "architecture"
  - "product"
---

## Context

Archcore reaches users in two shapes — the **Plugin** (the command surface and gated tracks over the engine) and the **CLI** (the engine itself: context store, MCP server, hooks, guardrails, scripting). Public surfaces repeatedly face the question of how to frame them relative to each other, and the wrong framing fragments the story.

The original framing named the Plugin the recommended path. That proved wrong in practice for one reason: a user cannot act on a recommendation they are ineligible for. The Plugin runs on four hosts; the CLI reaches all eight. A visitor running Gemini CLI who is told to "start with the Plugin" has been given advice they cannot take, and a recommendation label makes the CLI read as the consolation prize it is not.

The replacement framing — two peer entry points, chosen by host — then failed at the other end. A surface that offers two peers still asks the reader to choose, and by mid-2026 the choice was no longer real: `archcore init` installs the plugin on every host that supports it, and the plugin has never fetched the CLI. A tabbed install block therefore priced a decision the product had already made, and one of its two tabs shipped an incomplete path. The owner reaffirmed the single-product framing on 2026-09-09, which retires both the equal-entry-points wording and the permission to emphasize the plugin as the more polished experience. Recorded at the time in the landing repository's `messaging-alignment` rule; this record is where the stance belongs.

## Decision

Treat the Plugin and CLI as **components of one product** — never as two products, never as primary-vs-fallback, never as recommended-vs-alternative, and no longer as two peers the reader picks between.

- Both reach the same context and the same MCP tools.
- **No surface asks the reader to choose between the plugin and the CLI, and no surface compares them side by side.** A comparison is a choice with extra steps.
- **One install path.** Every install surface presents the platform install script followed by `archcore init`. A tab pair in an install block may select the reader's platform, which is a fact about their machine, never the product component. Install responsibility across the two: `architecture/install-responsibility`.
- **No "(recommended)" labels, and no ranking language** on any surface. The permission to call the plugin the most polished experience is withdrawn: it reads as a ranking on the one surface that stopped distinguishing the two.
- The capability difference stays as prose, not as a choice: the command surface, skills, and guardrails run inside the plugin hosts, and every other MCP-aware agent reaches the same context over MCP and session hooks.
- Entry-point-specific pages remain, and they own the split. A page dedicated to one component describes that component; a shared surface does not restate the split.
- Mental model: **CLI = the engine, Plugin = the runtime over it** (`architecture/engine-runtime-boundary`).

## Alternatives

- **Two products** — fragments the narrative, doubles positioning work, confuses entry points.
- **CLI as fallback** — wrongly implies the CLI is lesser; it is the engine the Plugin runs on.
- **Plugin as the recommended path** — the original framing, retired on 2026-07-06. It routes users by our preference rather than by their eligibility, and it mislabels the CLI for the majority of hosts.
- **Two peer entry points chosen by host** — the framing from 2026-07-06, retired on 2026-09-09. It removed the ranking and kept the choice, and the choice had stopped existing: one command installs both, and the plugin path alone leaves a reader without the engine behind it.
- **Keep the comparison and fix only its accuracy** — rejected. Both branches would open with the same first command, so the accurate version of the comparison compares nothing.

## Consequences

- All public surfaces use one narrative for one product with two named components.
- Install CTAs carry one path. A surface that must offer a second install step offers it as a link, not as a branch.
- The host roster still governs where the plugin exists — `architecture/supported-ai-hosts` — and a component page still states its own scope. What no surface does is turn that scope into a question for the reader.
- Any change to the entry-point story is reflected across all public surfaces together.
- This stance governs the ecosystem; surface-specific messaging must align to it (`product/messaging-and-voice`, `product/canonical-narrative`). The landing site's `messaging-alignment` rule holds the per-surface enforcement, including which copy layers must change together.
