---
title: "Competitive Tracking: Tiers, Cadence, and Exclusions"
status: draft
tags:
  - "market"
  - "product"
---

## Summary

A proposal for which competitors Archcore actually tracks, how often, and what it
deliberately ignores. `market/competitive-landscape` inventories roughly ninety verified
entries. Tracking ninety is the same as tracking none.

Status is `draft`: the tiering below is a recommendation, not an accepted decision.

## Motivation

Three problems the inventory alone does not solve.

**The list has no priority.** A single-maintainer spec skill and an AWS IDE appear as
adjacent rows. They demand different responses.

**Snapshots decay.** Kiro reached GA in March 2026, Sourcegraph exited bottom-up pricing in
mid-2025, Vibe Kanban is sunsetting. A landscape document with no refresh obligation becomes
confidently wrong within a quarter — the failure mode `concepts/controlled-technical-writing`
rule 13 exists to prevent.

**Unbounded scope invites re-research.** Without a stated exclusion list, every new SDD
repository on GitHub reopens the question of whether it matters.

## Detailed Design

### Tier 0 — the first line

Nine entries. These are the only competitors whose feature changes should trigger a review of
Archcore's own roadmap.

Kiro · OpenSpec · Spec Kitty · ByteRover · PROJECTMEM · Sprintra · Tessl · Conductor (Google)
· GitHub Spec Kit

Selection rule: repo-native, explicit human-authored context, and either a vendor behind it
or an architecture that matches Archcore's four differentiating properties.

Note two departures from the source list this analysis started from. **ByteRover moves up** —
its Context Tree is typed, related, lifecycle-scored, and stored as plain markdown, which
makes it the closest architectural analogue in the landscape, not the fifth-closest.
**Conductor is added** — a first-party Google extension producing repo-resident context
artifacts was absent from the source list entirely.

Cadence: monthly. Check releases, docs, and pricing.

### Tier 1 — substitutes that reframe the buyer

Repowise · BMAD-METHOD · claude-mem · OpenMemory / Mem0 · Recallium · MemNexus · Sentra ·
Augment Context Engine · codebase-memory-mcp · LeanSpec · MoAI-ADK ·
`AGENTS.md` and the per-host rule formats

These do not threaten the mechanism. They threaten the framing — a buyer who names the
problem "my agent forgets" or "I already have a rules file" never reaches the comparison.

Cadence: quarterly, plus on any signal from
`market/commoditization-and-bundling-risks`.

### Tier 2 — standing signals, not products

Not tracked as competitors. Tracked as conditions.

- The `AGENTS.md` specification and Agentic AI Foundation roadmap.
- Per-host context features in Claude Code, Cursor, Copilot, Gemini CLI, Junie, Cline.
- Managed agent memory from AWS and Google.

Cadence: watched through the signals named in the risks document, not on a calendar.

### Explicitly not tracked

- The single-maintainer SDD long tail — `cc-sdd`, MetaSpec, gsd-core, colign, Cosmosmith,
  quint-code, fspec, dotdog, Shotgun, `pi-sdd-kit`, THROUGHLINE, `adversarial-spec`, VibeDoc,
  Task Master, `agent-skills`. Recorded in the inventory as evidence of category momentum.
  A single entry re-enters tracking on funding, vendor adoption, or a host integration.
- Architecture and documentation tooling — adr-tools, log4brains, MADR, Structurizr,
  IcePanel, Backstage TechDocs, Confluence, Notion, GitBook, Mintlify, Docusaurus. They
  compete for budget and attention, and neither moves on what Archcore ships.
- Harness and orchestration platforms, until Risk 4 shows a verified instance.
- General agent-memory infrastructure not shaped around code repositories.
- The sixteen unverified names. They re-enter only with a source.

### Refresh obligation

Each refresh restates the verification date at the top of
`market/competitive-landscape` and moves anything it could not re-verify into the unverified
section. A tier-0 entry that cannot be re-verified for two consecutive refreshes drops to
tier 1.

## Drawbacks

Monthly tier-0 review is real recurring work with no direct output. It is justified only
while Archcore's own roadmap is still open enough for a competitor's release to change it.

Excluding the long tail risks missing the project that becomes the next Spec Kit. The funding
and adoption triggers are the mitigation, and they are lagging indicators by construction.

The tiers encode a judgement about which competitors matter. That judgement is
`market/moat-parity-and-gaps`, and if that analysis is wrong the tiers inherit the error.

## Alternatives

**Track everything on one cadence.** Rejected. Ninety entries at any useful depth is a
full-time role.

**Track nothing; revisit annually.** Rejected. Three of the five commoditization risks are
already in progress, and two tier-0 entries changed materially within the last two quarters.

**Delegate to an automated watch.** Deferred, not rejected. Release feeds for nine
repositories would cover most of tier 0 mechanically. Worth building once the tiering itself
is accepted.
