---
title: "Layer 1 Command Surface Mapped to the Jobs"
status: rejected
tags:
  - "product"
---

## Summary

**Rejected — superseded by the shipped four-command surface.** This RFC proposed five Layer 1 verbs (`context`, `capture`, `plan`, `decide`, `health`) mapped onto `product/jobs-to-be-done`. The plugin instead collapsed the surface to **four** commands — `init`, `plan`, `document`, `review` — with a non-visible gated track layer beneath them. The shipped surface is normative in `plugin/.archcore/plugin/command-surface-v2.spec`; the reasoning is in `plugin/.archcore/plugin/four-command-palette.adr`. The ecosystem-level ownership split is recorded in `architecture/engine-runtime-boundary`.

The original proposal is kept below for the record.

## Motivation

The command surface is how the jobs become reachable. If a user's job is "ship this feature by this repo's rules", the first command they meet should answer exactly that, in their words.

At the time of writing the plugin shipped `audit`, `capture`, `context`, `decide`, `help`, `init`, `plan`. Four of the five proposed verbs already existed; the surface was not organised around the jobs, and `audit` named the activity rather than the question the user has.

## Detailed Design

| Command | Job it serves | The question it answers |
|---------|---------------|-------------------------|
| `/archcore:context` | 1 (primary), 2 (secondary) | "What rules, decisions, specs, and patterns constrain this area before I touch it?" |
| `/archcore:capture` | 3 | "This module / API / feature is undocumented — write it down as the right typed document." |
| `/archcore:plan` | 4 | "This change is too big for one file — lay out the artifacts and the steps." |
| `/archcore:decide` | 3 | "We chose X. Record it so the agent stops re-litigating it." |
| `/archcore:health` | — (maintenance) | "Where is my context thin, stale, or disconnected?" |

Changes proposed against the then-current surface:

1. `audit` → `health`. Same capability, renamed to the user's question.
2. `init` and `help` drop out of Layer 1 into a setup/discovery layer.
3. `context`, `capture`, `plan`, `decide` keep their names.

## Drawbacks

- Renaming `audit` breaks muscle memory, existing docs, and any external write-ups referencing it.
- "Health" is softer than "audit" and reads less like a check that can fail.
- Five commands still ask the user to choose. If Job 1 is genuinely primary, a smaller surface may convert better.

## Alternatives

- **Keep `audit`.** No rename, Layer 1 defined purely as a grouping.
- **Fold health into `context`.** Fewer verbs, muddier output.
- **Ship three.** `context`, `decide`, `plan` only.

## Why it was rejected

The third drawback proved decisive, and further than this RFC went. User research recorded the *system verbs* — `capture`, `decide`, `context`, `audit` — as the discovery bottleneck rather than the count, so renaming one of them did not address the problem. The shipped answer keeps only job-shaped verbs, absorbs `capture` and `decide` into `document`, absorbs `audit` into `review`, drops `context` in favour of automatic hook injection (`architecture/lifecycle-hooks`), and drops `help` into the command descriptions. Job coverage moved from command names to the gated track layer described in `concepts/gated-tracks`.
