---
title: "Two Discovery Categories: Spec-Driven Development and Context Engineering"
status: accepted
tags:
  - "messaging"
  - "product"
---

## Context

Archcore's public surfaces carry three incompatible category claims at once.

- `product/messaging-and-voice` names "git-native context for AI coding agents" as the positioning and puts "context engineering platform" on the avoid-list as outdated framing.
- Both public sites lead their `<title>` with the category term "repo memory", under `landing/.archcore/landing/home-title-category-keyword.adr`. The same messaging rule flags that exception as undeclared and marks it `[DECISION REQUIRED]`.
- `landing/.archcore/landing/seo-research-sdd-context-skills.rnd` rates "context engineering" and "spec-driven development" as occupied heads (IBM, Gartner, Anthropic, GitHub, Wikipedia) and recommends the "{host} memory" long tail instead.

A reader therefore meets "repo memory" in search, "git-native context layer" in the README, and "structured, machine-readable context" in the docs. Meanwhile `product/jobs-to-be-done` warns that describing Archcore as a spec-driven pipeline on a public surface contradicts Job 1.

There is no single place that holds the canonical strings, so every surface re-derives them.

## Decision

Archcore occupies **two adjacent discovery categories** and keeps **one narrow product definition**.

- Discovery categories: **Spec-Driven Development** and **Context Engineering**. Canonical category line: *Spec-Driven Development & Context Engineering for AI Coding Agents*.
- Product definition, unchanged in substance: *Archcore is a git-native context layer for AI coding agents.*
- Category terms carry search, discovery, and pillar pages. The product definition answers every "what is this".
- **"Memory" retires as positioning on every surface, including `<title>`.** It stays legal in comparison and migration content, where the reader arrives already holding the term.
- **Specs are one part of context; context is broader than specs.** Every surface that uses both category terms teaches that relation.
- The two categories describe the product, not the entry points. `architecture/one-product-two-entry-points` continues to govern Plugin and CLI framing: the CLI descriptor leads on git-native context infrastructure, the Plugin descriptor leads on spec-driven development and context engineering inside the host. That is a scope difference, never a rank.

Canonical strings live in `product/canonical-narrative`. Per-surface strings live in `product/surface-descriptors`. Page-level ownership lives in `product/seo-information-architecture`.

This decision supersedes the "repo memory" category-term carve-out and closes the open question in `product/messaging-and-voice`.

## Alternatives

- **Keep "repo memory" as the category term.** It wins an empty SERP and disambiguates the brand from archcore.com, but it contradicts the product definition on the highest-authority page and trains the reader on a frame the FAQ then denies. Rejected as positioning; the underlying content cluster survives as comparison content.
- **Context engineering only.** Drops the spec-driven acquisition path, where reader intent is high and the search is for a workflow rather than a concept. Rejected.
- **Spec-driven development only.** Collapses Archcore into the spec-generator category it is not, and contradicts Job 1 in `product/jobs-to-be-done`. Rejected.
- **No category claim, product definition alone.** The status quo that produced zero non-brand visibility. Rejected.

## Consequences

- **Spec-driven development becomes an acquisition category, not the primary product scenario.** Job ordering, first-run behaviour, demos, and hero proof stay Job-1-first per `product/jobs-to-be-done`. A surface that sells Archcore as a spec pipeline violates that document, not this one.
- `product/messaging-and-voice` drops "context engineering platform" from its avoid-list. The avoided shape is *platform*, not *context engineering*.
- The landing site retires "repo memory" from `<title>`, OG and Twitter cards, prerendered route bodies, `llms.txt`, and the RU catalog, and marks `landing/home-title-category-keyword.adr` superseded by this decision.
- The published memory-cluster articles (`blog/claude-code-memory`, `blog/cursor-memories-removed`, `learn/repo-memory`) keep their URLs and target keywords. Each gains a link to the canonical definition and stops asserting "repo memory" as what Archcore *is*.
- Two content programs now run against occupied heads. Ranking for them is a long play. The immediate return is entity consistency and clarity; long-tail acquisition continues through the wedges already identified in the landing research.
- Every surface changes together. The rollout order is `product/narrative-rollout`.
