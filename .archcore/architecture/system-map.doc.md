---
title: "System Map: From a Command to a Document Type"
status: accepted
tags:
  - "architecture"
  - "concepts"
  - "product"
---

## Overview

One vertical walkthrough of the whole system: what a user touches, what it routes into, what that produces, where it is stored, and how it comes back to the agent. Every stage below is defined in depth elsewhere; this document is the map that connects them, so a reader never has to reconstruct the chain from six documents.

These are **named stages, not a new numbering**. `architecture/conceptual-architecture` names four architectural roles — context, engine, runtime, access — and tool repositories number their own internals. The stages below map onto the roles; they never introduce a competing count.

## The stack at a glance

| Stage | What it is | Owner |
|-------|------------|-------|
| Entry | A request in plain language, a slash command, or just a file edit | — |
| Command | Four verbs: `init`, `plan`, `document`, `review` | Runtime |
| Track | A gated flow selected by routing, never by a menu | Runtime |
| Gate | One stage of a track: entry conditions, questions, output, exit checks | Runtime |
| Document | A typed Markdown file with frontmatter and relations | Context |
| Store | `.archcore/` in Git — scanning, validation, the relation graph | Engine |
| Access | MCP tools and three lifecycle hooks | Engine |

## Entry — three ways in, and one of them is silent

1. **Plain language.** The user describes intent; the runtime routes it. No command is typed.
2. **A command.** The same workflows, reached explicitly.
3. **No interaction at all.** The everyday path. The session opens with a recap, and the rules and specs that apply to a file arrive when the agent edits it. This is why there is no "load my context" command — see `architecture/lifecycle-hooks`.

## Command — four verbs

| Command | Moment | Writes mostly |
|---------|--------|---------------|
| `init` | First day in a repository | All three categories — a seeded first-day pack |
| `plan` | Before building something | vision types |
| `document` | A decision was made, or code has no doc | knowledge types |
| `review` | Before merge, or when checking health | experience types |

Write affinity is a tendency, not a fence: **every command reads all three categories**, because vision supplies intent, knowledge supplies constraints, and experience supplies precedent.

Invocation scales with how much the user already knows: no arguments, vague arguments, specific arguments, or the expert form — naming a track or type directly, which skips routing entirely.

`init` sits outside the track layer. It detects the repository, composes a seed in one preview, creates it on one confirmation, wires host configs, and imports existing `CLAUDE.md` / `AGENTS.md` / `.cursorrules` content.

## Track — where the branching lives

Beneath each work command sit gated tracks (`concepts/gated-tracks`). Routing picks one from signals in fixed order: an explicitly named track, the state of the document graph, the state of the branch, then the wording of the request.

- `plan` → `sdd`, `requirements-cascade`, `research`
- `document` → `describe`, `decision`
- `review` → `actualize`, `closeout`, `experience`
- `decision` is reachable from all three, because a decision can surface anywhere

The user is never asked to pick. Vagueness sets the **question budget**, not the route.

## Gate — the unit of work

A gate carries: its purpose, entry conditions with a skip rule, the elicitation knobs that bound its questions, the document it produces, exit checks marked blocking or advisory, and the next gate.

Two properties matter more than the rest:

- **A satisfied gate asks nothing.** When existing documents or the request text already answer it, the gate skips. A fully specified request runs question-free.
- **A track resumes.** Track state lives inside the draft it is producing, so an interrupted flow picks up in a later session at the earliest gate whose blocking checks have not passed, without re-asking answered questions.

## Document — where the type comes from

A gate produces a file named `<slug>.<type>.md`. The type suffix is the whole classification mechanism:

- The **type** (19 of them) selects the template and the section contract.
- The **category** — vision, knowledge, experience — is *derived* from the type. No command asks the user to choose a category.
- The **directory** carries no meaning; layout is free-form.
- The **status** starts at `draft`. Promotion to `accepted` is a separate explicit act, never a side effect of a gate, a hook, or an automated check.
- **Relations** — `implements`, `extends`, `depends_on`, `related` — link the new document into the chain, so the next agent can walk back to the rationale.

Every one of the 19 types is reachable through at least one command path. Full type reference: `concepts/document-types-reference`. Recommended cascades of types: `concepts/document-tracks`.

## Store — one mutation surface

Documents live as Markdown in `.archcore/`, versioned in Git and reviewed in pull requests. The engine scans and validates them, maintains the relation graph, and holds the templates plus the precision canon those documents are measured against.

MCP is the **single** mutation surface. A direct editor write into `.archcore/` is refused by the write guard, so a path the MCP tools reject cannot be reached by going around them.

## Access — how it comes back

Two paths, both engine-owned (`architecture/engine-runtime-boundary`):

- **MCP tools** — list, search, read, create, update, relate. Available to any MCP-aware agent, with or without the runtime.
- **Lifecycle hooks** — `SessionStart` (recap), `PreToolUse` (write guard, code-alignment injection), `PostToolUse` (validation and advisories).

Coverage varies by host, and a host missing an event loses that event's value and nothing else — see `architecture/supported-ai-hosts`. A repository may also mount shared context read-only from another repository (`concepts/global-sources`); those documents appear in the same searches, marked as global, and are never written by the consumer.

## End to end

A user says *"we're switching the payments API to token-bucket rate limiting"*.

1. Wording routes to `document` → the `decision` track. No command was typed.
2. `decision.classify` finds the decision already final and the reasoning present in the request, so it asks nothing.
3. `decision.adr` produces `token-bucket-rate-limiting.adr.md` as a draft — knowledge category, derived from the `adr` suffix.
4. `decision.cascade` offers the Standard cascade and produces a `rule` for where limiter middleware belongs, linked `depends_on` the ADR.
5. The engine validates both on the post-write hook and reports the new relation.
6. Next week, in a fresh session on another host, an agent edits a payments handler. The pre-write hook injects that rule before the edit. Nobody re-explained anything.

Step 6 is the product. Steps 1 to 5 are how it gets there.
