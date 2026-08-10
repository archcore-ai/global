---
title: "Messaging, Voice & Positioning"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Rule

All public-facing copy follows one positioning and one voice. This is the ecosystem source of truth; surface-specific messaging must not contradict it.

### Positioning
- Archcore is **git-native context for AI coding agents** — infrastructure, not magic, not a docs tool, not a generic memory / RAG layer.
- **One product, two entry points** (Plugin + CLI). Never two products; the CLI is not a fallback.
- The two entry points are **peers, chosen by the host the reader runs** — never ranked, never labelled "(recommended)". See `architecture/one-product-two-entry-points`.
- Core promise: **"The agent stops guessing and starts following the system."**

### Voice
Direct, technical, confident, minimal, calm, specific. Archcore should read like serious developer infrastructure, not a generic AI SaaS landing page.

### Preferred vocabulary
repository · structured context · machine-readable · architecture · rules · decisions · workflows · MCP · typed documents · relation graph · lifecycle hooks · guardrails · coding agents · durable context · source of truth · repo-aware · "decisions, rules, plans, and guides" · entry point · runtime · engine · tracks.

### Avoid
magic · revolutionary · seamless · effortless · unlock · supercharge · game-changing · "10x developer" · "copilot for X" · "shared memory" / "shared architectural memory" / "system context platform" / "context engineering platform" (outdated framing) · vague productivity claims · enterprise jargon · ranking language between the two entry points.

## Rationale

The product's credibility rests on sounding precise and infrastructural. Consistent vocabulary across every surface keeps the story coherent and prevents drift back to vague "AI memory" framing. "Memory" implies persistence semantics that don't match the product; "context" names the value — structured knowledge that agents consume.

The no-ranking clause exists because a recommendation the reader is ineligible for is worse than no recommendation: it tells a Gemini CLI or OpenCode user that the path available to them is the lesser one.

## Examples

**Good**
- "Stop re-explaining your repo to every AI agent."
- "Archcore turns your repository into structured, machine-readable context — so agents follow your architecture, rules, and decisions instead of guessing."
- "Instruction files are flat memory. Archcore is structured system context."
- "Same product, two entry points. Pick by the agent you run, not by a recommendation."

**Bad**
- "Supercharge your workflow with AI magic."
- "The revolutionary shared-memory platform for autonomous coding."
- Framing the CLI as a fallback for users who can't run the Plugin.
- "Plugin (recommended)" — ranking language between peers.

## Enforcement

Public surfaces conform to this whenever hero copy, CTAs, or positioning change. Each surface keeps its own canonical phrasing and CTAs; this document governs the ecosystem-wide stance they all align to. The entry-point framing is fixed by `architecture/one-product-two-entry-points`. The landing site's `messaging-alignment` rule holds the per-surface copy layers and the enforcement checklist.

## Open question

Both public surfaces now lead their `<title>` with the category term "repo memory" (`Archcore — repo memory for AI coding agents`), under an SEO decision recorded in `landing/.archcore/landing/home-title-category-keyword.adr`, while this rule's avoid-list discourages memory framing. The exception is currently undeclared. It needs either a sanctioned carve-out — category term in `<title>` and search surfaces only, never in H1, hero, or body copy — or a rollback. [DECISION REQUIRED]
