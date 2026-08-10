---
title: "How Agents Use Archcore"
status: accepted
tags:
  - "concepts"
---

## Overview

The day-to-day loop. Archcore only helps if agents read context before acting and record context as decisions are made. Both are cheap; skipping them is what causes drift.

## What arrives without being asked

Two of the three steps below happen on their own where lifecycle hooks are wired (`architecture/lifecycle-hooks`): the session opens with a recap of what is decided and in progress, and the rules, specs, and decisions that apply to a file arrive at the moment the agent edits it. The loop below is what the agent still owns — and it is the whole loop on a host without hooks.

## The agent loop

1. **Search first.** Before touching real code or behaviour, query the context for anything that already constrains the work — a decision, rule, or spec may already apply. Read only what matches.
2. **Read the chain.** Open the relevant documents and follow their relations, so the rationale behind a rule or plan comes along with it.
3. **Act in line with what's recorded.** Code lands where the architecture says it belongs and follows the conventions already decided.
4. **Capture new context.** When a decision is made ("we'll use X", "from now on Y"), a module has no documentation, or a search comes back empty — record it as the right typed document.
5. **Link it.** Connect the new document to what it implements, extends, or depends on, so the next agent finds the whole chain.

## When to record

- A decision or convention was chosen → capture it (adr / rule).
- A module, API, or contract is undocumented → capture it (doc / spec / guide).
- A recurring task or an incident learning emerged → capture it (task-type / cpat).

## When to skip

Turns the project would have no opinion on — syntax trivia, throwaway snippets, pure mechanics. The search is cheap; lean on it, and skip only when there is genuinely nothing to constrain.

## How to write

Every write goes through MCP — it is the single mutation surface, and a direct editor write into `.archcore/` is refused by the write guard. A document is created as a draft; promotion to accepted is a separate, explicit act, never a side effect of a hook.

## Why it matters

Context that is never read is dead weight; context that is never written is lost the moment the session ends. The loop keeps the repository's understanding alive across agents, sessions, and teammates.
