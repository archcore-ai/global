---
title: "Canonical Narrative: Fixed Strings for Every Surface"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Rule

This document holds the canonical Archcore strings. Voice and vocabulary are governed by `product/messaging-and-voice`; the category decision behind these strings is `product/two-discovery-categories`; the adjacent-term boundaries are `product/adjacent-category-terms`.

1. WHEN an author writes public-facing copy for any Archcore surface, the author MUST reuse a canonical string from this document instead of composing a new one.
2. IF a hard length or format constraint prevents reuse, THEN the author MUST shorten a canonical string and MUST NOT introduce a different category definition for that surface.
3. WHEN one sentence must explain what Archcore is, the author MUST use the product definition.
4. WHEN a surface is SEO-critical or discovery-facing, the author MUST use the category line.
5. The author MUST NOT define Archcore primarily as AI memory, a knowledge base, a documentation tool, a prompt library, RAG, a methodology kit, a one-shot spec-to-code generator, a generic AI assistant, or an agent framework.
6. WHEN a surface names both spec-driven development and context engineering, the author MUST state that specs are one part of context and that context is broader than specs.
7. The author MUST NOT create a new tagline. The canonical taglines are the six listed under Taglines.
8. WHEN an author describes the Archcore CLI, the author MUST frame it as context infrastructure.
9. WHEN an author describes the Archcore Plugin, the author MUST frame it as the command surface and guardrails over the context layer.
10. The author MUST NOT present the CLI and the Plugin as two unrelated products.
11. The author MUST NOT rank the CLI against the Plugin on any surface, per `architecture/one-product-two-entry-points`.
12. WHEN an author writes prose, the author MUST write `git-native`, `spec-driven development`, and `context engineering` in lower case.
13. WHEN an author writes a heading or a title, the author MUST write `Spec-Driven Development` and `Context Engineering` in title case.
14. The author MUST NOT call `.archcore/` "memory".
15. The author MUST NOT state that Archcore is an MCP server without naming the CLI as the component that serves MCP.
16. WHEN an author uses "memory" on a comparison or migration page, the author MUST attribute the term to the alternative being compared and MUST NOT attribute it to Archcore.
17. IF the target surface forbids the em dash in prose, THEN the author MUST use the comma variant of the expanded definition given below.
18. WHEN spec-driven development appears as a discovery category, the author MUST NOT reorder the product's job ranking in `product/jobs-to-be-done` to match it.
19. The author MUST NOT describe Archcore as a harness, and MUST describe it as a component of the harness.
20. WHEN an author names harness engineering, the author MUST state that the host supplies the loop, the tools, and the sandbox.
21. The author MUST NOT present prompt engineering, context engineering, and harness engineering as a progression in which a later term supersedes an earlier one.
22. The author MUST NOT place `harness engineering`, `loop engineering`, or `prompt engineering` in a `<title>`, an H1, or a tagline on any surface other than the page that owns the term.
23. The author MUST NOT describe Archcore as designing or owning the agent loop.
24. The author MUST NOT use `workflow` or `workflows` in positioning copy, and MUST name the concrete capability instead: skills, slash commands, gated tracks, hooks, review, or guardrails.
25. The author MAY use `workflow` in its unrelated technical senses, such as a GitHub Actions workflow or the `task-type` document definition.

### Canonical strings

| Role | String |
|------|--------|
| Category line | Spec-Driven Development & Context Engineering for AI Coding Agents |
| Product definition | Archcore is a git-native context layer for AI coding agents. |
| Expanded definition | Archcore keeps specs, architecture, decisions, rules, and plans in Git — and makes the right project context available to AI coding agents as they work. |
| Expanded definition, comma variant | Archcore keeps specs, architecture, decisions, rules, and plans in Git, and makes the right project context available to AI coding agents as they work. |
| Narrative line | Specs define intent. Context preserves understanding. Agents write the code. |
| Product promise | The agent stops guessing and starts following the system. |
| Problem statement | Stop re-explaining your repo to every AI coding agent. |

### One-liners by length

| Length | String |
|--------|--------|
| Ultra-short | Git-native context for AI coding agents. |
| Short | Spec-driven development and context engineering for AI coding agents. |
| Product definition | Archcore is a git-native context layer for AI coding agents. |
| Medium | Archcore keeps specs, architecture, decisions, rules, and plans in Git and makes the right project context available to AI coding agents. |
| Medium with SDD | Archcore combines spec-driven development with git-native context engineering, keeping specs, architecture, decisions, rules, and plans available to AI coding agents as they work. |
| Technical | Archcore is a git-native project context layer and local MCP infrastructure for AI coding agents, with spec-driven development through the Archcore Plugin. |

### Taglines

| Role | String |
|------|--------|
| Category | Spec-Driven Development & Context Engineering for AI Coding Agents |
| Product | Git-native context for AI coding agents. |
| Marketing | Build with specs. Code with context. |
| Problem | Stop re-explaining your repo to every AI coding agent. |
| Outcome | The agent stops guessing and starts following the system. |
| Narrative | Specs define intent. Context preserves understanding. Agents write the code. |

### Message hierarchy

Each term has one job. They are not interchangeable.

