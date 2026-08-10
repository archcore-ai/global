---
title: "Narrative Rollout Across Plugin, CLI, Landing, and Docs"
status: accepted
tags:
  - "messaging"
  - "product"
  - "web"
---

## Goal

Bring every public Archcore surface onto the narrative fixed by `product/two-discovery-categories`, `product/canonical-narrative`, `product/surface-descriptors`, and `product/seo-information-architecture`. No surface keeps a category term the others have retired.

Rollout order is P0 → P4. **P0 ships as one coordinated pass**, because a half-migrated set of surfaces is worse than the current state: the reader would meet three category terms instead of two.

## Status

**P0 executed 2026-08-10.** All file-level work in the four repositories is done and verified against the acceptance criteria below. Two groups remain open on purpose:

1. **P1 through P4**, which were always sequenced after P0.
2. **Two account-level items**: the GitHub organization profile README (its repository does not exist yet, so creating it publishes a new public repository) and the social bios on X, Bluesky, and LinkedIn, which are not reachable from this machine.

The homepage section restructure landed on the same day, after the meta pass. `landing.tsx` now runs the canonical sequence and the RU catalog is complete. The outward-facing GitHub metadata followed, on an explicit go-ahead.

Two facts were corrected in passing, in the opposite direction from the one expected: the docs site had already caught up with the shipped product, and the landing `messaging-alignment` rule was the surface carrying stale facts (a missing `/archcore:plan research` track, and a warning that the docs were a release behind).

## Tasks

### P0 — consistency (blocking; one pass)

**Global context (this repo) — done**

- [x] `product/two-discovery-categories.adr` — the decision, superseding the "repo memory" carve-out.
- [x] `product/canonical-narrative.rule` — fixed strings, message hierarchy, brand architecture, terminology.
- [x] `product/surface-descriptors.doc` — resolved copy per surface.
- [x] `product/seo-information-architecture.doc` — pillars, keyword ownership, page rules, editorial clusters.
- [x] `product/messaging-and-voice.rule` — avoid-list corrected, open question closed.
- [x] `product/messaging-playbook.rule` — hierarchy reordered around category-led vs benefit-led surfaces.

**CLI repo (`archcore-ai/cli`)**

- [x] `README.md` line 1 — H1 becomes `# Archcore CLI — Git-Native Context for AI Coding Agents`.
- [x] `README.md` logo placeholder comment — alt text already carries the correct tagline; leave it.
- [x] `README.md` first block — replace with the three-paragraph CLI block in `product/surface-descriptors`. The current opening sentence is already the product definition; the paragraphs after it must name specs, architecture decisions, rules, plans, and project knowledge.
- [x] GitHub repository description — set to the CLI repository description string.
- [x] GitHub topics — the canonical 13 plus `mcp-server`, `claude-code`, `cursor`. Removed `rag`, `graphrag`, `agent-memory`, `repo-memory`, which contradicted the positioning, and the vague `agent`, `ai`, `documentation`, `developer-platform`.
- [x] No code change needed for help text or banners: `@cmd/root.go:77`, `@internal/display/display.go:27`, `@internal/display/display.go:41`, and `@internal/mcp/server.go:14` already read "Git-native context for AI coding agents", which is the canonical ultra-short string. Verify, do not rewrite.
- [x] `AGENTS.md` and `CLAUDE.md` in the repo root — align any positioning sentence.

**Plugin repo (`archcore-ai/plugin`)**

- [x] `README.md` H1 — `# Archcore Plugin — Spec-Driven Development & Context Engineering for AI Coding Agents`.
- [x] `README.md` first block — replace the current "Make your AI code like it already knows your repo." opener and the two paragraphs after it with the plugin block in `product/surface-descriptors`, including the CLI-pairing paragraph.
- [x] Manifest descriptions — the string `Make your AI agent code with your project's architecture, rules, and decisions.` appears in **six** files and must change in all of them in one commit:
  - `@.claude-plugin/marketplace.json`
  - `@.cursor-plugin/marketplace.json`
  - `@plugins/archcore/.claude-plugin/plugin.json`
  - `@plugins/archcore/.cursor-plugin/plugin.json`
  - `@plugins/archcore/.plugin/plugin.json`
  - `@plugins/archcore/.codex-plugin/plugin.json`
