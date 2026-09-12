---
title: "Content-Kind Ownership: One Statement, One Owning Document"
status: accepted
tags:
  - "concepts"
  - "docs-style"
  - "document-types"
---

## Rule

A track produces several documents on one topic: a `prd` that states the wanted outcome, the `spec` that grades the behavior satisfying it, the `plan` that delivers it, and an `adr` that records the alternative that was rejected. Each kind of statement has exactly one owning type and one section inside it. This assignment is the ecosystem's; both tool repositories previously carried their own copy of it.

| Content kind | Owner | Section |
|---|---|---|
| Wanted outcome, beneficiary, threshold | `prd` | Requirements |
| Measured goal with units and a target value | `prd` | Goals and Success Metrics |
| Graded behavior: EARS clauses, BCP 14 modals | `spec` | Normative Behavior |
| Interfaces, signatures, states, field-driven rules | `spec` | Surface |
| Error, edge, and degradation handling | `spec` | Failure Behavior |
| Phases, tasks, milestones, delivery dates | `plan` | Tasks |
| Rejected alternative and the reason it was rejected | `adr` | Alternatives Considered |

1. WHEN an author writes a statement of a kind the table assigns, the author MUST write it into the owning document and MUST NOT write it into a second document.
2. WHEN a later document takes over a kind the upstream document currently states, the author MUST edit the upstream statement down to the kind that document owns, in the same change that adds the new one.
3. The author MUST state a `prd` requirement as an outcome, and MUST NOT use EARS clause order or a BCP 14 modal in a `prd`. Those are `spec` notation, and the ISO requirement types keep their own.
4. WHEN a document type offers no section for a kind, the author MUST route the statement to the owning type rather than add a heading that type does not own.
5. A completion signal reaches three different sections — `prd` Goals and Success Metrics, `plan` Acceptance Criteria, `spec` Conformance — and coverage in one MUST NOT be read as coverage in another.
6. A content kind absent from the table is unconstrained, and an author MUST NOT infer an owner for it.
7. An automated restatement or foreign-heading finding MUST report and MUST NOT reject a write.
8. A document accepted before this rule MUST NOT be retro-fitted, and a finding on it MUST NOT invalidate it.

## Rationale

Two documents holding one statement have no single owner. An edit to one leaves the other stating the opposite, and a reader cannot tell which of the two binds. The failure is measured, not theoretical: on the corpus of 2026-08-13 one statement appeared unchanged in an `idea`, a `prd`, and the `plan` implementing it, six of eight requirements in one `prd` reappeared as numbered behavior in its `spec`, and one `prd` stated eight numbered behaviors that its own `spec` also carried.

The `prd` is where the pressure concentrates, because it is the first document written and the author has nowhere else to put a detail yet. Clause 3 removes the specific temptation: a `prd` that reaches for a modal is usually reaching for the `spec` it has not written.

Clause 7 exists because both checks are heuristic by construction. A near-verbatim comparison over a token threshold can be wrong, and a wrong finding costs the author a glance while a wrong rejection costs the author the write. Paraphrase detection was deliberately excluded: a `prd` requirement and the `spec` behavior that grades it are *meant* to differ in wording, so a threshold low enough to catch paraphrase reports the boundary working as noise.

Clause 6 keeps the table honest. Only unambiguous kinds are assigned. A `prd` may name a business constraint inside its Problem Statement without owing the reader a Constraints section, so that kind carries no owner and produces no finding.

## Examples

**Good** — the `prd` states the outcome and the `spec` grades it, and neither sentence is the other:

> `prd` — A user who runs the update command learns whether an update exists without waiting on the network.
>
> `spec` — WHEN the check exceeds its total timeout, the CLI MUST discard the outcome and continue.

**Good** — the handover in clause 2, as one change: the `spec` gains the graded behavior and the `prd` sentence is edited back to the outcome it owns.

**Bad** — the same sentence in the `prd` Goals section and in the `plan` Acceptance Criteria, word for word.

**Bad** — a `prd` numbered requirement reading `WHEN the payload arrives, the server MUST validate it`.

## Enforcement

- **Engine** — the heading-to-owner table as data, the `prd` template reduced to the sections it owns, and the post-write foreign-section and restatement checks: `cli/.archcore/document-types/prd-spec-plan-content-ownership.adr`.
- **Runtime** — the content contract the composing skills load, and the blocking exit checks on the gates that produce a second document on one topic: `plugin/.archcore/plugin/prd-spec-plan-content-ownership.adr`.
- The line format and the prose profile each type carries: `concepts/document-prose-canon`. Which type to reach for at all: `concepts/document-types-reference`.
- Adding a content kind means adding a row here and in the engine's table, and nothing else.