| Concept | Role | Where it leads |
|---------|------|----------------|
| Spec-Driven Development | Acquisition category and practice | Homepage SEO, SDD pillar page, Plugin, articles, comparisons |
| Context Engineering | Primary category and discipline | Homepage SEO, positioning, docs, category articles |
| Git-native | Primary differentiator | Brand copy, CLI, architecture, comparison pages |
| Project context | Plain-language value | Homepage, docs, onboarding, articles |
| AI coding agents | Primary audience | Every surface |
| Context layer | Product definition | The canonical short explanation |
| Project truth | Supporting brand concept | Long-form copy and narrative, not a primary SEO category |
| MCP | Mechanism and search intent | CLI, integration docs, the MCP pillar page |
| Specs, ADRs, rules, plans | Concrete proof | Supporting copy and long-tail SEO |
| Harness engineering | Adjacent term, never a category | Its own `/learn/` page, plus body copy on the context-engineering section |

### Adjacent terms

Governed by `product/adjacent-category-terms`. These carry search intent but do not move the positioning.

| Term | Archcore's relation | Where it may appear |
|------|---------------------|---------------------|
| Harness engineering | Archcore is the project-specific half of the harness: the guides, and the criteria its sensors check against. The host supplies the loop, the tools, the permissions, and the sandbox. | The `/learn/` page that owns it, and body copy elsewhere |
| Loop engineering | Archcore does not design the loop. It is what each turn of the loop reads before acting and writes back after. | Bounded coverage inside the harness page only |
| Prompt engineering | A different unit of work: one turn, not the system. | Comparison content only |

The canonical framing is **nesting, not progression**. A harness for a coding agent is a specific form of context engineering; the three terms describe different scopes, and none supersedes another.

### Brand architecture

| Entity | Role | Canonical descriptor |
|--------|------|----------------------|
| Archcore | Product and umbrella brand | Git-native context for AI coding agents. |
| Archcore CLI | Context infrastructure | Git-native project context and MCP infrastructure for AI coding agents. |
| Archcore Plugin | Command surface and guardrails | Spec-driven development and context engineering inside your coding agent. |

Mental model to repeat verbatim: **CLI = context infrastructure. Plugin = the command surface and guardrails. Archcore = one product system.**

### Terminology style

Use: `git-native` in prose · `Git` for the technology · `AI coding agent` rather than `AI agent` when category clarity matters · `Archcore CLI` · `Archcore Plugin` · `project context` in user-facing explanation · `harness engineering` in lower case in prose.

Do not use: `spec driven` without the hyphen · `Git native` · `AI Coding Assistant` as the primary category · `memory` for `.archcore/` · `harness` as a bare noun for Archcore.

## Rationale

Surfaces drift because each one re-derives its own phrasing under its own constraints. Fixing the strings, rather than the intent behind them, is the only version of this rule that a reviewer can check mechanically.

Clause 5 exists because each listed category has an established leader whose definition the reader already holds. Adopting one of those definitions inherits its expectations, and Archcore then fails them.

Clause 18 exists because a discovery category and a product scenario are different things. Spec-driven development brings readers in; repo alignment at the moment of coding is what they stay for. `product/jobs-to-be-done` ranks the jobs, and a category decision does not outrank it.

Clauses 19 to 23 exist because harness engineering is the adjacent term most likely to be adopted carelessly. Calling Archcore a harness overclaims (the host already ships one), collides with Harness.io on the bare query, and lands Archcore in the agent-framework category that clause 5 rules out. Clause 21 guards the specific error of repeating the vendor-blog progression in which context engineering reads as superseded, which the canonical source contradicts.

Clause 24 exists because "workflow" has become a contested word in the AI coding-assistant market: it is claimed by orchestration products, automation builders, and agent frameworks at once, so it now signals a category Archcore does not occupy rather than describing anything. Every use of it in Archcore copy had a concrete replacement available, which is the test the clause encodes. The word arrived through the source messaging document and was retired on 2026-08-10.

Clause 17 exists because the landing site bans the em dash in shipping prose while the canonical expanded definition contains one. The comma variant carries the identical claim.

## Examples

**Good**

- `<title>Archcore — Spec-Driven Development & Context Engineering</title>`
- "Archcore is a git-native context layer for AI coding agents. It keeps specs, architecture, decisions, rules, and plans with your code, then gives agents the context that applies to the work in front of them."
- "A spec is one part of context, not the whole context."
- "Memory remembers what happened in previous sessions. Archcore stores what the project says is true."
- "CLI = context infrastructure. Plugin = the command surface and guardrails."
- "Your agent ships the loop, the tools, and the sandbox. Archcore holds the half no vendor can ship for you: what your project decided, requires, and forbids."

**Bad**

- "Archcore — repo memory for AI coding agents" — memory as positioning, retired by `product/two-discovery-categories`.
- "Archcore is a context engineering platform." — "platform" inflates a context layer into a category the product does not occupy.
- "Archcore is an MCP server for repo context." — mechanism first, and it omits the CLI as the component that serves MCP.
- "Archcore Plugin (recommended)" — ranking language between peers.
- "Archcore gives your agent memory of your repo." — memory attributed to Archcore.
- "Archcore is a harness for AI coding agents." — the host is the harness; Archcore is a component of it.
- "The field moved from prompt engineering to context engineering to harness engineering." — a progression the canonical source does not support.

## Enforcement

- Every PR that changes a `<title>`, a meta description, an H1, a hero subhead, a repository description, a plugin manifest description, or a social bio checks the string against the tables above.
- `product/surface-descriptors` holds the resolved string for each named surface. Where a surface is listed there, that entry is the one to copy.
- A surface that must deviate records the deviation and its constraint in its own repository, and links back to this rule.
- Landing keeps its per-surface enforcement in `landing/.archcore/messaging-alignment.rule.md`, which must align to this document and must not restate it.
