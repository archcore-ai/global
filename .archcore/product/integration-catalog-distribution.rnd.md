---
title: "Integration Catalog Distribution: Landing, Docs, and Search"
status: accepted
tags:
  - "integrations"
  - "product"
  - "web"
---

## Goal

Choose the distribution surface and search architecture for a curated catalog of Archcore integration recipes. Compare the landing project at archcore.ai with the documentation project at docs.archcore.ai. Preserve the user's Archcore-centered offering, existing-harness installation, and choice of command entry.

This investigation is dated 2026-09-08. The user accepted its distribution direction on the same date. Acceptance does not establish a published catalog, tested recipe compatibility, or measured acquisition growth.

## Questions

1. Which surface best serves discovery, evaluation, setup, and ongoing use?
2. What does the existing implementation already support, and what needs extension?
3. Which pages merit separate searchable URLs without duplicating existing host pages or documentation?
4. How can one recipe connect a public listing, installable instructions, verification evidence, and a future assembler?
5. What observations would justify expanding the catalog or changing the recommendation?

## Approach

Inspect local code, accepted product constraints, and existing integration research. Compare first-party catalog and documentation examples. Check current Google documentation for crawling, rendering, duplicate content, and sitemap behavior. Sample problem-oriented searches for Superpowers, OpenSpec, and grill-me.

The landing checkout was clean at a1bb203; docs was clean at 7b1f9c1. The local MCP corpus is global only, so sibling code and documents were read from the filesystem. No website code was changed or built.

### Inputs

All web sources were accessed on 2026-09-08. Source rows describe what was inspected, not measured market performance.

