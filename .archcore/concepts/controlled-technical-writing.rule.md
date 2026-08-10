---
title: "Controlled Technical Writing for Archcore Documentation"
status: accepted
tags:
  - "concepts"
  - "vocabulary"
---

## Rule

Two readers consume Archcore documentation: engineers and AI coding agents. Both fail the same way on ambiguous text — they guess the actor, the trigger, or whether a sentence records a fact, a decision, or a wish. This is the ecosystem writing profile that every repository applies. Each repository declares its own file scope and its own enforcement; none of them restates these obligations.

1. WHEN an author creates or updates documentation in an Archcore repository, the author MUST apply this profile. Each repository names the covered paths, which MUST include `.archcore/**`, `README.md`, and any user-facing technical documentation.
2. WHEN instructions conflict, the author MUST follow this precedence: an explicit user requirement, accepted `.archcore/` rules and decisions, the document-type contract and template, this profile, general stylistic preference.
3. In a numbered requirement of a normative document — `rule`, `spec`, `brs`, `strs`, `syrs`, `srs` — the author MUST state one obligation, one uppercase BCP 14 modal, and one named obligated actor.
4. WHEN a requirement depends on a trigger or a state, the author MUST place the trigger or the state before the obligation.
5. In a numbered requirement, the author MUST NOT use an open-ended list marker such as `etc.`.
6. The author MUST NOT place a required action only in a note, a rationale paragraph, a heading, or an example.
7. WHEN the author writes a descriptive document — `adr`, `rfc`, `doc`, `guide`, `prd`, `idea`, `plan`, `rnd` — the author MUST NOT force normative modals into content that records context, rationale, or exploration.
8. In a procedure, the author MUST state prerequisites and inputs before the first numbered step, MUST put one primary action in each step, and MUST place a warning before the action it guards.
9. The author MUST preserve identifiers, package names, paths, commands, flags, configuration keys, API and tool names, document type names, and literal values exactly.
10. The author MUST NOT invent a constraint, a measurement, a behavior, a rationale, or a guarantee that repository evidence does not support.
11. IF a claim has no repository evidence, THEN the author MUST mark it `[assumption]` or insert a visible placeholder such as `[EVIDENCE REQUIRED]`.
12. The author MUST reference an implementation file with `@path/to/file` instead of reproducing its body.
13. The author MUST state whether described behavior is current, deprecated, planned, or unsupported.
14. The author MUST write repository documentation in English unless the user or the existing document requires another language.
15. The author MUST NOT state or imply that a repository complies with ASD-STE100, ISO 24495-1, or any other external standard. The profile is inspired by them and is internal.
16. The author MUST NOT edit a mounted global source and MUST NOT create a relation to one.
17. The author MUST NOT include a review checklist in a generated document, and MUST NOT include a writing-quality score unless the user asked for a review report.

## Rationale

A single profile keeps the wording of a `rule` verifiable and keeps an `adr` readable as a record of reasoning. Rules 3 to 6 exist because a requirement an agent cannot parse into (actor, trigger, obligation) is a requirement it will apply inconsistently. Rules 10 and 11 exist because a confidently invented guarantee is worse than a visible gap: the gap gets filled, the invention gets cited.

Rule 15 protects a real liability. Claiming conformance to a standard the repository does not audit against is a compliance statement, not a style note.

Rule 16 restates the read-only invariant of `concepts/global-sources` at the moment an author is most likely to break it — while editing documentation.

This rule lives in the shared context because both tool repositories previously carried their own copy, and the copies had already diverged on precedence order, on covered types, and on whether external-standard compliance may be claimed.

## Examples

**Good** — one actor, one modal, trigger first:

> WHEN `sync` receives a non-2xx response, the CLI MUST leave the manifest unchanged.

**Good** — an unsupported claim marked rather than asserted:

> `init` writes the instruction file for each detected agent. Current behavior; see `@internal/agents/instructions.go`.

**Bad** — no actor in the first clause, two obligations, mixed modals, an open-ended list, and no failure path:

> The MCP config should be merged carefully and the CLI must not break other keys, fail silently, etc.

**Bad** — a qualitative claim with nothing behind it:

> The sync engine is fully standards-compliant and very fast.

## Enforcement

- Each repository holds a local `controlled-technical-writing` rule that names its covered paths, its host instruction file, and its automated checks. That rule MUST NOT restate the obligations above.
- Automated coverage is partial by design: a precision check can verify modals, sections, frontmatter, and body length; the actor, the evidence, and the tense obligations are review-time checks.
- The authoring agent verifies the profile before returning a document.
