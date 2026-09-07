---
title: "Document Tracks"
status: accepted
tags:
  - "concepts"
  - "document-types"
---

## Overview

Tracks are recommended multi-document flows. Most work doesn't need a single document in isolation — it moves from intent to decision to implementation, and the documents link into a chain. A track names that chain so the path is repeatable.

This document defines **document tracks**: cascades of document *types*, part of the shared vocabulary and followed by any agent, with or without the runtime. The runtime's gated flows are a different thing that reuses the word — see `concepts/gated-tracks`.

For picking the right *type* at each step, see `concepts/document-types-reference`; for the Sources-vs-Specifications layering that the requirements tracks rest on, see `concepts/requirements-layers`.

## The tracks

**Product** — `(rnd) → idea → prd → plan`. Explore a concept, define what to build, then plan the work. The lightweight default for features. `rnd` is an optional research gate — used only when a question must be resolved first (is this worth exploring? is it feasible? which approach?).

**Architecture** — `adr → spec → plan`. Record a technical decision, specify the contract it implies, then plan the implementation.

**Standard** — `adr → rule → guide`. Decide on a convention, codify it as an enforceable rule, then document how to follow it.

**Sources** — `mrd → brd → urd`. Discovery: market analysis, business justification, user needs — where requirements come from.

**ISO 29148** — `brs → strs → syrs → srs`. The formal requirements cascade (business → stakeholder → system → software) for contexts that need rigorous decomposition.

## Research vocabulary

The accepted vocabulary adds `research` in vision and `evidence` in knowledge — `concepts/research-and-evidence-types`. CLI v0.8.3 (2026-09-07) ships both types and the three relations; plugin v0.8.3 (2026-09-07) ships the runtime routes.

`evidence supports research` links a reusable material to a territory investigation. `rnd depends_on research` links a decision-bound investigation to that territory. These are document conventions, not additional execution gates; the existing Product flow remains valid.

## How they connect

Documents in a track are wired with relations — typically `implements` and `depends_on` — so an agent loading the last document can walk back to the rationale behind it. Tracks are guidance, not gates: use the lightweight ones by default and the formal ones only when the rigor is warranted.

The Sources and ISO tracks are two **layers**, not rivals: sources discover requirements informally; ISO specs formalize them. They are linked `spec implements source` (e.g. `brs implements brd`). PRD is a pragmatic hybrid that can stand in for the full ISO cascade — see `concepts/requirements-layers`.

## Natural overall flow

`idea → prd → plan → adr → rule → guide → task-type / cpat` — vision becomes knowledge becomes experience.

## How the runtime walks them

The runtime does not expose these names. It routes a request into a gated track that carries one or more of these cascades: `requirements-cascade` carries Sources and ISO, `decision` carries Architecture and Standard, `sdd` covers Product with a design stage added. The cascades above stay canonical — the gated tracks are one way of walking them, not a replacement.