| ID | Material | Use and limit |
|---|---|---|
| U1 | User instructions in this conversation | Archcore-centered recipes; Markdown MVP; optional cooperation; investigate landing versus docs |
| U2 | User confirmation on 2026-09-08: “ок. давай так и запишем” | Accepts catalog placement, landing/docs roles, shared recipe source, and the Superpowers pilot direction |
| U3 | User clarification on 2026-09-08: the solution should be usable by users of any harness | Product scope is harness-independent; research remaining delivery uncertainties rather than select one exclusive pilot host |
| G1 | Accepted global SEO information architecture and surface descriptors, retrieved through MCP | Existing query ownership, product positioning, and page boundaries |
| G2 | Existing integration ecosystem and recipe MVP investigations, retrieved through MCP or inspected locally | Draft marketplace direction, four candidate recipe records, bounded verification |
| G3 | Accepted static hosting decision, retrieved through MCP | GitHub Pages is the current static-web hosting boundary |
| L1 | @landing/package.json; @landing/content-site/astro.config.mjs; @landing/content-site/src/content.config.ts; @landing/content-site/src/pages/learn/[slug].astro | Current Vite plus Astro composition and static content collections |
| L2 | @landing/scripts/merge-content.mts; @landing/scripts/prerender-routes.mts; @landing/.github/workflows/deploy.yml | Deployment sections, sitemap generation, static route ownership |
| L3 | @landing/content-site/src/layouts/ListingLayout.astro; @landing/content-site/src/layouts/PillarLayout.astro; @landing/content-site/src/components/SiteHeader.astro | Existing listing markup, metadata, navigation, and content shell |
| L4 | @docs/astro.config.mjs; @docs/src/components/Head.astro; @docs/src/lib/analytics/; @docs/AGENTS.md | Static documentation, Starlight navigation, search instrumentation, metadata and machine-readable sets |
| L5 | @landing/src/lib/analytics/events.ts; @landing/src/lib/analytics/core.ts | Existing copy and navigation events; cross-subdomain cookie setting; no measured recipe funnel |
| L6 | Landing's accepted content-hub Astro sub-build ADR, inspected in the sibling corpus | Reuse the implementation decision; challenge its categorical subdomain-authority rationale |
| S1 | [Google SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide) | Business-based domain organization and content guidance; no guarantee of rankings |
| S2 | [Google site navigation guidance](https://developers.google.com/search/docs/specialty/ecommerce/help-google-understand-your-ecommerce-site-structure) | Crawlable links and navigation hierarchy; apply catalog principles by analogy |
| S3 | [Google faceted navigation guidance](https://developers.google.com/crawling/docs/faceted-navigation) | Prevent filter-generated URL expansion |
| S4 | [Google rendering guidance](https://developers.google.com/search/docs/crawling-indexing/javascript/dynamic-rendering) | Static rendering and hydration as alternatives to bot-specific rendering |
| S5 | [Google sitemap guidance](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) | Accurate significant-update dates |
| S6 | [Google spam policies](https://developers.google.com/search/docs/essentials/spam-policies) | Low-value mass-generated pages are a content risk |
| S7 | [n8n integration catalog](https://n8n.io/integrations/), [GitHub listing](https://n8n.io/integrations/github/), [integration docs](https://docs.n8n.io/integrations/) | Observable division between discovery and operation; no conversion data |
| S8 | [Superpowers issue 1515](https://github.com/obra/superpowers/issues/1515) | One user's request for persistent project knowledge; closed as duplicate; not a demand estimate |
| S9 | [Live Archcore content page](https://archcore.ai/learn/harness-engineering/), [docs home](https://docs.archcore.ai/) | Browser-fetchable content and navigation; not a Google index inspection |

The investigation also inspected Vercel Marketplace and skills.sh documentation as adjacent distribution examples. Their presence does not establish the effectiveness of an Archcore catalog; the recommendation does not depend on their adoption claims.

Coverage limits: Search Console, keyword volumes, backlink profiles, PostHog results, field performance, and user studies were not obtained. Direct shell HTTP requests failed at DNS resolution in this environment; web retrieval of the robots and sitemap URLs returned tool errors. Those failures are not evidence of a website outage. Live robots, sitemap status, canonical selection, and indexing remain unverified. Local configuration and selected public page content were inspected.

## Findings

### 1. Landing is the preferred discovery surface; docs remains a viable alternative

The accepted direction places the initial catalog at archcore.ai/integrations/ and uses docs.archcore.ai for operational material. U2. The reason is fit with the product journey and the existing Astro content build. Search traffic superiority has not been established.

| Option | Benefit | Cost or limitation | When to choose |
|---|---|---|---|
| Catalog and all recipe guidance in landing | One destination from discovery to first use; one publishing surface | Long platform-specific maintenance guidance adds work to the marketing content system | A small pilot with short instructions |
| Catalog entirely in docs | Existing documentation authoring, search, and navigation; fewer publishing surfaces | Discovery cards and configuration comparison need a separate presentation within the docs shell | Existing-user activation is the primary job, or docs has measured acquisition strength |
| Catalog in landing, operational guidance in docs | Product evaluation stays in the catalog; detailed setup fits the docs structure | Content ownership and release synchronization need explicit handling | Accepted direction for a growing catalog |
| Independent marketplace site | Separate identity and product operation | Another domain, build, navigation system, and publishing responsibility | Only after a distinct marketplace business is demonstrated |

The recommendation is the third option with a small pilot that can resemble the first: include the complete short Markdown setup on the listing, and link to existing docs for tool installation. A duplicate per-recipe docs page is unnecessary until it answers additional operational questions [assumption].

S7 demonstrates the separation: n8n exposes discovery pages on its main site, and its GitHub integration listing links to node and credential documentation on docs.n8n.io. This is an implementation precedent, not a causal SEO experiment.

### 2. Domain location does not establish a ranking advantage

S1 treats subdomains versus subdirectories as a business and organization choice. S2 emphasizes links between pages when explaining how Google understands relative page importance. Together they do not justify the claim that a docs subdomain automatically loses authority.

L6 contains that stronger claim as rationale for the already accepted Astro sub-build. This investigation retains the useful implementation boundary but does not use that claim as evidence. No controlled Archcore comparison, backlink analysis, or search performance data supports it here.

[assumption] A main-site catalog can benefit from links from product pages, relevant articles, and external integration descriptions. Docs can also receive these links. A cohesive visitor journey and clear page ownership are the reasons to prefer landing in this case.

This investigation does not amend L6. Its rationale merits a targeted correction when the distribution choice is formalized.

### 3. The existing landing already has a static catalog foundation

L1 shows that landing is more than a React SPA. Its Astro subproject already generates Markdown-backed pages for blog, learn, alternatives, and root-level pillars. L3 supplies a static listing layout with normal links, canonical URLs, CollectionPage and ItemList metadata, and a shared visual shell.

[assumption] Add an integrations collection and dedicated listing/detail layouts within content-site. Reuse the shell and metadata conventions. Add browser behavior only for filtering, host selection, and copying instructions; the unfiltered catalog and substantive detail content remain present in initial HTML.

This direction is consistent with S4's rendering guidance. It does not require migrating the SPA or changing hosting.

Concrete extension points:

- L2 copies only blog, learn, alternatives, detected pillar directories, and Astro assets. A new integrations subtree needs explicit inclusion or a generalized content-section registry.
- Static detail paths need generation from publishable records. A path handled only by the SPA fallback does not establish the catalog's HTML contract.
- Navigation needs a catalog link in the relevant React and Astro surfaces, plus contextual links from host pages and docs.
- Existing layouts are article and pillar oriented. Integration pages need prerequisite, behavior, support-scope, and setup fields instead of a forced article publication shape.
- Sitemap lastmod currently uses the build date in both prerender and merge scripts. S5 calls for the last significant page update. A catalog needs content-derived dates; verification date remains a separate field.
- L5's ContentSection union does not include integrations. Recipe attribution needs an explicit extension rather than classifying every recipe as an article.

The local robots files allow crawling and point to sitemap URLs. These are source observations; live output checks remain a pilot acceptance item.

### 4. Searchable pages represent user jobs and released combinations

[assumption] Start with an integrations index and one or two substantive recipes. A page earns a URL through distinct guidance, behavior, and evidence. Installing two tools is not sufficient content for a claim that their cooperation has been verified.

Proposed query ownership:

| Visitor intent | Proposed owner | Boundary |
|---|---|---|
| Find an Archcore setup for tools I already use | archcore.ai/integrations/ | Catalog and selection |
| Use Superpowers with persistent project context | archcore.ai/integrations/superpowers/ | Archcore + Superpowers behavior, prerequisites, evidence, quick setup |
| Use OpenSpec with Archcore | archcore.ai/integrations/openspec/ | Native specification ownership and Archcore contribution |
| Preserve decisions from Matt Pocock's grill-me | archcore.ai/integrations/grill-me/ | Interview input reuse and knowledge capture |
| Add FPF to an Archcore + Superpowers setup | A section on the Superpowers page initially | A separate URL only after distinct guidance and combination-specific tests exist |
| Configure Archcore in Claude Code or another host | Existing root host pages and linked setup docs | Preserve accepted host query ownership; avoid a second competing host landing page |
| Diagnose or update an installed recipe | A distinct operational docs page when required | Task guidance, not a duplicate marketing listing |

The catalog index and Superpowers pilot location were accepted in U2. Other URLs and intents remain design candidates. None of these entries establishes a publication date or measured keyword opportunity. Context7, Graphify, and FPF remain candidates subject to the same content and verification criteria.

S8 provides a narrow signal: one Superpowers user requested durable project context and standards on May 11, 2026. The issue was closed as duplicate. It supports exploring the pain point; it does not establish frequency, willingness to install Archcore, current Superpowers capability, or maintainer endorsement.

[assumption] Early acquisition can target the external tool plus the problem, since someone who has never encountered Archcore may not search for Archcore + tool. Each page then explains the specific Archcore contribution. Titles retain the exact product identity; grill-me names Matt Pocock and links to the upstream repository to distinguish forks.

A content-rich experimental report can be useful in search when labeled accurately. Empty future listings and a generated matrix of tool × host × version pages add no corresponding evidence. S6 identifies mass production of low-value pages for rankings as problematic.

### 5. A recipe page is both an explanation and a usable distribution endpoint

[assumption] The primary page sequence is:

1. State the problem and the contribution of Archcore to the selected tool.
2. Show participating tools, required host capabilities, and the exact scope of verification.
3. Explain what happens from each supported entry point, including Archcore's own skills.
4. Show where specifications, plans, and accepted decisions remain, with one concrete task example.
5. Provide the available setup instructions, their revision, and a preview of the configuration change.
6. Link to verification results, limits, update/removal instructions, and operational docs.

A compact summary can show the verification date and environment; expanded records identify host, model, tool revisions, recipe revision, scenarios, and interventions. Editorial update date and last successful scenario execution are different facts. A newly edited page does not acquire a newly verified status.

[assumption] For an existing harness, the action applies the recipe after prerequisite checks. For a new setup, it first directs the user through dependency installation. Before an assembler exists, the page distributes the actual Markdown fragment and manual instructions; it does not display an invented working CLI command.

A request involving Archcore + Superpowers + FPF uses the tested scope of that specific combination. Passing separate pair tests does not produce an automatic triple compatibility claim. No marketplace selection forces Archcore to own the user's process; a user's explicit skill entry keeps its task.

### 6. Separate the public URL from the recipe's release identity

G2 proposes four small records: the recipe card, cooperation instructions, evaluation scenarios, and evaluation results. The website can present these records before a universal machine-readable manifest exists.

[assumption] Use one authored source for each installable instruction fragment and one revision-linked evidence record. The catalog presents their data and explanatory text; docs adds distinct operational guidance. Avoid independently editable copies of the same instructions on both sites.

[assumption] The later assembly path is: reviewed recipe records produce a versioned distribution artifact; the catalog renders the selected release; the assembler consumes the same release. A static JSON index and downloadable Markdown are sufficient candidate delivery formats for a pilot. The source repository and exact schema remain open.

A stable public page can describe current recommendations while linking to immutable release material. Updating search copy does not silently change what a pinned recipe installs. Cross-site publishing can use a pinned snapshot so a catalog build cannot advertise evidence belonging to a different instruction revision [assumption].

This preserves an exit from landing-specific storage. A future assembler need not parse marketing HTML. A future marketplace does not require a database, accounts, or an open submission platform to begin distribution.

### 7. SEO constraints apply to the catalog's content and navigation

[assumption] Initial indexable content consists of the catalog and substantive recipe pages with direct links between them. Filter controls can operate on the already rendered list; no separate indexable URL is created for every host, status, or tool permutation.

S2 states that a search box is not a reliable discovery path for Googlebot. S3 documents URL expansion from faceted navigation. Applying those principles here means real href links to recipes, and deliberate decisions about which filtered collections deserve public pages.

[assumption] A later curated category page gets its own URL only when it answers a distinct selection question. The pilot does not expose arbitrary configuration selections as indexable documents.

Each distinct catalog or operational docs page uses its own canonical URL. Two pages about the same integration can serve different intents. Canonicalizing detailed docs to a shorter marketing card would not express that distinction [assumption]. Identical content is better consolidated before publishing two owners.

[assumption] Metadata describes visible content: CollectionPage with ItemList on the catalog, and WebPage with breadcrumbs on detail pages. The colloquial term recipe does not imply food Recipe markup. Search-result enhancements, ratings, and compatibility claims are not invented from metadata.

Before publication, inspect built HTML and real deployed responses for links, content, metadata, status codes, and sitemap inclusion. Verify a nonexistent integration path as well: a product-looking SPA fallback is not a useful catalog error experience. This is proposed validation, not a report of an observed live failure.

### 8. Distribution starts with a demonstrated result

[assumption] The acquisition path is a problem-specific explanation or upstream ecosystem link, followed by a recipe page, prerequisite/setup action, a successful task in the user's harness, and later reuse of the saved project knowledge.

The page provides a stable destination for a demonstration, repository README reference, release note, or permitted upstream directory entry. These are candidate channels. No external post, message, submission, or partnership claim was made in this investigation.

L5 already defines copy, CTA, and navigation events; its runtime enables a cookie shared across subdomains. This is a code foundation for measurement, not proof that the full funnel currently works.

[assumption] Measure distinct stages:

| Stage | Candidate observation | Interpretation limit |
|---|---|---|
| Search discovery | Search Console impressions, queries, and clicks per recipe page | Queries and exposure; not installation |
| Evaluation | Catalog-to-detail visits and setup actions by recipe and referring page | Interest; not successful use |
| Setup | Instruction copy or recipe download, with recipe ID and revision | Acquisition intent; not completed installation |
| Activation | Observed successful scenario in a participating pilot project | Evidence limited to that environment |
| Continued value | A subsequent task retrieves and uses relevant preserved knowledge | Stronger adoption signal; requires task evidence |
| Maintenance | Time spent refreshing recipe guidance and rerunning affected checks | Operating cost of advertised support |

Browser analytics alone cannot establish that a copied Markdown fragment was installed or used correctly. Pilot observations can supply that missing evidence without first adding runtime telemetry [assumption].

## Recommendation

**Refine, accepted by the user on 2026-09-08.** Place a curated catalog in landing at archcore.ai/integrations/, implemented through the existing Astro sub-build, with docs retaining operational guidance. Findings 1–3 support the surface choice. Findings 4–7 define a restrained publishing and delivery model. Finding 8 separates discovery from demonstrated value.

The recommendation assumes that the next objective is acquisition and activation through Archcore-centered combinations. It changes if docs already supplies materially stronger relevant traffic and an experiment shows that moving through the catalog reduces completed setup, or if coordinating two content surfaces costs more than the recipes justify.

The accepted first pilot is Archcore + Superpowers, which already has a candidate recipe design; S8 adds a concrete problem report. U2. Select another recipe only after its behavior can be demonstrated. Publish the actual level of checking; no combination has been executed as part of this investigation.

The first deliverable is a usable recipe page and its evidence. Catalog breadth, native marketplace packaging, advanced filtering, community submissions, and a general assembler remain separate expansion hypotheses.

## Next Action

The first recipe now lives in @plugin/integrations/superpowers/ and is connected through the plugin repository's instructions. Use it on real plugin tasks first. Use those observations to shape the catalog index, Superpowers detail page, and the snapshot fields they actually need. Website construction can then run alongside broader cooperation and installation checks with truthful evidence labels. Obtain combined scenario results before advertising tested cooperation.

[assumption] Review discovery and setup observations after an initial 4–8 week publishing period. This is an operational checkpoint, not a promise that Google will rank the pages by then. With too little exposure, inspect indexing and distribution before treating weak traffic as rejection of the recipe.

## Open Gaps

- Search Console and PostHog baselines for both sites, and the acquisition contribution of existing host and content pages.
- Keyword volume, region and language priorities, referring-domain profiles, and the size of each tool's addressable audience.
- Representative host/model environments, exact tool revisions, and actual dual-entry scenario results, including the manual connection path for an unrecognized harness.
- The source repository, release identity, evidence artifact format, and publication synchronization mechanism.
- Whether the short instructions fit entirely on the listing or need a distinct per-recipe operational page.
- Live sitemap, robots, HTTP status, canonical selection, index coverage, and built-output verification for future catalog routes.
- The maintenance capacity needed to keep public support claims current.
- A targeted correction to the old categorical subdomain-authority rationale; the accepted static sub-build choice itself is supported by current code.

## Clarifications

The user first requested a comparison of landing and docs, then accepted the recommended distribution direction on 2026-09-08. The selected catalog lives at archcore.ai/integrations/ through the existing landing Astro build; short setup stays on recipe pages, and docs carries additional operational guidance. The first pilot is Archcore + Superpowers. Installable instructions have one versioned source.

On the same date, the user clarified that any harness should have a path to use the recipe. U3. The catalog's product scope is harness-independent. Host-specific setup guidance and named verification environments do not form an exclusive eligibility list. The concrete portable delivery mechanism remains under research.

Earlier confirmed direction remains unchanged: offers start with Archcore; recipes work in existing harnesses; users may start through another tool or Archcore; original skills and available MCP tools implement the Markdown MVP; verification statements name their scope.

The investigation uses the existing requirement to keep research artifacts in global. Landing and docs were inspected without edits. The catalog location and first pilot direction are accepted. Other recipe URLs, detailed fields, release format, publishing mechanics, and metrics remain design proposals. Status acceptance records the research verdict; it does not imply that the catalog or any recipe is implemented or verified.

On 2026-09-08, the user requested the remaining uncertainties, an implementation plan, and execution order. The resulting planning defaults remain draft; this update adds no executed integration result.
