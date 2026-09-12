---
title: "Integration Catalog on archcore.ai, Operational Guidance in Docs"
status: accepted
tags:
  - "integrations"
  - "product"
  - "web"
---

## Context

Archcore needs a public destination where users can discover integration recipes, understand their behavior, and add them to an existing setup. The landing project already carried a static Astro content build, and the documentation site already carried operational guidance. On 2026-09-08 the user accepted the researched division between catalog discovery and operational documentation; search traffic and recipe compatibility were unmeasured at that point.

## Decision

Place the curated Archcore integration catalog at `https://archcore.ai/integrations/` in the landing project, with short setup instructions on recipe pages and operational depth in `docs.archcore.ai`.

## Scope

The catalog offers Archcore paired with a selected tool. A reader may enter through Archcore's own commands or through the other tool's; placement on Archcore's site assigns Archcore no permanent control over the reader's process, and a recipe is instructions for a pair of tools rather than a partnership.

The catalog targets readers on any host, including hosts Archcore's own setup guidance does not name. Required capabilities and available connection paths are stated; named host and model environments describe verification coverage, not an eligibility boundary. Dedicated instructions per host are allowed, and identical wording across hosts is not required.

Existing root host pages keep their query ownership. Recipe pages live under `/integrations/` and describe one pair each. The catalog publishes no page per tool, host, and version permutation.

The behavior of the published pages — what a recipe page must explain, what it may claim, how instructions are pinned and evidence is scoped — is `product/integration-recipes`. This record covers only where the catalog lives and how the two sites divide the work.

## Current state (2026-09-12)

The direction is implemented, and three of its open questions have since closed:

- **Four recipes are published, not one pilot.** OpenSpec, Serena, Spec Kit, and Superpowers. The accepted first pilot was Archcore + Superpowers alone.
- **The catalog builds in the single root Astro site.** The separate `content-site` sub-build named in the original alternatives was retired — `landing/.archcore/landing/single-astro-site.adr`, with `content-hub-astro-subbuild.adr` rejected. References to `content-site/` paths in the research behind this record describe the layout of 2026-09-08.
- **The instruction source and its synchronization are settled.** The authoring repository owns the cooperation instructions inside the instruction file its hosts already read, and the site imports those bytes verbatim, pinned by digest, with the source repository, path, and revision recorded. A checked-in release snapshot, a release schema, and an assembler were not needed to publish; none exists.

What remains open is narrower than it was. OpenSpec and Spec Kit carry measured runs — five configurations, twice each, on one fixture, on one host and one model — reviewed 2026-09-12 and published as a pilot note the two pages link. Those runs used earlier instruction digests than the text now published, so no record attaches to a current recipe and all four pages stay experimental by derivation rather than by choice. Acquisition through the catalog is unmeasured.

## Alternatives Considered

- **Entire catalog in `docs.archcore.ai`:** rejected for the initial direction because discovery and comparison belong with the product evaluation journey; documentation tooling stays useful for operation.
- **Catalog and all guidance in landing:** rejected as the general boundary because detailed setup, updates, and troubleshooting already have a documentation home; a short recipe page can still be complete on its own.
- **Independent marketplace site:** deferred because it would add a domain and a publishing surface before the Archcore-centered catalog has shown adoption.
- **Migrate the entire landing to Astro:** this was deferred here and then taken, for reasons of its own — one static site with shared layouts, recorded in the landing repository.

## Consequences

- A reader can evaluate a pair and reach its setup instructions from one public URL.
- The static pipeline hosts the catalog inside the existing GitHub Pages deployment, with no server at request time.
- Version-pinned instructions and digest-scoped evidence serve the catalog without a second editable copy of the instruction text.
- Landing and docs need explicit content ownership whenever one recipe change affects both.
- A public support claim creates maintenance work when either tool changes upstream; the digest is what makes that visible rather than silent.
- Trade-off: a recipe page needs substantive guidance and real evidence before it can advertise tested cooperation, and four pages currently cannot.

This record establishes no SEO advantage over a subdomain. Traffic, completed setup, and later reuse of stored context are separate measurements.

## Superseded when

- Comparable acquisition cohorts show a lower completed-setup rate through the catalog than through docs, after accounting for traffic source and recipe differences.
- The accepted static hosting or the landing build architecture changes so that the catalog can no longer be served statically.
- A separately approved marketplace requires accounts, transactions, or publishing operations that the static delivery boundary cannot carry.

## Clarifications

The user confirmed the distribution recommendation on 2026-09-08, covering the catalog location, the landing and docs roles, the shared recipe source, and the Archcore + Superpowers pilot direction. The user then asked that the solution serve readers on any host and explicitly allowed dedicated per-host instructions, prioritizing a reader's ability to install the integration. On 2026-09-12 the user set the catalog framing: two ways in, not one list of partnerships.

Accepting this record performed no publication. What has since shipped is recorded under Current state.
