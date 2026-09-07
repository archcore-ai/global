---
title: "Document Prose Canon: Profile and Line Format Per Document Type"
status: accepted
tags:
  - "concepts"
  - "docs-style"
---

## Rule

`concepts/controlled-technical-writing` states how an author writes. This rule states which prose each document type carries, and it adds only what that rule does not already hold. Two profiles govern every Archcore document: an ASD-STE100-inspired profile constrains the sentence, and an ISO 24495-1-inspired profile constrains the structure. Both profiles apply to every document. The type decides which half binds and which half advises.

1. WHEN an author writes a document of type T, the author MUST apply the profile and the line format that the assignment table gives T.
2. WHILE a document carries the STE profile, the author MUST satisfy rules S1 to S9.
3. WHILE a document carries the ISO profile, the author MUST satisfy rules P1 to P7.
4. The author MUST apply S4, S6, and S7 to English text only.
5. In a numbered clause of an ISO-profile document, the author MUST NOT use a BCP 14 modal.
6. A repository MUST NOT override the profile or the line format that this rule assigns to a type.
7. WHEN this assignment changes, the maintainer MUST carry the change into the engine's precision canon, which is what reaches a project that installs no runtime.

### Profile STE — the form of the sentence

An agent reads an STE-profile line and resolves it into actor, trigger, and obligation without a guess.

| | Rule |
|---|---|
| S1 | One sentence states one obligation or one action. |
| S2 | A procedural step holds 20 words or fewer. A normative clause holds 25 words or fewer. |
| S3 | The sentence uses active voice and names the actor. A subjectless passive is a defect. |
| S4 | The sentence uses present tense, and a gerund is not its main verb. `EN` |
| S5 | One concept keeps one term, taken from the term list the repository declares. |
| S6 | A noun cluster holds 3 words or fewer. `EN` |
| S7 | Every countable noun carries its article. `EN` |
| S8 | An open-ended list marker is a defect. |
| S9 | `and/or` and a slash alternative are defects in a normative clause. |

### Profile ISO — the form of the structure

An agent reads an ISO-profile document, finds the section it needs by name, and separates a fact from a guess.

| | Rule |
|---|---|
| P1 | The first sentence of a section states its purpose or its conclusion. |
| P2 | One bullet carries one claim. |
| P3 | The document uses the heading set that its type declares. |
| P4 | The document orders content as: what, then why, then what it costs. |
| P5 | Every claim carries evidence — an `@path` reference, a measurement, or a commit — or carries `[assumption]` or `[expected]`. |
| P6 | An enumerable fact goes in a table. An argument goes in prose. |
| P7 | The document labels described behavior current, planned, deprecated, or unsupported. |

### Five line formats

The profile decides the style. The format decides the parse.

| | Format | Form of the line | Modals |
|---|---|---|---|
| F1 | EARS with BCP 14 | `WHEN <trigger>, the <actor> MUST <response>.` One modal, active voice, obligated subject. | required |
| F2 | BCP 14 ubiquitous | `The <actor> MUST <response>.` A trigger clause is not required. | required |
| F3 | Imperative | `<Action>.` or `If <condition>, <action>.` One step carries one action. | forbidden |
| F4 | Claim with evidence | `<claim> — <@path, measurement, or commit>`, or the claim carries `[assumption]`. | forbidden |
| F5 | Structured field | `<key>: <value>` in a table or a registry. Prose stays minimal. | forbidden |

### Assignment

