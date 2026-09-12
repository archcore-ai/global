---
title: "Author an Integration Recipe for Archcore and Another Agent Toolkit"
status: accepted
tags:
  - "integrations"
  - "product"
  - "skills"
---

## What

Turn a chosen pairing of Archcore and another agent toolkit into instructions that reach every host and change agent behavior. The deliverable is a numbered section in the repository's shared instruction file, plus one decision record — and, when the pair is published, a catalog page that imports those exact bytes (`product/integration-recipes`). Delivery decides the outcome: a clause no host loads has no effect, whatever it says.

This is not the task of writing a `rule`. A rule lives in the corpus and reaches an agent through search or a hook. A recipe must reach the agent on every turn, in every host, before the first tool call.

Four recipes have been authored this way as of 2026-09-12 — OpenSpec, Serena, Spec Kit, and Superpowers.

## When to Use

- A connected toolkit claims a phase Archcore also claims: design, planning, execution, or review.
- Two connected toolkits write artifacts of one purpose under two paths, such as a plan or a spec.
- A recipe exists, and a task result shows behavior the recipe forbids.
- A toolkit gives project instruction files precedence over its own skills. That precedence is the seam a recipe binds to.

## Steps

1. Name the entry point each toolkit owns. Record which phase each one leads.
2. List the collisions. Note each artifact both toolkits produce for one purpose.
3. Write one clause per collision. Use line format F3: imperative, no modal.
4. Anchor every clause to a tool name, a path, or a status value.
5. Cut a clause that carries no anchor. It will not change behavior.
6. Put the section near the top of `AGENTS.md`, before any long section.
7. Add the line `@AGENTS.md` to `CLAUDE.md` and to `GEMINI.md`.
8. Keep one copy of the clause text. Every other file imports it.
9. Probe each host. Ask the agent to quote one numbered clause without tools.
10. Run one real task per guard clause. A rehearsal prompt does not test a guard.
11. Move a clause that fails twice into a hook. Prose does not hold it.
12. Record the adoption as an `adr`. Keep the clause text out of the corpus.
13. Publish only through an import: copy the bytes into the site, pin the digest, record the source path and revision.
14. Leave the page experimental until a run against that digest exists.

## Example

The Archcore + Superpowers recipe, measured over three rounds on 2026-09-08 and 2026-09-09. Hosts: Claude Code 2.1.265, Codex CLI 0.153.4, Copilot CLI 1.0.80. Model: claude-fable-5-1.

Delivery decided the outcome. Round one named the clause file from `AGENTS.md` and left the clauses to a read. They reached two sessions of eight, and each failure they forbade occurred: a read-only corpus rewritten, two records accepted without consent, an accepted decision overridden across 29 files. Round two imported the file into `CLAUDE.md` and reached eight sessions of eight.

Three mechanisms, one probe each per host. The probe asks the agent to quote a numbered clause with every read tool disabled.

| Mechanism | Claude Code | Codex CLI | Copilot CLI |
|---|---|---|---|
| A named reference to another file | no | no | no |
| An `@` import | yes | no | yes |
| Text inside the file the host reads | yes | yes | yes |

Form measured last, one run per cell over three tasks. The same clauses as EARS with `MUST` and as plain imperatives produced the same behavior on every clause tested. The imperative set held 388 words against 494.

The clauses ended up inside `@plugin/AGENTS.md` itself, which is the bottom row of that table. An earlier draft kept them in a separate `integrations/superpowers/` directory that the file merely named; that is the top row, and it is why the directory no longer exists.

## Pitfalls

- A named reference reaches no host. Three agents ignored `read and apply <file>`.
- An `@` import misses a host. Codex CLI 0.153.4 keeps the line as text.
- Codex CLI reads a project `AGENTS.md` only when the project is trusted.
- Copilot CLI expands `@` in `AGENTS.md` and `CLAUDE.md`, never in `.github/copilot-instructions.md`.
- Clause text inside `.archcore/` ranks in search: eighth of fifty for `plan`, first among rules.
- A release that strips `.archcore/` strips the recipe from the public branch with it.
- A strict ASD-STE100 pass splits clauses and returns the word count: 32 items, 490 words against 494.
- That same pass drops path anchors. It replaced `.archcore/**/*.adr.md` with a description.
- A clause that forbids a write fails in every form. An agent routes around a read-only mount.
- Two copies of the clause text diverge within weeks. Keep one copy and import it.
- A clause with no anchor states an intent the agent satisfies by another route.
- Editing the published copy instead of the source breaks the digest check and takes the page's evidence with it.
