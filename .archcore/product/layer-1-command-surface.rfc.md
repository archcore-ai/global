---
title: "Layer 1 Command Surface Mapped to the Jobs"
status: draft
tags:
  - "product"
---

## Summary

Reshape the plugin's Layer 1 — the command surface a user learns first — into five verbs that map one-to-one onto the jobs in `product/jobs-to-be-done`:

- `/archcore:context` — what do I need to know before changing this area
- `/archcore:capture` — document a module, folder, API, feature, or the whole project
- `/archcore:plan` — break a change down before implementing it
- `/archcore:decide` — lock a decision so the next code accounts for it
- `/archcore:health` — coverage, drift, stale docs, graph gaps

## Motivation

The command surface is how the jobs become reachable. If a user's job is "ship this feature by this repo's rules", the first command they meet should answer exactly that, in their words.

Today the plugin ships `audit`, `capture`, `context`, `decide`, `help`, `init`, `plan`. Four of the five proposed verbs already exist; the surface is not currently *organised* around the jobs, and `audit` names the activity rather than the question the user has ("is my context healthy — where are the gaps?").

Naming the set explicitly as Layer 1 also makes the split visible: `init` and `help` are setup and discovery, not day-to-day work.

## Detailed Design

| Command | Job it serves | The question it answers |
|---------|---------------|-------------------------|
| `/archcore:context` | 1 (primary), 2 (secondary) | "What rules, decisions, specs, and patterns constrain this area before I touch it?" |
| `/archcore:capture` | 3 | "This module / API / feature is undocumented — write it down as the right typed document." |
| `/archcore:plan` | 4 | "This change is too big for one file — lay out the artifacts and the steps." |
| `/archcore:decide` | 3 | "We chose X. Record it so the agent stops re-litigating it." |
| `/archcore:health` | — (maintenance) | "Where is my context thin, stale, or disconnected?" |

Changes from the current surface:

1. `audit` → `health`. Same capability, renamed to the user's question. Coverage, drift, stale docs, and graph gaps become the stated outputs.
2. `init` and `help` drop out of Layer 1 into a setup/discovery layer. They are still shipped; they are just not what the surface is *organised around*.
3. `context`, `capture`, `plan`, `decide` keep their names — they already read as the jobs.

Open questions, to settle before this moves to accepted:

- Is `audit` renamed outright, or kept as an alias for one release?
- Does `capture` cover whole-project bootstrap, or does that stay with `init`?
- Is five already too many for a first-run surface, given Job 1 dominates the ranking?

## Drawbacks

- Renaming `audit` breaks muscle memory, existing docs, and any external write-ups referencing it.
- "Health" is softer than "audit" and reads less like a check that can fail — a real cost for a command whose output is a gap list.
- Five commands still ask the user to choose. If Job 1 is genuinely primary, a smaller surface may convert better.

## Alternatives

- **Keep `audit`.** No rename, and Layer 1 is defined purely as a grouping. Cheapest; keeps the verb precise, loses the question-shaped naming.
- **Fold health into `context`.** One command that reports both what applies here and what is missing. Fewer verbs, muddier output.
- **Ship three.** `context`, `decide`, `plan` only — matching jobs 1–4 minus maintenance, with capture folded into decide. Sharpest first-run story, weakest coverage story.
