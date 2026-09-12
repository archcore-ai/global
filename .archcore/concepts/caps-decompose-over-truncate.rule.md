---
title: "Caps: Decompose Over Truncate, and State Every Remainder"
status: accepted
tags:
  - "architecture"
  - "concepts"
  - "docs-style"
---

## Rule

Both tools cap things: a document's body length, a detected-item list, a capability count, the findings in one advisory report. A cap that reduces content with no prescribed remedy and no visible marker loses knowledge silently. The distinction below governs every cap in the ecosystem, and each repository holds its own numbers.

1. An author or a tool MUST classify a cap as a quality cap or a coverage cap. A quality cap bounds how much one document says about one subject; a coverage cap bounds how much of the repository is described at all.
2. A quality cap MUST stay, and reaching it MUST NOT be answered by raising the number alone.
3. WHEN content exceeds a quality cap, the author MUST reference instead of reproduce, MUST route content to the type that owns it, and MUST split the subject by separable sub-surface.
4. IF no sub-surface boundary is unambiguous, THEN the author MUST keep one document and MUST report the excess rather than delete normative content to fit.
5. An author MUST NOT delete normative content to satisfy a cap.
6. WHEN a tool trims a list, the tool MUST state the remainder as a count, so a reader can tell an index from an inventory.
7. WHEN a count exceeds the size one document can carry, the tool MUST route the work to an umbrella document plus one document per part, and MUST NOT ask the user to re-scope it.
8. A cap that hides whole classes of finding MUST be raised or grouped; a report's length MUST be bounded by the number of distinct checks, not by the number of occurrences.
9. A cap MUST NOT be enforced by rejecting a write. An over-cap document is written, and the cap is reported.
10. WHEN a cap bounds cost the user has already priced — a budget they confirmed — the cap MUST stay bounded, and the treatment applied under it MUST be visible to the user before it runs.

## Rationale

A larger number moves the truncation point without giving the writer a remedy: an 80-line cap that fails at 81 lines fails the same way at 121. Clauses 3 and 4 are the remedy, so the number and the procedure are separate questions — revising a cap is allowed, and the procedure governs whatever the number becomes.

Clause 6 exists because a silent trim is by construction unreported: the reader who needs the marker is the one who cannot know anything is missing. The inconsistency was measured — two detection steps printed a remainder and two dropped items with no count, so the same page read as an inventory in one place and an index in another.

Clause 8 comes from a report capped at five findings, which hid whole check kinds on exactly the documents that tripped the most checks. Each check already bounds its own examples, so the report's real bound is the number of checks.

Clause 9 is load-bearing for the whole advisory layer. A line count cannot distinguish a padded document from a legitimately large one, so a blocking cap rejects correct work at some rate, and the cost of a wrong report is a glance.

Clause 10 is the exception that keeps a split from becoming unbounded: a decomposed subject that shares one slot of a confirmed budget would let one priced slot expand without limit. The ceiling bounds cost, not review exposure, so the user sees the treatment named before it runs.

## Examples

**Good** — a module too large for one contract yields one document per separable sub-surface, and each one is whole.

**Good** — a trimmed list that says what it dropped:

```
detected 18 integrations — 15 listed, +3 more
```

**Bad** — a cap answered by raising the number, with no procedure for the next document that exceeds it.

**Bad** — a detection step that drops items past its limit and prints nothing, next to one that prints `+N more`.

**Bad** — an over-cap write rejected, so the author loses the document instead of reading a finding.

## Enforcement

- **Runtime** — the over-the-cap procedure in the shared content contracts, the remainder markers in the grounding steps, the umbrella route above a capability count, and the flagship ceiling that bounds a confirmed budget: `plugin/.archcore/plugin/decompose-over-truncate.adr`.
- **Engine** — the report ceiling, and the general obligation that output leaving the process is bounded by a named ceiling and ordered before it is cut: `cli/.archcore/code-quality/bounded-and-deterministic-output.rule`.
- Which document type owns content routed out of another: `concepts/content-kind-ownership`.
