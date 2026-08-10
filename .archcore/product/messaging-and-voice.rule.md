---
title: "Messaging, Voice & Positioning"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Rule

All public-facing copy follows one positioning and one voice. This is the ecosystem source of truth for **stance and voice**; the fixed strings live in `product/canonical-narrative`, and per-surface resolved copy lives in `product/surface-descriptors`. Surface-specific messaging must not contradict any of the three.

### Positioning
- Archcore is **a git-native context layer for AI coding agents** — infrastructure, not magic, not a docs tool, not a generic memory or RAG layer.
- Archcore's two discovery categories are **Spec-Driven Development** and **Context Engineering** (`product/two-discovery-categories`). The product definition stays narrower than either category.
- **Specs are one part of context. Context is broader than specs.** Any surface that uses both category terms teaches this.
- **One product, two entry points** (Plugin + CLI). Never two products; the CLI is not a fallback.
- The two entry points are **peers, chosen by the host the reader runs** — never ranked, never labelled "(recommended)". See `architecture/one-product-two-entry-points`.
- Core promise: **"The agent stops guessing and starts following the system."**

### Voice
Direct, technical, confident, minimal, calm, specific. Archcore should read like serious developer infrastructure, not a generic AI SaaS landing page.

### Primary vocabulary
AI coding agents · spec-driven development · context engineering · project context · git-native · specs · architecture · architecture decisions / ADRs · rules · plans · project knowledge · MCP · coding agents · typed documents · relation graph · lifecycle hooks · guardrails · durable context · source of truth · repo-aware · entry point · runtime · engine · tracks · skills · slash commands · command surface.

### Secondary vocabulary
Use naturally for semantic coverage, never as the primary category: AI coding assistants · coding assistants · agentic coding · persistent context · repo context · repository context · coding agent memory · software specifications · requirements · engineering knowledge · harness engineering · guides and sensors · agent harness.

The harness terms carry a hard boundary: Archcore is a **component** of the harness, never a harness. See `product/adjacent-category-terms` and clauses 19 to 23 of `product/canonical-narrative`.

### Avoid
magic · revolutionary · seamless · effortless · unlock · supercharge · game-changing · "10x developer" · "copilot for X" · "shared memory" / "shared architectural memory" / "repo memory" as positioning · "platform" applied to Archcore ("context engineering platform", "system context platform") · "Archcore is a harness" · the "prompt engineering → context engineering → harness engineering" progression · **"workflow" / "workflows"** in positioning copy · vague productivity claims · enterprise jargon · ranking language between the two entry points.

"Context engineering" itself is **not** avoided. It is a primary category term. The avoided shape is *platform*, which inflates a context layer into a category the product does not occupy.

"Memory" is avoided as positioning on every surface, including `<title>`. It stays legal on comparison and migration pages, attributed to the alternative being compared.

**"Workflow" is banned in positioning copy, retired 2026-08-10.** The word is contested in the AI coding-assistant market, claimed simultaneously by orchestration products, automation builders, and agent frameworks, so it places Archcore in a category it does not occupy while describing nothing. Name the concrete capability: skills, slash commands, gated tracks, hooks, review, guardrails. The unrelated technical senses stay legal: a GitHub Actions workflow, and the `task-type` document definition.

## Rationale

The product's credibility rests on sounding precise and infrastructural. Consistent vocabulary across every surface keeps the story coherent. "Memory" implies persistence semantics that do not match the product; "context" names the value — structured knowledge that agents consume.

The category terms and the product definition do different work. The categories are how a reader finds Archcore; the definition is what they are told once they arrive. Collapsing the two produces either an unfindable page or an overclaiming one.

The "workflow" ban is a vocabulary decision, not a positioning one: nothing about what the Plugin does changed, only the word used for it. Every occurrence had a concrete replacement, which is why the ban costs no meaning.

Adjacent terms are admitted to the secondary set rather than the primary one because they carry search intent without describing what Archcore is. The progression framing is on the avoid-list specifically: it is repeated widely in vendor content and contradicted by the source it cites, and adopting it would retire Archcore's own category on someone else's say-so.

The no-ranking clause exists because a recommendation the reader is ineligible for is worse than no recommendation: it tells a Gemini CLI or OpenCode user that the path available to them is the lesser one.

## Examples

**Good**
- "Stop re-explaining your repo to every AI coding agent."
- "Archcore is a git-native context layer for AI coding agents. It keeps specs, architecture, decisions, rules, and plans with your code, then gives agents the context that applies to the work in front of them."
- "Instruction files are useful entry points. Archcore adds typed documents, relations, lifecycle, selective retrieval, and cross-agent portability."
- "Same product, two entry points. Pick by the agent you run, not by a recommendation."
- "A spec is one part of context, not the whole context."
- "Your agent ships the loop, the tools, and the sandbox. Archcore holds the half no vendor can ship for you."

**Bad**
- "Supercharge your workflow with AI magic."
- "The revolutionary shared-memory platform for autonomous coding."
- "Archcore — repo memory for AI coding agents" — memory as positioning, retired 2026-08-10.
- "Archcore is a context engineering platform." — the category term is fine; "platform" is not.
- "Archcore is the harness for your coding agent." — the host is the harness.
- "Prompt engineering gave way to context engineering, which gave way to harness engineering." — a progression the canonical source does not support.
- Framing the CLI as a fallback for users who can't run the Plugin.
- "Plugin (recommended)" — ranking language between peers.

## Enforcement

Public surfaces conform to this whenever hero copy, CTAs, or positioning change. Each surface keeps its own canonical phrasing and CTAs; this document governs the ecosystem-wide stance they all align to. The fixed strings are enforced by `product/canonical-narrative`. The entry-point framing is fixed by `architecture/one-product-two-entry-points`. The landing site's `messaging-alignment` rule holds the per-surface copy layers and the enforcement checklist.

The former open question about "repo memory" in `<title>` is closed. `product/two-discovery-categories` selected rollback, not a carve-out.
