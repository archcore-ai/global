---
title: "Gated Tracks: the Runtime Workflow Model"
status: accepted
tags:
  - "architecture"
  - "concepts"
---

## Overview

A **gated track** is a short chain of gates that a runtime command routes into, producing typed, linked documents. It is the runtime's answer to "how does a request become the right documents without a taxonomy quiz". The runtime owns tracks (`architecture/engine-runtime-boundary`); this document defines the model at the concept level so consumers — the docs site, the landing, a second runtime — describe it the same way. The normative gate contract lives in `plugin/.archcore/plugin/track-layer.spec`.

Do not confuse this with a **document track** (`concepts/document-tracks`), which is a recommended cascade of document types. See "Two senses of track" below.

## The model

- A **command** is what the user sees. The surface is four verbs: `init`, `plan`, `document`, `review`.
- A **track** sits beneath a command and is never shown as a menu. Routing selects it from signals, in a fixed order: an explicitly named track, the state of the document graph, the state of the branch, then the wording of the request.
- A **gate** is one stage of a track: entry conditions, a bounded set of questions, the document it produces, and exit checks that are either blocking or advisory.

## Governing behaviors

- The user is never asked to choose a track. Vagueness of the request sets the **question budget**, not the routing.
- A gate that finds its entry conditions already satisfied by existing documents or by the request text asks **zero** questions. A fully specified request runs question-free.
- A document a gate produces is created as a **draft**. Promotion to accepted is a separate, explicitly confirmed step — never a side effect of a hook or a gate.
- Track state lives inside the draft artifact, so an interrupted flow **resumes** in a later session at the earliest gate whose exit checks have not passed, without re-asking answered questions.
- Every one of the 19 document types is reachable through at least one track.

## The catalog

| Track | Shape | Command |
|-------|-------|---------|
| `sdd` | frame → require → design → decompose | `plan` |
| `requirements-cascade` | sources mode: mrd → brd → urd · ISO mode: brs → strs → syrs → srs | `plan` |
| `research` | frame questions → gather evidence → conclude with a recommendation | `plan` |
| `decision` | classify → adr or rfc → cascade (plus a resolution entry on an existing rfc) | `document`, callable from all |
| `describe` | read the code → draft spec/doc/guide → clarify gaps | `document` |
| `actualize` | scope the diff → verdict per finding → confirmed fixes | `review` |
| `closeout` | verify the plan against the branch → merge the canon → transition statuses | `review` |
| `experience` | detect a repeated pattern → offer a cpat or task-type | `review` |

## Two senses of track

| | Document track | Gated track |
|---|---|---|
| What it is | A recommended chain of document *types* | A runtime flow of *gates* |
| Where it lives | The shared vocabulary (`concepts/document-tracks`) | The runtime (this document) |
| Who follows it | Any agent, with or without the runtime | The runtime's command skills |
| Example | `adr → rule → guide` | `decision` (classify → adr → cascade) |

The gated tracks *implement* several document tracks and do not replace them: `requirements-cascade` carries both the Sources and the ISO document tracks, `decision` carries the Architecture and Standard tracks, and `sdd` covers the Product track with a design stage added. A CLI-only user still follows document tracks by hand; they lose the gates, not the cascades.

## Why gates rather than commands

Every earlier surface expanded one command per flow, and each expansion recreated the same failure: two commands that both plausibly match a request, and a user who must first learn the taxonomy to pick one. Gates move the branching below the surface, where routing evidence — the graph, the branch, the wording — is available and the user's vocabulary does not have to match ours.
