---
title: "Adjacent Category Terms: Harness, Loop, and Prompt Engineering"
status: accepted
tags:
  - "messaging"
  - "product"
  - "web"
---

## Context

Three terms adjacent to Archcore's two discovery categories carry real search intent, and the question is whether any of them changes the positioning fixed by `product/two-discovery-categories`.

**Harness engineering** was named and systematized in early 2026. The canonical source is Birgitta Böckeler on `martinfowler.com`, which defines the harness as everything in an agent except the model, and splits it into **guides** (feedforward controls that steer before the agent acts) and **sensors** (feedback controls that check after), each in a computational or an inferential mode. Mitchell Hashimoto's shorthand, *Agent = Model + Harness*, is what carried the term. Several vendor posts (Faros, MindStudio, Milvus, Atlan) present a **prompt → context → harness** progression in which context engineering reads as superseded.

That progression is not what the cited source says. Böckeler states that context engineering provides the means to make guides and sensors available to the agent, and that engineering a harness for a coding agent is **a specific form of context engineering**. The two are nested, not sequential.

Archcore maps onto the taxonomy directly: the documents in `.archcore/` are guides, the pre-write hook is guide delivery at the moment of the edit, and `/archcore:review` against recorded decisions is an inferential sensor. The source does not name ADRs or repository storage as harness components, so that mapping is Archcore's claim, not Böckeler's.

**Loop engineering** designs the reason-act-observe-repeat cycle. IBM holds the definitional query. Archcore does not design the loop.

**Prompt engineering** is an occupied head (OpenAI, Anthropic, promptingguide.ai) and describes a different unit of work.

A brand collision also applies: the bare query *harness* belongs to Harness.io, the CI/CD company, the same way *archcore* belongs to a steel manufacturer.

## Decision

All three stay **adjacent terms**. The discovery categories remain exactly two.

- **Harness engineering** is sanctioned secondary vocabulary with a canonical owner page at `/learn/harness-engineering/`. Archcore is **a component of the harness, never a harness**. The claim Archcore makes is bounded: the host ships the loop, the tools, the permissions, and the sandbox; Archcore holds the project-specific guides and the criteria its sensors check against.
- **Loop engineering** is covered inside the harness page with an explicit boundary and gets no page of its own. A dedicated page would be a doorway page under `product/seo-information-architecture`.
- **Prompt engineering** appears only in comparison content, never as a description of what Archcore does.
- **Root pillar pages are reserved for the two primary categories. Adjacent and definitional terms live in `/learn/`.** This keeps one owner per query as the pillar system lands in P1.
- The homepage earns the harness term in the body of the context-engineering section, with a link to the explainer. The H1, the category line, and the two categories are unchanged.

## Alternatives

- **Harness engineering as a third discovery category.** Rejected on three grounds. It concedes the progression narrative that the weaker sources push, while the canonical source subordinates harness to context engineering. It inflates the category line and H1 past readability and forces a rewrite of every surface just aligned. And describing Archcore as a harness reads as an agent framework, which clause 5 of `product/canonical-narrative` forbids.
- **A dedicated `/loop-engineering/` page.** Rejected: the term is young and the competition thin, but Archcore's product fit is weak, so the page would be someone else's topic with a CTA attached.
- **Chasing the bare term *harness*.** Rejected: Harness.io owns it, and the qualified phrase is the winnable form.
- **Nothing on the homepage, page only.** Considered and not taken: it captures the query but forfeits an internal link from the site's highest-authority page, and the harness relation is genuinely explanatory where it now sits.

## Consequences

- `product/canonical-narrative` gains a clause fixing the component-not-category boundary, and `harness engineering` joins the secondary vocabulary in `product/messaging-and-voice`.
- `product/seo-information-architecture` gains the ownership row, the `/learn/` placement rule for adjacent terms, and the editorial entries.
- The landing homepage carries the term once, in body copy, in the context-engineering section.
- Any surface that adopts the prompt → context → harness progression contradicts this decision and the source it rests on. The correct framing is nesting.
- If harness engineering later absorbs context engineering in general usage, this decision is the one to revisit, and the evidence to watch is whether `martinfowler.com` changes its framing rather than whether vendor blogs do.