| Type | Track | Profile | Format | Metric |
|---|---|---|---|---|
| `spec` | Knowledge | STE | F1 · F2 · F4 | clause <= 25 words · body <= 80 lines |
| `rule` | Knowledge | STE | F2 · F4 · F3 | clause <= 25 words · rationale <= 3 sentences |
| `guide` | Knowledge | STE | F3 | step <= 20 words |
| `adr` | Knowledge | ISO | F4 | context 2-4 sentences · decision 1 sentence |
| `rfc` | Knowledge | ISO | F4 | summary <= 5 sentences |
| `doc` | Knowledge | ISO | F5 · F4 | 1 orienting sentence per section |
| `prd` | Product | ISO | F4 | every goal carries a number |
| `plan` | Product | ISO | F4 · F3 | task <= 20 words, one outcome |
| `idea` | Product | ISO | F4 | `[assumption]` density is unbounded |
| `rnd` | Product | ISO | F4 | one recommendation of four |
| `research` | Product | ISO | F4 | coverage of the declared scope |
| `evidence` | Knowledge | ISO | F5 · F4 | four fixed Locator lines |
| `mrd` | Sources | ISO | F5 · F4 | every market figure carries a source and a date |
| `brd` | Sources | ISO | F5 · F4 | every KPI carries a number and a horizon |
| `urd` | Sources | ISO | F5 · F4 | every need traces to a named persona |
| `brs` | ISO 29148 §9.3 | STE | F2 | identifier `BRS-nnn` · measurable success criteria |
| `strs` | ISO 29148 §9.4 | STE | F2 | identifier `STRS-nnn` · grouped by stakeholder class |
| `syrs` | ISO 29148 §9.5 | STE | F1 | identifier `SYRS-nnn` · verification method per requirement |
| `srs` | ISO 29148 §9.6 | STE | F1 | identifier `SRS-nnn` · traces up to a `syrs` |
| `task-type` | Experience | STE | F3 | step <= 20 words |
| `cpat` | Experience | ISO | F4 | Before and After both hold code |

The `research` and `evidence` assignments follow the accepted vocabulary in `concepts/research-and-evidence-types`. `research` belongs to vision; `evidence` belongs to knowledge. CLI v0.8.3 (2026-09-07) ships both types and the three relations; plugin v0.8.3 (2026-09-07) ships the runtime routes.

The Sources track carries one more constraint that its three types share: formal ISO structure — a mission statement, an operational concept, a verification matrix — belongs to the specification layer, so it is a defect in `mrd`, `brd`, and `urd`.

## Rationale

The split follows the job of the sentence, not the category of the document. A sentence that instructs is parsed and executed, so it earns the tighter form. A sentence that argues is read for its reasoning, and the same tightening strips the reasoning out: an `adr` written under S1 to S9 reads as a manual and loses the record of why the choice held.

Requirement 6 protects portability. A `spec` that means one thing here and another thing in a consumer project stops being a contract. A repository keeps its own scope, its own precedence resolution, and its own enforcement — never its own assignment.

The metrics in S2 come from a measurement. Across 244 documents in the three ecosystem repositories, 99% of `rule` clauses and 96% of `spec` clauses carry an uppercase modal, and 2.5% of documents carry a word from the forbidden lexicon — the one check a program performs today. Against that, 26% of `rule` clauses and 19% of `spec` clauses run past 25 words, 11% of `rule` clauses carry two modals in one clause, and 29% of `guide` steps run past 20 words. `scripts/prose-conformance.py` in the engine repository reproduces these figures. What is binary and named holds; what is gradient and unnumbered does not. The number is the part of ASD-STE100 that the earlier profile stated as intent and never wrote down.

Requirement 7 records where the canon reaches its reader. This shared context is mounted by the two tool repositories only. A project that installs the CLI and no runtime receives the canon through the document templates and the post-write checks, so an assignment that never reaches the engine never reaches most of its audience.

This rule is an internal writing profile. It is not a claim of compliance, certification, or approval by ASD, ISO, or any standards organization.

## Examples

**Good** — an STE-profile clause in F1: trigger first, one actor, one modal, 13 words.

> WHEN `sync` receives a non-2xx response, the CLI MUST leave the manifest unchanged.

**Good** — an ISO-profile claim in F4: the claim carries its evidence, and no modal grades it.

> Session auth added 3-5s latency spikes above 200 concurrent users (dashboard #42, March 2024).

**Bad** — an STE-profile clause that fails S1, S3, and S9.

> Tokens must be rotated and/or revoked, and the gateway should also log the attempt.

Nothing names the obligated component, two obligations share one clause, `and/or` leaves the reader to pick, and the lowercase modals grade nothing.

**Bad** — an ISO-profile bullet that fails P5.

> Improves performance and is easier to operate.

No measurement, no reference, and no `[assumption]` marker, so the claim cannot be checked or challenged.

## Enforcement

- The engine measures the mechanical half: the forbidden lexicon, the heading set per type, the line format per type, the word metrics in S2, and the trigger order. The checks report and never block.
- S4, S6, and S7 carry no automated check. They bind English text under review.
- P1, P4, and P7 carry no automated check. A program finds a missing section; it does not decide whether the first sentence carries the conclusion.
- Each repository holds a local `controlled-technical-writing` rule that names its covered paths, its host instruction file, and its checks. That rule states scope, precedence resolution, and enforcement only, and it restates no assignment from this table.
