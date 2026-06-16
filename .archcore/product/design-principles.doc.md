---
title: "Design Principles"
status: accepted
---

## Overview

The principles that shape every Archcore decision. When a choice is unclear, these break the tie.

## Local-first, Git-versioned

Context lives in the repository as plain Markdown, versioned in Git and reviewed in pull requests like code. No database, no external service, no separate system to keep in sync. Context travels with branches, survives sessions, and keeps a full history.

## One setup, every agent

Archcore is tool-agnostic. A single context layer serves every MCP-aware coding agent — Claude Code, Cursor, Codex CLI, GitHub Copilot, Gemini CLI, OpenCode, Roo Code, Cline, and others — through open standards (MCP, Agent Skills, Markdown agent definitions). Knowledge is written once, not re-encoded per tool.

## Documentation as code

Type is encoded in the filename (`slug.type.md`), structure in templates, lifecycle in a status. No hidden state — `ls` shows what exists, and a diff shows exactly what changed. Knowledge is authored, reviewed, and versioned with the same tools as code.

## Structured, not flat

Context is a graph of typed documents with relations, not an ever-growing wall of text. Agents load the specific, relevant chain instead of re-reading everything — and the structure is what makes the context queryable.

## Simplicity by constraint

A deliberately small surface: three statuses, a fixed set of document types, four relation types, one naming convention. Few rules to learn, easy to enforce, hard to misuse. Constraints are a feature.