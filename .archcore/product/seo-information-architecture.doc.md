---
title: "SEO Information Architecture: Pillars, Ownership, and Page Rules"
status: accepted
tags:
  - "messaging"
  - "product"
  - "web"
---

## Overview

Which page owns which query, how a new public page is titled and described, and what the editorial program builds around the two discovery categories in `product/two-discovery-categories`. Adjacent terms are bounded by `product/adjacent-category-terms`. Copy strings come from `product/canonical-narrative` and `product/surface-descriptors`.

Landing and docs implement this. Each keeps its own build-level rules; neither restates the ownership table.

## Content

### Page-level placement rule

**Root pillar pages are reserved for the two primary discovery categories and the product's own concepts.** Adjacent and definitional terms live under `/learn/`. This keeps one owner per query while the pillar system is built, and it stops an adjacent term from reading as a third category just because it sits at the root.

### Keyword ownership

No two pages compete for the same primary query.

| Query cluster | Canonical owner |
|---------------|-----------------|
| spec-driven development | `/spec-driven-development/` |
| context engineering for AI coding | `/context-engineering/` |
| project context for AI agents | `/project-context/` |
| git-native context | `/git-native-context/` |
| MCP coding agent context | `/mcp/` |
| Claude Code context | `/claude-code/` |
| Cursor context | `/cursor/` |
| Codex context | `/codex/` |
| Copilot context | `/github-copilot/` |
| AGENTS.md alternative and comparison | `/agents-md/` |
| CLAUDE.md alternative and comparison | `/claude-md/` |
| harness engineering, agent harness | `/learn/harness-engineering/` |
| repo memory (term) | `/learn/repo-memory/` |

The homepage targets the combined brand and category query: Archcore + Spec-Driven Development + Context Engineering.

**Not pursued as owned queries:** the bare term *harness* (Harness.io, the CI/CD company, owns it, the same way a steel manufacturer owns *archcore*), *loop engineering* (IBM holds the definitional query and Archcore does not design the loop), and *prompt engineering* (an occupied head describing a different unit of work). The first two are covered inside `/learn/harness-engineering/`; the third appears in comparison content.

### Pillar pages

Durable, product-linked reference pages. Not thin marketing pages.

| URL | `<title>` | H1 |
|-----|-----------|-----|
| `/context-engineering/` | Context Engineering for AI Coding Agents — Archcore | Context Engineering for AI Coding Agents |
| `/spec-driven-development/` | Spec-Driven Development for AI Coding Agents — Archcore | Spec-Driven Development for AI Coding Agents |
| `/project-context/` | Project Context for AI Coding Agents — Archcore | Project Context for AI Coding Agents |
| `/git-native-context/` | Git-Native Context Engineering — Archcore | Why Project Context Belongs in Git |
| `/mcp/` | MCP Server for AI Coding Agent Context — Archcore | MCP for AI Coding Agent Context |
| `/claude-code/` | Context Engineering for Claude Code — Archcore | Persistent Project Context for Claude Code |
| `/cursor/` | Spec-Driven Development & Context for Cursor — Archcore | Project Context for Cursor |
| `/codex/` | Project Context for Codex CLI — Archcore | Context Engineering for Codex CLI |
| `/github-copilot/` | Project Context for GitHub Copilot — Archcore | Context Engineering for GitHub Copilot |
| `/gemini-cli/` | Project Context for Gemini CLI — Archcore | Context Engineering for Gemini CLI |
| `/agents-md/` | AGENTS.md and Structured Project Context — Archcore | Beyond AGENTS.md |
| `/claude-md/` | CLAUDE.md and Structured Project Context — Archcore | Beyond CLAUDE.md |

Pillar meta descriptions:

- `/context-engineering/` — Learn how context engineering gives AI coding agents structured, relevant project knowledge: specs, architecture, decisions, rules, plans, and more.
- `/spec-driven-development/` — Use spec-driven development with AI coding agents while keeping specs connected to architecture, decisions, rules, plans, and implementation context.
- `/project-context/` — Give AI coding agents persistent project context that lives in Git: specs, architecture decisions, rules, plans, and project knowledge.
- `/git-native-context/` — Keep AI coding agent context reviewable, portable, and versioned with code. Learn why specs, decisions, rules, and plans belong in Git.
- `/mcp/` — Expose structured project context to AI coding agents through MCP, including specs, ADRs, rules, plans, and project knowledge.

`/context-engineering/` links to `/learn/harness-engineering/` and states the nesting: a harness for a coding agent is a specific form of context engineering.

### Integration page formula

This formula covers host pages at their existing root URLs. Integration recipe pages use the separate catalog ownership below.

Every host gets its own page.

- Title pattern: `Context Engineering for {Agent} — Archcore`. Use `Spec-Driven Development with {Agent} — Archcore` where that host's search intent supports it. Titles are not identical across integration pages.
- H1 pattern: `Persistent Project Context for {Agent}`.
- First paragraph: `Archcore gives {Agent} structured project context from Git — including specs, architecture decisions, rules, plans, and project knowledge — so the agent can follow how your repository is actually built.`
- Required sections: What Archcore adds to {Agent} · Installation · Project context · Spec-driven development · Automatic context and hooks · MCP · Worked examples · Comparison with the host's native instruction or memory features · FAQ.

The host set stated on an integration page follows the shipped support matrix, not this document. Landing holds one source for that matrix; docs and repository taglines follow it.

### Integration recipe catalog

Accepted on 2026-09-08; planned implementation. The catalog lives at archcore.ai/integrations/ in landing's Astro content build. It serves discovery and evaluation of Archcore + selected tools. Short setup instructions stay on recipe pages; docs.archcore.ai carries additional setup, update, removal, and troubleshooting guidance.

| Query cluster or reader task | Selected owner |
|---|---|
| Find an Archcore integration for an existing tool setup | archcore.ai/integrations/ |
| Use Superpowers with Archcore project context | archcore.ai/integrations/superpowers/ |
| Configure Archcore in a supported AI host | Existing root host pages and their linked operational docs |
| Diagnose or maintain an installed recipe | Distinct operational docs where the catalog's short instructions do not cover the task |

Archcore + Superpowers is the first pilot. Other combinations receive pages when they have distinct guidance; these entries do not establish current compatibility or a publication date.

Recipe pages explain the problem, each tool's contribution, supported entry points, artifact ownership, configuration effect, and exact verification scope. They link to one versioned source for installable instructions.

The catalog targets users across harnesses. A named host guide is a setup shortcut; tested host/model environments describe evidence coverage. Required capabilities and a connection path for an unrecognized harness belong on the recipe page.

Existing host pages keep their query ownership. A docs page and a catalog page can each have a canonical URL when they answer different tasks. Independently authored copies of the same recipe instructions and generated tool × host × version pages are outside the selected approach. Host-specific instruction exports can derive from the same versioned source.

The catalog choice rests on the product journey and existing build, not on an established ranking advantage over the docs subdomain.

### Title and description rules

Titles:

- Every indexable page has a unique `<title>`.
- The title leads with the page's actual search intent.
- Branding stays concise, usually `… — Archcore`.
- The homepage tagline is not appended to every page.
- The title avoids keyword repetition.
- The visible H1 is consistent with the title's topic.
- Both category phrases appear together only where both are genuinely central.
- An adjacent term appears in a `<title>` or H1 only on the page that owns it.

Meta descriptions:

- Every important page has a unique description.
- The description describes the page, not a keyword list.
- The description names concrete entities: specs, architecture, decisions, rules, plans, MCP, or the relevant agent.
- The description optimizes for relevance and click intent rather than a character count.

Page copy on a strategic SEO page: primary term in `<title>`, in the H1, and naturally in the first paragraph; a concrete Archcore product connection near the top; internal links to related pillar pages; examples and technical depth; no thin doorway pages.