- [x] `@.agents/plugins/marketplace.json` — check for a description field and align it.
- [x] Marketplace collection description (`Archcore plugins for AI coding agents`) — replace with the collection string in `product/surface-descriptors`.
- [x] GitHub repository description and topics — the canonical 13 plus `claude-code-plugin`, `codex-cli`, `plugin`, `subagents`, `ai-agents`. Removed `repo-memory` and the unhyphenated `spec-driven`.

**Landing (`archcore.ai`)**

- [x] `@index.html` — `<title>`, `name="description"`, `og:title`, `og:description`, `og:image:alt`, `twitter:title`, `twitter:description`, the `SoftwareApplication` JSON-LD description, and the static crawler fallback body inside `#root`.
- [x] `@src/components/sections/hero-section.tsx` — eyebrow, H1, subhead, supporting promise. The narrative line ("Specs define intent…") was left out of the hero to avoid four text blocks above the install tabs; it belongs in the homepage section restructure below.
- [x] `@src/components/sections/plugin-hero-section.tsx` and `@src/components/sections/cli-hero-section.tsx` — page H1s and subheads. `/plugin` now opens with the plugin README's first line; `/cli` replaced its "Repo memory" H1.
- [x] `@src/components/sections/migration-section.tsx` — its "What is repo memory?" link label was kept. It is the title of the `/learn/` explainer it points at, which is exactly the attributed-comparison case clause 16 allows.
- [x] `@scripts/prerender-routes.mts` — `ROUTES[]` titles, descriptions, and `body.h1` for `plugin` and `cli`. The `body.paragraphs` were reviewed and make no retired category claim, so they were left as written.
- [x] `@scripts/generate-og-image.mts` — `VARIANTS[]` headlines and subtitles must mirror the new page H1s and subheads.
- [x] `@public/llms.txt` — summary line rewritten to the product definition plus both categories.
- [x] `@src/locales/en/messages.po`, `@src/locales/ru/messages.po`, `@src/locales/en/messages.ts` — run `npm run i18n:extract`, translate new RU strings with formal «вы».
- [x] Homepage section sequence — restructured to the canonical sequence, plus Before/After kept between the problem and the two category sections as the Job 1 proof. New components: `problem-section`, `spec-driven-section`, `context-engineering-section`, `git-native-section`, `cross-agent-section`; `how-it-works-section` reworked from `init → write → agents read` to Capture → Connect → Apply → Evolve. The static crawler body in `@index.html` was rewritten so its H2s mirror the visible sections. Order and background rhythm recorded in the landing `messaging-alignment` rule.
- [x] `@.archcore/messaging-alignment.rule.md` — rewrite the canonical-phrase block to point at `product/canonical-narrative` and `product/surface-descriptors` instead of restating strings. Keep its per-surface enforcement checklist, the copy-layer list, and the host-matrix invariant, which have no equivalent in global.
- [x] `@.archcore/landing/home-title-category-keyword.adr.md` — set status to `rejected`, note that `product/two-discovery-categories` supersedes it.
- [x] `@.archcore/landing/seo-research-sdd-context-skills.rnd.md` — add a note that its "not winnable heads" recommendation was overridden as a positioning decision, and that its wedge findings still stand for the editorial program.
- [x] `@AGENTS.md` — the stable-terminology clause named "repo memory" as a pinned term; now names "project context".

**Docs (`docs.archcore.ai`)**

