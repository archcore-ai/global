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
- Core promise: **"The agent stops guessing and starts following the system."**

### Voice
Direct, technical, confident, minimal, calm, specific. Archcore should read like serious developer infrastructure, not a generic AI SaaS landing page.

### Preferred vocabulary
repository · structured context · machine-readable · architecture · rules · decisions · workflows · MCP · typed documents · relation graph · session hooks · coding agents · durable context · source of truth · repo-aware · "decisions, rules, plans, and guides" · entry point · runtime · core.

### Avoid
magic · revolutionary · seamless · effortless · unlock · supercharge · game-changing · "10x developer" · "copilot for X" · "shared memory" / "shared architectural memory" / "system context platform" / "context engineering platform" (outdated framing) · vague productivity claims · enterprise jargon.

## Rationale

The product's credibility rests on sounding precise and infrastructural. Consistent vocabulary across every surface keeps the story coherent and prevents drift back to vague "AI memory" framing. "Memory" implies persistence semantics that don't match the product; "context" names the value — structured knowledge that agents consume.

## Examples

**Good**
- "Stop re-explaining your repo to every AI agent."
- "Archcore turns your repository into structured, machine-readable context — so agents follow your architecture, rules, and decisions instead of guessing."
- "Instruction files are flat memory. Archcore is structured system context."

**Bad**
- "Supercharge your workflow with AI magic."
- "The revolutionary shared-memory platform for autonomous coding."
- Framing the CLI as a fallback for users who can't run the Plugin.

## Enforcement

Public surfaces conform to this whenever hero copy, CTAs, or positioning change. Each surface keeps its own canonical phrasing and CTAs; this document governs the ecosystem-wide stance they all align to. The entry-point framing is fixed by `architecture/one-product-two-entry-points`.