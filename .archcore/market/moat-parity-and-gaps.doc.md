---
title: "Moat, Parity, and Gaps Against the First Line"
status: accepted
tags:
  - "market"
  - "messaging"
  - "product"
---

## Overview

Archcore's capabilities scored against the nine closest competitors from
`market/competitive-landscape`. The purpose is to separate three things that positioning
copy tends to blur: what only Archcore does, what every serious competitor also does, and
what competitors do that Archcore does not.

Verified 2026-08-12. A cell reads `?` when no public source stated the answer — an unknown is
recorded as unknown, never as an absence.

Legend: `+` present · `~` partial · `−` absent · `?` unverified.

## The matrix

| Capability | Archcore | Kiro | OpenSpec | Spec Kitty | ByteRover | PROJECTMEM | Sprintra | Tessl | Repowise | Spec Kit |
|---|---|---|---|---|---|---|---|---|---|---|
| Plain files in the repo | + | + | + | + | + | + | ~ | + | − | + |
| Versioned in Git, reviewed in PRs | + | + | + | + | + | + | ~ | + | − | + |
| Typed document set | + | ~ | ~ | ~ | ~ | + | ~ | ~ | ~ | ~ |
| Explicit relation graph | + | − | − | ~ | + | − | ? | ? | + | − |
| Status lifecycle on documents | + | − | + | + | + | − | ? | ? | − | − |
| Selective context, not whole-corpus | + | + | + | + | + | + | + | + | + | ~ |
| Host-agnostic, one setup per repo | + | − | + | + | + | + | + | + | + | + |
| MCP surface | + | + | ~ | ~ | + | + | + | + | + | − |
| Lifecycle hooks / guardrails | + | + | − | + | ~ | + | − | ~ | − | − |
| Explicit intent, not inferred from code | + | + | + | + | + | + | + | + | ~ | + |
| Shared org-wide sources | + | − | − | − | ? | − | ~ | + | − | − |
| Local-first, no external service | + | − | + | + | + | + | + | − | ~ | + |
| Execution orchestration | − | + | − | + | − | − | ~ | − | − | ~ |
| Inferred code intelligence | − | ~ | − | − | ~ | − | − | ~ | + | − |
| Registry of external knowledge | − | − | − | − | − | − | − | + | − | − |

## Where Archcore is genuinely differentiated

**The combination, not any single row.** No verified competitor holds all four of: a typed
document set, an explicit relation graph, a status lifecycle, and host-agnostic plain files
in Git. Kiro has the richest feature surface and gives up portability. OpenSpec has the
lifecycle and gives up typing and relations. ByteRover has typing, relations, and lifecycle
and is a memory store rather than an authored document set.

**Nineteen document types with section contracts.** Competitors ship three to five artifact
shapes — usually requirements, design, tasks. Archcore's type set spans decisions, rules,
specs, guides, requirements cascades, and experience patterns, and the type selects the
template and the section contract. No verified competitor types knowledge this finely.

**The relation graph as a first-class store.** `related`, `implements`, `extends`,
`depends_on` in a tracked manifest, queryable before a document is read. ByteRover's Context
Tree and Repowise's decision timeline are the only comparable structures found, and both are
generated rather than authored.

**Mounted global sources.** Read-only org-wide context shared across repositories. The only
competitors with anything equivalent are Tessl's Spec Registry — external library specs, not
your organization's — and Junie's `~/.junie/AGENTS.md` global guidelines, which is a flat
file per user rather than a governed shared source.

**Authored, not derived.** Repowise, Augment, codebase-memory-mcp, Greptile, and DeepWiki all
infer. Inferred context reproduces what the code already says; it cannot recover a rejected
alternative or an unwritten constraint.

## Where Archcore is at parity

These are table stakes and must not carry the pitch. Every serious competitor has them.

- Plain markdown in the repository, versioned in Git.
- An MCP surface for any compatible host.
- Selective retrieval instead of loading the whole corpus.
- Local-first operation with no account.
- Cross-agent portability. `AGENTS.md`-compatible tooling gets this for free.

A public surface that leads on "your context lives in Git" is leading on a row where nine
competitors also score `+`.

## Where competitors are ahead

Recorded plainly. Each is a real gap, not all are worth closing.

1. **Execution.** Spec Kitty runs work packages in isolated git worktrees with a
   `next → review → accept → merge` loop and a Kanban dashboard. Kiro runs event-driven
   hooks on save, create, delete, and repo events. Archcore governs documents, not runs.
2. **Distribution.** GitHub Spec Kit ships with 30+ agent integrations under a GitHub brand.
   Kiro is an AWS product. Conductor is an official Gemini CLI extension. Archcore's
   distribution is a plugin and a CLI it must place itself.
3. **External knowledge.** Tessl's registry of 10,000+ library usage specs answers a question
   Archcore has no mechanism for: what does the agent know about code the team did not write.
4. **Zero-friction adoption.** claude-mem installs as a plugin and starts capturing with no
   authoring step. Archcore requires someone to write the first document. This is the single
   biggest adoption asymmetry in the landscape.
5. **Measured token economics.** Repowise publishes 393 tokens versus 13,984 raw for one
   commit's context. codebase-memory-mcp publishes ~120x reduction and a 31-repository
   evaluation. ByteRover and PROJECTMEM published papers. Archcore has no comparable public
   measurement. `[EVIDENCE REQUIRED]`
6. **Code-derived context.** Archcore cannot answer "what calls this function". Tools that can
   are cheap to add alongside, which makes them complements more than substitutes — but a
   buyer comparing one purchase sees a gap.

## What this implies for positioning

The defensible claim is **typed, related, lifecycle-governed, human-authored context that any
host can read** — four properties held together. Each property alone is matched somewhere in
the landscape.

Two claims should be retired from competitive copy because they no longer differentiate:
*it lives in Git* and *it works with any agent*. Both are now cluster-wide table stakes.

The two facts that most need answering are adoption friction against capture-based memory
tools, and the absence of a published token or quality measurement. Neither is a messaging
problem.

See `product/positioning-vs-alternatives` for the customer-facing framing this document
should inform, and `market/commoditization-and-bundling-risks` for what erodes these rows
over time.