- [x] `@astro.config.mjs:97` — Starlight `title` was the lowercase wordmark `archcore`, used as an entity name. Now `title: 'Archcore'` with `titleDelimiter: '—'`, so every page reads `… — Archcore` per `product/seo-information-architecture`. The home page keeps its own full title via the frontmatter `head` override.
- [x] `@astro.config.mjs:107` — `starlightLlmsTxt` description contains "repo memory".
- [x] `@astro.config.mjs:122` — Starlight `description` contains "repo memory".
- [x] `@astro.config.mjs:167` — `WebSite` JSON-LD description carries the superseded "turns your repository into structured, machine-readable context" phrase.
- [x] `@src/content/docs/index.mdx` — frontmatter `title`, `description`, the `head` title override, the H1, and the intro paragraph. All four currently carry retired framing.
- [x] `@src/content/docs/start/migrate-from-flat-files.mdx` and `@src/content/docs/concepts/vs-flat-files.mdx` — both cross-link the `/learn/` explainer, which clause 16 allows. `migrate-from-flat-files` was reworded because it framed repo memory as what the reader migrates *to*, which is a positioning claim rather than a link.
- [x] `@.archcore/plain-language-and-seo.rule.md` — already compatible; added two clauses (take positioning wording from the shared rules; do not hand-write the brand suffix into a frontmatter title) and the cross-references.

**Cross-surface facts to reconcile in the same pass**

- [x] **This turned out to be false.** The docs had already caught up: Copilot is documented as implemented with both install steps and the `github/copilot-cli#4234` rationale, only the four commands appear, and the count says 19 types. The stale surface was the landing `messaging-alignment` rule itself, which still warned that docs were a release behind and listed only three `/archcore:plan` tracks while the shipped skill has four. Both corrected there.
- [x] Supported-agent lists must match across landing, docs, and both repository taglines. Landing's `plugin-hosts-section.tsx` and `cli-agents-section.tsx` remain the single source.
- [x] Command and track lists match: four slash commands, four positional tracks (`sdd`, `sources`, `iso`, `research`), no MCP prompts, 19 document types.

**Organization surfaces**

- [x] GitHub organization bio — was the superseded "turns your repository into structured, machine-readable context" phrase, now the canonical bio. The 422 on the first attempt was GitHub's 160-character limit, not a token scope.
- [x] GitHub organization profile README — `archcore-ai/.github` created public, `profile/README.md` live on the organization page. The draft's link to `/learn/harness-engineering/` was replaced with the `/learn/` hub before publishing: the article exists only in the local build, so a public profile would have pointed at a 404. Restore the direct link after the landing deploy.
- [ ] X / Bluesky bio, LinkedIn tagline and description.

**Surfaces found stale during the outward-facing pass (all fixed)**

- [x] `cli` welcome banner second line read "Context engineering for repositories", an uncanonical descriptor on the first thing a user sees. Now "Spec-driven development & context engineering", which carries both category terms without repeating the audience the first line already states (`@internal/display/display.go`).
- [x] `docs/README.md` opened with "System Context Platform that keeps humans and AI in sync with your system" — retired framing, and "platform" is on the avoid-list.
- [x] `docs/concepts/what-is-archcore.mdx` used the benefit phrase where the canonical product definition belongs, on the page that answers "what is Archcore". It now also states the specs-are-part-of-context relation.
- [x] `docs/cli/overview.mdx` said to use the CLI "when the plugin does not ship for your agent yet", which frames the CLI as a fallback and violates `architecture/one-product-two-entry-points`.
- [x] `docs/concepts/mental-model.mdx` introduced a third metaphor ("the CLI is the compiler"). Now leads with the canonical line and keeps engine/runtime as the elaboration.
- [x] `landing/README.md` carried the retired expanded explanation from the old messaging playbook.
- [x] `landing/public/llms.txt` plugin line omitted GitHub Copilot CLI, which ships since v0.7.0.
- [x] Docs counts verified consistent: eight agents over MCP, five with hooks, four plugin hosts, four commands, 19 document types.

**Repository descriptions also aligned beyond the two tool repos**

- [x] `archcore.ai`, `docs.archcore.ai`, and `global` had generic descriptions ("Official website Archcore AI") and no topics. All three now carry a category-bearing description, and the two site repositories carry topics.

**Rollback**: the pre-change GitHub metadata for all repositories is captured in the session scratchpad as `github-before.json`.

