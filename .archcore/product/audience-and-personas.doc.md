---
title: "Audience & Personas"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Overview

Who Archcore is for, and who it is not for. This frames every product and messaging decision.

## Primary personas

**Founders building with AI agents.** Move fast with coding agents but need output to respect the architecture without constant correction.

**Staff / principal engineers.** Own architectural consistency across a codebase and many contributors — human and AI. Need decisions and standards to be durable and enforced, not tribal.

**Engineering teams using coding agents.** Already run Claude Code, Cursor, Codex CLI, and similar. Want one source of truth that works across whichever tool each teammate uses.

## Strong fit

- Teams with scattered architectural knowledge — ADRs, CLAUDE.md, conventions in PR comments, decisions in chat.
- Codebases with conventions worth enforcing across people and agents.
- Multi-tool teams that don't want to re-encode knowledge per agent.

## Weak fit

- Throwaway or single-session greenfield work with no conventions to preserve.
- Teams not using AI coding agents at all.

## What they feel when it works

- "The agent finally understands my repo."
- "Our architecture is no longer tribal knowledge."
- "The context survives across agents, sessions, and teammates."