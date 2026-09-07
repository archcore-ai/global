---
title: "Relation Conventions"
status: accepted
tags:
  - "concepts"
  - "vocabulary"
---

## Overview

The seven accepted relation types are named in `concepts/core-concepts`. This document is the conventions layer: which direction an edge points, which edge each recurring pair takes, and what a missing edge costs. Relations are what turn a folder of documents into a graph an agent can walk, so a wrong direction is not cosmetic — it sends the next reader the wrong way.

The CLI release that adds `supports`, `contradicts`, and `supersedes` remains pending — `product/research-direction`. Older binaries reject manifests containing these values; this change adds no downgrade conversion.

## Direction carries meaning

Every relation has a source and a target, and reversing them changes the claim. "plan implements prd" is true; "prd implements plan" is not.

**The direction rule:** the **more specific** document is the `implements` source, the **more general** one is the target. A PRD implements an idea; a plan implements the PRD; a BRS implements the BRD it formalizes. When unsure which end is which, ask which document could not exist without the other — that one is the source.

## Choosing the type

| Type | Use it when | Example |
|------|-------------|---------|
| `implements` | One document fulfils what another specifies | plan implements prd |
| `extends` | One document builds on another that stays valid | rfc extends adr |
| `depends_on` | One document requires another to make sense | plan depends_on adr |
| `related` | General association, or two peers at the same level | mrd related brd |
| `supports` | Material backs the target statement | evidence supports research |
| `contradicts` | Challenger disputes the target statement | evidence contradicts research |
| `supersedes` | Newer document replaces the older target | evidence supersedes evidence |

`related`, `implements`, `extends`, and `depends_on` are structural. `supports` and `contradicts` are evidential. `supersedes` is temporal. The engine accepts these values independently of document type or category.

`implements` and `extends` are easy to confuse. `implements` means the target stated a requirement and the source satisfies it. `extends` means the target stated a position and the source adds to it without replacing it.

## Canonical patterns

**Product flow**

```
prd  ──implements──→ idea
plan ──implements──→ prd
plan ──depends_on──→ adr
```

*An idea became requirements, the requirements became a plan, and the plan is constrained by decisions made along the way.*

**Decision to standard**

```
rfc  ──extends────→ adr    (a proposal against an existing decision)
adr  ──related────→ rule   (the decision produced a standard)
rule ──related────→ guide  (the standard has a how-to)
```

**Experience**

```
task-type ──depends_on──→ rule   (the task follows this standard)
cpat      ──extends─────→ rule   (the pattern change updates this standard)
```

**Requirements cascade**

```
brs  ──implements──→ brd   (the specification formalizes the source)
strs ──implements──→ brs   (each ISO level implements the previous)
syrs ──implements──→ strs
srs  ──implements──→ syrs
```

Three conventions govern this one, and they are the ones most often broken. Same-layer documents link with `related`, not `implements` — an `mrd` and a `brd` are peers. A `prd` links to an ISO type with `related`, because it is an alternative path rather than a formalization of one. Partial cascades are valid: a project that skips the middle levels links `srs implements brs` directly. The full formalization map is in `concepts/requirements-layers`.

**Research**

An `rnd` does not take `implements` by convention. Use `idea related rnd`, `plan depends_on rnd`, and `adr depends_on rnd`.

A `research` takes neither `implements` nor `extends` by convention. Use `rnd depends_on research` for a decision-bound investigation that relies on territory discovery. Both types belong to vision. An `evidence` belongs to knowledge and can support or contradict either investigation.

These patterns are authoring conventions, not type restrictions. Creating an evidential or temporal relation does not change a document's status or resolve a contradiction. Record the resolution in the disputed document's prose.

## Relations are never automatic

Creating a document links it to nothing. No tool infers a relation, and none is created as a side effect of a write — the semantic claim an edge makes is the author's to assert, and a guessed edge is worse than a missing one because it reads as deliberate.

A document that ends a session unlinked stays unlinked. That is the common failure: the document is correct, findable by search, and invisible to anyone walking the graph from a neighbouring document. Health checks surface orphans for this reason.

## Storage

Relations live in the sync manifest beside the documents, not inside the document files, and the manifest is tracked in Git so the graph travels with the repository. Frontmatter carries no relation fields. The manifest is tool-managed: change relations through the MCP tools, never by editing the file.

Keeping edges out of the documents is deliberate — a relation is a claim about a pair, and storing half of it in each file would let the two halves disagree.