### P1 — category ownership

Build the pillar pages in `product/seo-information-architecture`, in this order:

- [x] `/context-engineering/`
- [x] `/spec-driven-development/`
- [x] `/project-context/`
- [x] `/git-native-context/`
- [x] `/mcp/`

Each ships with its own `<title>`, H1, meta description, first-paragraph primary term, a product connection near the top, internal links to sibling pillars, and technical depth. A pillar page without examples does not ship.

**Delivered 2026-08-10.** All five live at root paths, titles matching `product/seo-information-architecture` exactly.

Infrastructure, in `content-site/`:

- [x] A `pillars` content collection with its own schema: `heading` separate from `title` (SERP intent and visible H1 differ), `updatedDate` instead of `pubDate`, and a `related` list of sibling slugs.
- [x] `PillarLayout.astro` — `WebPage` structured data rather than `Article`, since these are evergreen reference pages with no publication event; plus `FAQPage`, an "On this page" contents list built from the h2 headings, a Related block, and the install CTA.
- [x] A root `[slug].astro` route. Sibling slugs resolve at build time, so a dead cross-link **fails the build** instead of shipping. This fired on the first build, as intended.
- [x] `[slug].md.ts` raw-markdown twins at `/<slug>.md`, matching the hub pattern and linked as `rel="alternate"`.
- [x] `scripts/merge-content.mts` derives pillar directories from the content folder rather than a hard-coded list, so adding a markdown file is all it takes to ship a page. It also copies the root-level `.md` twins, which the directory copy misses because they sit beside the page directory rather than inside it.

Internal linking:

- [x] Homepage sections link to their pillar with descriptive anchors: spec-driven → `/spec-driven-development/`, context engineering → `/context-engineering/`, git-native → `/git-native-context/`.
- [x] A "Reference" group in the footer carries all five, so `/project-context/` and `/mcp/` are reachable from every page and not only from siblings.
- [x] `llms.txt` gained a Reference section listing all five.
- [x] Pillars cross-link each other through `related`.
- [x] `/context-engineering/` links to `/learn/harness-engineering/` and states the nesting, which unblocks the item left open in P2.5.

### P2 — integration search (done 2026-08-10)

- [x] `/claude-code/`, `/cursor/`, `/codex/`, `/github-copilot/`, `/gemini-cli/`, each following the integration page formula, with non-identical titles and a host set that matches the shipped matrix.

Titles and H1s are the ones fixed in `product/seo-information-architecture`, and all five differ from each other. They reuse the P1 infrastructure: same collection, same layout, same route, so shipping them was five markdown files.

Each carries the host-specific facts rather than a template fill, taken from the shipped matrix in `plugin-hosts-section.tsx` and `cli-agents-section.tsx`:

- **Claude Code** — production plugin host, full hook set, compared with `CLAUDE.md` and Claude Code memory.
- **Cursor** — plugin on 2.5+, the one-time MCP config for marketplace installs, the CLI fallback below 2.5, compared with `.cursor/rules` and the removed Memories feature.
- **Codex CLI** — plugin on 0.117+, hooks behind `codex --enable hooks` and unavailable on Windows, so MCP is stated as the reliable path here. Compared with `AGENTS.md`.
- **GitHub Copilot** — the two required install steps and the `github/copilot-cli#4234` reason, plus the honest statement that pre-write injection is not available on this host and what to do instead.
- **Gemini CLI** — the CLI path with the full hook set, framed as a peer rather than a fallback, and the several-agents case.

- [x] Linked from the homepage cross-agent section, from `llms.txt` under a new "Agent integrations" section, and from sibling pages through `related`.

### P2.5 — adjacent terms (done 2026-08-10)

Bounded by `product/adjacent-category-terms`. Adjacent terms live in `/learn/`, not at the root.

