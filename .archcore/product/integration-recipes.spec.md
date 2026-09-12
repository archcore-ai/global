---
title: "Integration Recipes and the Public Catalog"
status: accepted
tags:
  - "integrations"
  - "product"
  - "web"
---

## Purpose & Scope

An **integration recipe** is a set of cooperation instructions for Archcore and one other agent toolkit, delivered through the instruction file the host already reads, plus the public page that explains the pair and hands the instructions out. This spec is the ecosystem contract between the three owners of that pair: the repository that authors the instructions, the site that publishes them, and the documentation site that carries operational depth. Dependents: `@landing/src/content.config.ts`, `@landing/src/pages/integrations/`, `@landing/src/lib/recipe-source.ts`, and the instruction file of any repository that opts a recipe in.

Shipped as of 2026-09-12: four recipes — OpenSpec, Serena, Spec Kit, and Superpowers — at `/integrations/` and `/integrations/<recipe>/`, all four experimental. Recorded as current behavior, not as a coverage target.

The OpenSpec and Spec Kit pilot note of 2026-09-12 is what the digest rule looks like in practice: real runs exist, they were measured against earlier instruction text, and the pages therefore publish them as reading material rather than as verification of what they now hand out.

Out of scope: an execution harness, an assembler that installs a recipe automatically, community submissions, accounts, payments, and generated combinations of arbitrary tools. Catalog presentation detail — layout, tabs, the install panel, the Russian layer — belongs to `landing/.archcore/landing/integration-page-authoring.rule`. The delivery mechanics of a recipe's clauses belong to `product/author-an-integration-recipe`.

## Surface

- Routes: `/integrations/` (the catalog) and `/integrations/<recipe>/` (one pair), plus the raw-instruction route each page hands out.
- A recipe entry holds three parts with three owners: the presentation body, which the site owns; the imported instruction text, which the authoring repository owns; and the binding between them — `source` (repository, path, revision), `digest`, `hosts[]`, and `evidence[]`.
- `source.revision` is `null` while the instructions exist only on a mutable branch.
- `digest` is the SHA-256 of the imported instruction bytes.
- An evidence record carries the digest it ran against, the date, the host, and the observed outcome; the extract lives outside the entry.
- `hosts[].verified` records whether a path was exercised, never whether it was written.
- There is no publication-status field. Status is derived: a recipe with no evidence record is experimental.
- Categories group entries in the catalog; a category is a description of the partner tool's kind, not a tier.

## Normative Behavior

1. WHEN a visitor opens the catalog, the page MUST state both ways in: using Archcore with tools the reader already runs, and making Archcore part of the reader's own agent setup over MCP.
2. The catalog MUST NOT frame a recipe as a partnership or an endorsement, and MUST NOT imply that the partner tool's maintainers took part.
3. WHEN a visitor opens a recipe page, the page MUST name the joint outcome before the mechanism that produces it, and MUST state each tool's own contribution.
4. WHEN a recipe page states a benefit, the page MUST state the material limitation beside it.
5. WHEN a recipe has no evidence record, the page MUST identify the recipe as experimental.
6. The page MUST NOT present copied instructions, a completed installation, or an unexecuted scenario as verification.
7. WHEN the build renders a recipe, the build MUST verify the imported instruction bytes against the recipe's `digest`, and IF they disagree, THEN the build MUST fail naming the recipe.
8. WHEN the build resolves evidence for a recipe, the build MUST exclude a record whose digest is not the recipe's current digest.
9. The authoring repository MUST own the instruction text, and the publishing site MUST import it verbatim.
10. WHEN an author edits presentation copy, the author MUST NOT change the imported instruction text to match it.
11. WHEN the instruction text changes, the publisher MUST recompute the digest and MUST re-establish any evidence claim the previous digest carried.
12. WHEN a recipe page hands out instructions, the page MUST deliver the same revision it displays.
13. A recipe MUST include Archcore; a pairing of two other tools is outside the offering.
14. A recipe MUST stay opt-in. Installing Archcore MUST NOT select a partner toolkit's method, and connecting a recipe MUST NOT be read as authorization to implement, to accept a document, or to take over the user's next task.
15. WHEN both toolkits produce an artifact of one purpose, the recipe MUST name one owning artifact and MUST surface the collision rather than maintain two canonical copies.
16. WHEN a reader's host has no written setup path, the page MUST expose the generic path — document access over MCP — and MUST NOT promise automatic hook delivery outside the supported hosts.
17. WHEN a page names a section of an imported file, the page MUST keep that file's own wording.
18. The recipe pages MUST stay inside the accepted static hosting boundary, and MUST NOT require a server at request time.

## Constraints & Invariants

- Invariant: one instruction text, one owner. Every other copy is an import pinned by digest, so a presentation edit cannot change what an agent reads.
- Invariant: a claim is scoped to the configuration that produced it. A result for one pair establishes nothing about a third tool, another host, or another revision of either tool.
- Invariant: publication status is derived, never asserted. A field an author can edit to claim verification is a field that eventually lies.
- Constraint: the catalog MUST NOT publish a page per tool, host, and version permutation. One page describes one pair.
- Constraint: an existing root host page keeps its query ownership; a recipe page MUST NOT compete for it.
- Constraint: a recipe page MUST NOT redistribute a partner's packaged skills or assets; it links to the partner and imports only the cooperation instructions.
- Constraint: the catalog and the operational documentation MUST NOT hold two editable copies of one instruction. A documentation page exists only where it adds operational guidance the short page does not carry.

## Failure Behavior

1. IF the imported instruction file is missing, THEN the build MUST fail naming the recipe rather than render a page without instructions.
2. IF an evidence record references another digest, THEN the build MUST omit that record and MUST NOT relabel the recipe as verified.
3. IF a host path was written but never exercised, THEN the page MUST show it as unverified guidance.
4. IF a scenario failed, THEN the page MUST state the affected scope and MUST NOT report it as passed.
5. IF clipboard access fails, THEN the page MUST expose selectable instructions.
6. IF JavaScript is unavailable, THEN the page MUST still carry the installation instructions in its initial HTML.
7. IF a recipe route is unknown, THEN the site MUST answer with a not-found outcome.
8. IF the partner tool or its instructions change upstream, THEN the previous evidence MUST remain historical evidence for its own digest, and support for the new revision MUST read as unknown until it is checked.

## Conformance

Conformance is checked against built output, not against source intent: the digest check at build time, the evidence filter on the rendered page, the presence of instructions in the initial HTML, the published title and description against the SEO baseline, and the unknown-route outcome. Browser checks cover copying, the install dialog, the generic path, and the no-JavaScript fallback.

A source review, a setup check, one scenario run, and repeated project use are four separate findings, and none of them upgrades another. Deployment verification checks the public routes after publication; a passing build establishes neither live behavior nor a completed installation by any reader.
