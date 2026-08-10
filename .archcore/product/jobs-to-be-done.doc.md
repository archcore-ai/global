---
title: "Jobs To Be Done"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Overview

Archcore is not adopted "to document things". It is adopted for four jobs that **start in code and end in code** — context is the means, not the deliverable.

This document names the jobs, ranks them, and fixes what each one turns into on public surfaces and in first-run prompts. The ranking is also the display order. Phrasing is governed by `product/messaging-and-voice`.

## Content

### Job 1 — "Ship this feature, but by this repo's rules" (primary)

**Trigger.** The user asks for an endpoint, service, screen, integration, or refactor — already knowing the agent tends to code by generic patterns instead of this project's.

**What they actually want.** Not code. Code placed where this repo puts it, following existing conventions, without inventing a new structure.

**Why it is an Archcore job.** Architecture tells the agent where code belongs; rules make it follow team standards instead of improvising. The mechanism is automatic: the applicable rules, specs, and decisions are injected on the pre-write hook, at the moment of the edit — the user runs no command (`architecture/lifecycle-hooks`).

**How the user says it.** *"I already asked the agent to build the feature. I want it built by this repo's rules, not however it likes."*

This is the lead job. It is the most concrete, and it is what separates Archcore from spec-driven pipelines: Spec Kit starts at "describe what you want to build" and walks specify → plan → tasks → implement. Archcore is sold as a **repo-alignment layer at the moment of coding**, not as a spec pipeline.

### Job 2 — "Continue the work without re-explaining the project" (secondary)

**Trigger.** New session, different agent, different host. The long context is gone; the feature work is not finished.

**What they want.** The agent quickly understands what was already decided, which patterns are in use, what is in focus, and what the next steps are.

**Why it is an Archcore job.** Prior ADRs, existing specs, and captured patterns are respected; the session hook loads the document index and relations at the start of work.

**How the user says it.** *"I don't want to explain again why payments / auth / the API layout are built this way."*

This is not pure memory. The claim is narrower and stronger: *give the agent a fast read on what already counts as true in this project.*

### Job 3 — "Record this decision so it changes the next code" (supporting)

**Trigger.** A decision was made — Postgres was picked, a rule for API handlers was set, a testing guide was agreed, an ADR was written down.

**What they want.** Not a Markdown file. They want the agent to account for that decision in the next changes.

**Why it is an Archcore job.** Document creation is valuable as a change in later agent behaviour, not on its own. The user does not arrive to write an ADR — they arrive to make the new ADR affect future code.

**How the user says it.** *"Record this decision so the agent stops arguing with it on the next task."*

### Job 4 — "Walk me through a change that needs a chain of artifacts" (advanced)

**Trigger.** Not a small edit — a change that pulls a PRD, a plan, a rule, a guide, and possibly an audit trail along with it.

**What they want.** A structured sequence of artifacts that ends in implementation, not a single generated document.

**Why it is an Archcore job.** Cascades like PRD → plan and ADR → rule → guide are supported. The runtime carries them as gated tracks — including a spec-driven track and the ISO requirements cascade — reached by escalation from a normal planning request rather than as a separate mode the user selects (`concepts/gated-tracks`). This is adjacent to Spec Kit / BMAD territory, where the staged flow is the *primary* product scenario — for Archcore it is **advanced mode**, never the first use case.

**How it is framed.** *"When the task is complex, Archcore can walk the agent through a chain of project artifacts to implementation."*

**Where the boundary holds.** The spec-driven track produces linked context documents that later code is measured against. It does not generate code from a spec, and `spec` stays a contract of a depended-on boundary rather than a source artifact (`concepts/spec-boundary-contract-repositioning`). Borrowing the staged flow does not move Archcore from a context layer to an SDD pipeline; describing it as one on a public surface contradicts Job 1's positioning.

### Ranking

| # | Job | Role |
|---|-----|------|
| 1 | Build by this repo's architecture, rules, and past decisions | **Primary** — always lead with this |
| 2 | Continue work without re-explaining the project | Secondary |
| 3 | Record a decision so it shapes future code | Supporting |
| 4 | Run a multi-step track through to implementation | Advanced |

### What this means for public surfaces

**Primary promise.** Archcore helps your coding agent make changes that fit your repo's architecture, rules, and past decisions.

**Secondary promise.** It also gives the agent durable project context across sessions, and turns new decisions into future guardrails.

Together these close the three recurring misreads — *"is this Spec Kit?"*, *"is this a knowledge-management suite?"*, *"is this just memory?"*. It is none of them: Archcore makes code generation repo-aware. See `product/positioning-vs-alternatives` for the full comparison set.

## Examples

First prompts, one per job:

- **Job 1** — "Before changing auth, what architecture rules and prior decisions should you follow here?"
- **Job 2** — "Read the project context and tell me what matters before we continue the payments work."
- **Job 3** — "Record a rule for where API handlers belong, then explain how it should affect future changes."
- **Job 4** — "Create a PRD and implementation plan for the auth redesign, based on the repo's current architecture."
