---
title: "Document Tracks"
status: accepted
---

## Overview

Tracks are recommended multi-document flows. Most work doesn't need a single document in isolation — it moves from intent to decision to implementation, and the documents link into a chain. A track names that chain so the path is repeatable.

## The tracks

**Product** — `idea → prd → plan`. Explore a concept, define what to build, then plan the work. The lightweight default for features.

**Architecture** — `adr → spec → plan`. Record a technical decision, specify the contract it implies, then plan the implementation.

**Standard** — `adr → rule → guide`. Decide on a convention, codify it as an enforceable rule, then document how to follow it.

**Sources** — `mrd → brd → urd`. Discovery: market analysis, business justification, user needs — where requirements come from.

**ISO 29148** — `brs → strs → syrs → srs`. The formal requirements cascade (business → stakeholder → system → software) for contexts that need rigorous decomposition.

## How they connect

Documents in a track are wired with relations — typically `implements` and `depends_on` — so an agent loading the last document can walk back to the rationale behind it. Tracks are guidance, not gates: use the lightweight ones by default and the formal ones only when the rigor is warranted.

## Natural overall flow

`idea → prd → plan → adr → rule → guide → task-type / cpat` — vision becomes knowledge becomes experience.