- [x] `/learn/harness-engineering/` — the owner page for harness engineering and agent harness. Covers the guides-and-sensors taxonomy, the nesting relation to context engineering, a bounded section on loop engineering, and the prompt-engineering comparison table. Ships with FAQPage and Article JSON-LD.
- [x] Homepage — one paragraph in the context-engineering section, in both the React copy and the static crawler body in `@index.html`, linking to the owner page. H1, category line, and the two categories unchanged.
- [x] `@public/llms.txt` — new "Concepts and explainers" section covering `/learn/` and `/blog/`, which the file had never listed. Its plugin line also gained GitHub Copilot CLI, which was missing.
- [x] `/learn/` index title, description, and intro now name harness engineering.
- [x] `/context-engineering/` links to the harness page and states the nesting.

### P3 — comparison and migration intent (done 2026-08-10)

- [x] `/agents-md/` and `/claude-md/`, root pages in the same collection, framed as "Beyond X" rather than "X is bad": each opens with what the file gets right, names the three structural signals (scope, lifecycle, portability) that mean it has outgrown a flat file, and ends with a migration that does not require rewriting.
- [x] "AI agent memory vs project context" (`/learn/agent-memory-vs-project-context/`)
- [x] "Context engineering vs prompt engineering" (`/learn/context-engineering-vs-prompt-engineering/`), expanding the comparison table that `/learn/harness-engineering/` covered only partially
- [x] "Spec-driven development vs context engineering" (`/learn/spec-driven-development-vs-context-engineering/`)
- [x] Retrofit of the three memory-cluster pieces. All three keep their URLs and target keywords. `learn/repo-memory` now names Archcore by the canonical product definition rather than by the term; `blog/claude-code-memory` points its engineering-record sentence at `/project-context/`; `blog/cursor-memories-removed` links the new memory-versus-context piece, since the Memories removal is the concrete case that article argues from.

The two comparison pages sit at the root rather than in `/learn/` because they own a query cluster (`AGENTS.md alternative`, `CLAUDE.md alternative`) in `product/seo-information-architecture`. The three articles are definitional comparisons, which is what `/learn/` holds per the landing `messaging-alignment` rule.

Site totals after P3: **28 content pages, all titles unique**, 27 URLs in the sitemap, and a raw-markdown twin for every root and hub page.

### P4 — topical authority

- [ ] Publish the four editorial clusters in `product/seo-information-architecture` and interlink them to the pillars.

## Acceptance Criteria

1. `grep -ri "repo memory"` over `cli`, `plugin`, `landing`, and `docs`, excluding `node_modules`, `dist`, and `.git`, returns only comparison-page occurrences attributed to an alternative, plus the archived `.archcore/` decision records.
2. Every `<title>` across landing and docs is unique and carries the page's primary term.
3. The homepage `<title>`, H1, and meta description match `product/surface-descriptors` exactly.
4. The plugin description string is identical across all six manifest files and the GitHub repository description.
5. The CLI README H1, first block, and GitHub repository description match `product/surface-descriptors`.
6. No surface carries a recommendation label between the Plugin and the CLI.
7. Landing's `messaging-alignment` rule no longer restates canonical strings and links to the global rule instead.
8. `landing/home-title-category-keyword.adr` is marked superseded.
9. Landing prerendered bodies, OG images, and `llms.txt` carry the same claims as the rendered pages. Check `dist/`, not the dev server.
10. Docs state the shipped host matrix and the four-command surface.

## Dependencies

- `product/two-discovery-categories` — the decision this plan executes.
- `product/canonical-narrative` — the strings.
- `product/surface-descriptors` — the per-surface resolution.
- `product/seo-information-architecture` — P1 through P4 scope.
- `architecture/one-product-two-entry-points` — unchanged and still binding on every install surface.
- `product/jobs-to-be-done` — unchanged. Spec-driven development is a discovery category; Job 1 remains the primary product scenario, and hero proof, demos, and first-run stay Job-1-first.
- Landing i18n workflow — every visible string change requires `npm run i18n:extract`, RU translation, and a build.
- Docs content currency — the docs correction is a prerequisite for acceptance criterion 10, and it is a content backlog item independent of this narrative change.