### Internal linking

Use descriptive anchors: `context engineering for AI coding agents`, `spec-driven development`, `project context for Claude Code`, `MCP for coding agent context`, `git-native project context`, `architecture decisions for coding agents`, `harness engineering, explained`.

Avoid repeated generic anchors: `learn more`, `click here`, `docs`, `read this`.

### Structured data

- Homepage uses `Organization` for Archcore with consistent `name`, `url`, `logo`, and relevant `sameAs` profiles. Organization identity stays consistent across the website and external profiles.
- Product and installation pages may use `SoftwareApplication` where the page genuinely describes the installable software and the markup satisfies the applicable requirements.
- Structured data is never added to inject keywords. Markup represents visible page content.

### Editorial clusters

Content builds topical authority around the two categories, then connects them to agent-specific and problem-specific intent.

**Context engineering.** What Is Context Engineering for AI Coding Agents? · Context Engineering vs Prompt Engineering for Coding Agents · How to Give AI Coding Agents Persistent Project Context · What Should Be in an AI Coding Agent's Project Context? · Context Windows vs Context Engineering · Why AI Coding Agents Need Architecture Context · How to Share Context Across Multiple AI Coding Agents · Git-Native Context Engineering: Why Context Belongs in Your Repository.

**Spec-driven development.** What Is Spec-Driven Development? · Spec-Driven Development with AI Coding Agents · Spec-Driven Development vs Context Engineering · How to Use Spec-Driven Development in an Existing Codebase · From Product Requirements to Implementation Plans for AI Coding Agents · How to Keep Specs from Becoming Stale · Specs as Living Context, Not One-Time Handoffs · Spec-Driven Development with Claude Code / Cursor / Codex.

**Harness engineering (adjacent).** What Is Harness Engineering? (owner page) · Guides and Sensors: A Checklist for Your Coding Agent Harness · What Your Coding Agent Cannot Ship for You · Harness Engineering vs Context Engineering: Why It Is Nesting, Not a Progression.

**Project context.** Project Context for AI Coding Agents · AI Agent Memory vs Project Context · CLAUDE.md vs Structured Project Context · AGENTS.md vs Structured Project Context · How to Make AI Coding Agents Follow Your Architecture · How to Make AI Coding Agents Follow Team Coding Rules · Architecture Decision Records for AI Coding Agents · Persistent Context Across Claude Code, Cursor, Codex, and Copilot.

**MCP.** MCP for AI Coding Agents: Project Context as Tools · How to Build a Local MCP Context Layer for a Repository · MCP vs Instruction Files for Coding Agents · Using MCP to Share Project Knowledge Across Coding Agents.

### The editorial rule that connects the two categories

Repeat this distinction across the program:

> Spec-driven development defines intent. Context engineering supplies the broader project understanding required to execute that intent correctly.

A spec is one part of context, not the whole context. Typical context also includes architecture, prior decisions, constraints, team rules, implementation plans, conventions, operational knowledge, and previous incidents or patterns.

This distinction is what keeps Archcore out of the spec-generator category while the SDD acquisition path stays open.

## Examples

**Good** — `/cursor/` titled `Spec-Driven Development & Context for Cursor — Archcore`, distinct from `/claude-code/` titled `Context Engineering for Claude Code — Archcore`.

**Good** — an article on agent memory that ranks for the memory query and closes with the canonical definition of project context.

**Good** — the homepage naming harness engineering once, in the body of the context-engineering section, linking to the page that owns the term.

**Bad** — `/context-engineering/` and a blog post both targeting "context engineering for AI coding agents" as the primary term.

**Bad** — appending `— Spec-Driven Development & Context Engineering for AI Coding Agents` to every page title.

**Bad** — a pillar page with three paragraphs and a CTA. Pillar pages carry examples and technical depth or they do not ship.

**Bad** — a root `/harness-engineering/` page. The root is for the two primary categories; an adjacent term at the root reads as a third one.
