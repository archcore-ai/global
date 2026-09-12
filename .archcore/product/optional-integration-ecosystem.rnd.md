---
title: "Archcore Integration Recipes — Markdown MVP and Assembly Research"
status: accepted
tags:
  - "architecture"
  - "integrations"
  - "product"
---

## Goal

Investigate optional, Archcore-centered integration recipes that preserve a user's existing harness and chosen entry point. The candidate set includes FPF Reference MCP, Superpowers, OpenSpec, Graphify, Context7, and Matt Pocock's grill-me. Readers: product and engineering maintainers. Investigation and clarification date: 2026-09-08.

Current recommendation: **refine the direction around tested Archcore + other-tool recipes; validate the first behavior layer through project instruction files before building additional runtime mechanisms.**

The user confirmed the product scope and MVP direction under Clarifications. A separate integration assembler is the primary architecture hypothesis. Its packaging, implementation, and effectiveness remain unvalidated. This report stays draft while that investigation continues.

The offered product starts from Archcore + a specific other tool or selected set. A general service for combining arbitrary tools without Archcore is outside the current scope. Product positioning around Archcore does not assign Archcore permanent control of the user's workflow.

## Questions

1. Which responsibilities and artifact owners allow Archcore and the selected tools to contribute from either entry point?
2. How much cooperation can project Markdown instructions establish, and which observed failures justify stronger mechanisms?
3. What does a separate assembler need to deliver a recipe into an existing harness without becoming its workflow controller?
4. What distinguishes an Archcore-verified recipe from an installation bundle or an unsupported compatibility claim?
5. Which recipe records and experiments establish explainable behavior and determine the next implementation step?

## Approach

Read first-party documentation, upstream skill and schema definitions, and local Archcore code. Compare ownership, activation, artifact lifecycle, portability, installation, recovery, and distribution. Search for counterexamples to the premise that integration or durable decisions alone differentiate Archcore.

OpenSpec means Fission-AI/OpenSpec. Graphify means Graphify-Labs/graphify and graphify.com for this investigation; the user identified grill-me as Matt Pocock's implementation. FPF is evaluated as a reference provider, not as a validated reasoning theory. Existing plugin FPF drafts are inputs to the investigation; their previously excluded candidates remain in this comparison.

The local audit covered MCP startup, instruction wiring, hook delegation, routing, delivery, and track state. No third-party plugin was installed and no combined workflow was executed. External sources were read on 2026-09-08 from mutable pages and main branches; this establishes inspected behavior, not compatibility with every published release. The installed Archcore research vocabulary probe returned yes for version 0.8.3.

### Inputs

All external access dates below are 2026-09-08. Publication dates are unknown unless stated by the source.

| ID | Material and publisher | Question supported |
|---|---|---|
| S1 | [FPF Reference MCP](https://mcp.fpf.sh/), FPF Reference maintainers | Provider boundary, lookup tools, source freshness |
| S2 | [Superpowers using-superpowers](https://github.com/obra/superpowers/blob/main/skills/using-superpowers/SKILL.md), obra | Activation, instruction precedence |
| S3 | [Superpowers brainstorming](https://github.com/obra/superpowers/blob/main/skills/brainstorming/SKILL.md), obra | Design ownership and output location |
| S4 | [Superpowers writing-plans](https://github.com/obra/superpowers/blob/main/skills/writing-plans/SKILL.md), obra | Execution-plan format and handoff |
| S5 | [OpenSpec customization](https://github.com/Fission-AI/OpenSpec/blob/main/docs/customization.md), Fission-AI | Context, schemas, community distribution |
| S6 | [OpenSpec concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md), Fission-AI | Current specs versus change deltas |
| S7 | [superpowers-bridge README](https://github.com/JiangWay/openspec-schemas/tree/main/superpowers-bridge), JiangWay | Existing integration precedent and limitations |
| S8 | [superpowers-bridge schema](https://github.com/JiangWay/openspec-schemas/blob/main/superpowers-bridge/schema.yaml), JiangWay | Actual adapter mechanics and output redirection |
| S9 | [Agent Skills host integration](https://agentskills.io/client-implementation/adding-skills-support), Agent Skills | Disclosure, activation, scope and collisions |
| S10 | [Spec Kit extension development](https://github.com/github/spec-kit/blob/main/extensions/EXTENSION-DEVELOPMENT-GUIDE.md), GitHub | Manifest, dependencies and extension events |
| S11 | [Spec Kit extension catalogs](https://github.com/github/spec-kit/tree/main/extensions), GitHub | Public discovery versus curated catalogs |
| S12 | [Skills documentation](https://www.skills.sh/docs), Vercel; [packs](https://www.skills.sh/docs/packs) | Existing skill distribution and bundles |
| S13 | [Claude Code plugins reference](https://code.claude.com/docs/en/plugins-reference), Anthropic | Native packaging, MCP names and hook loading |
| S14 | [intent-driven schemas](https://github.com/intent-driven-dev/openspec-schemas), intent-driven-dev | Counterexample: durable ADRs alongside OpenSpec |
| S15 | [Claude Code memory](https://code.claude.com/docs/en/memory), Anthropic | Instruction loading and enforcement limits |
| S16 | [Claude Code hooks](https://code.claude.com/docs/en/hooks), Anthropic | Command expansion and model-invoked skill activation |
| S17 | [Claude Code skills](https://code.claude.com/docs/en/skills), Anthropic | Namespaces, instruction loading and isolated execution |
| S18 | [grill-me](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md), Matt Pocock | User entry delegates to grilling |
| S19 | [grill-with-docs](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md), Matt Pocock | Interview and domain-modeling composition |
| S20 | [grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md), Matt Pocock | Interview mechanics and shared-understanding confirmation |
| S21 | [Graphify MCP tools](https://graphify.com/docs/mcp-tools), Graphify | Repository graph queries and source navigation |
| S22 | [Context7 MCP rules](https://github.com/upstash/context7/blob/master/rules/context7-mcp.md), Upstash | Library resolution and documentation lookup |
| S23 | [Ruler](https://github.com/intellectronica/ruler), intellectronica | Existing instruction and MCP distribution |
| S24 | [Skills CLI](https://github.com/vercel-labs/skills), Vercel Labs | Existing installation across agent hosts |
| S25 | [AGENTS.md](https://agents.md/), AGENTS.md maintainers | Plain Markdown interchange and documented host-specific setup; no universal loading guarantee |
| S26 | [Gemini CLI context files](https://geminicli.com/docs/cli/gemini-md/), Google | GEMINI.md default and configurable context.fileName |
| S27 | [OpenCode rules](https://opencode.ai/docs/rules/), Anomaly | AGENTS.md, configured instruction files, and absence of automatic reference expansion |
| S28 | [Cursor rules](https://cursor.com/docs/rules), Cursor | Root and nested AGENTS.md; rule scope differs between Agent and other surfaces |
| S29 | [Superpowers for OpenCode](https://github.com/obra/superpowers/blob/main/docs/README.opencode.md), obra | Native bootstrap and action-to-tool mappings; upstream claims are not Archcore test results |
| U1 | User instructions in the research conversation, 2026-09-08 | Confirmed scope, symmetry, assembler hypothesis, Markdown MVP, explainability, and harness-independent product scope |
| L6 | @plugin/plugins/archcore/skills/plan/SKILL.md; @plugin/plugins/archcore/skills/document/SKILL.md | Current command results, routing and continuation behavior |
| L1 | @cli/cmd/mcp.go; @cli/internal/mcp/server.go | Independent engine and project-root binding |
| L2 | @cli/internal/agents/instructions.go; @cli/internal/agents/mcp_helpers.go | Managed instructions and configuration ownership |
| L3 | @cli/cmd/hook_command.go; @plugin/plugins/archcore/bin/pre-tool-use | Existing lifecycle checks |
| L4 | @plugin/plugins/archcore/skills/_shared/delta-routing.md; @plugin/plugins/archcore/skills/_shared/gate-contract.md | Fixed runtime routing and draft state |
| L5 | @cli/internal/plugin/plan.go; @cli/internal/plugin/hosts.go; @plugin/.claude-plugin/marketplace.json | Existing delivery foundations |
| L7 | Installed Archcore 0.8.3, read-only stdio MCP probe on 2026-09-08 | Explicit landing project root returned 25 local documents and 50 mounted global documents; no recipe scenario or write test |

Local architectural constraints are discussed where they affect an option. Their graph relations accompany this investigation.

## Findings

### 1. The tools supply different roles (Q1)

| Tool | Inspected role | Useful contribution in a composition | Collision to resolve |
|---|---|---|---|
| FPF Reference | Read-only lookup over framework material | Cited reasoning concepts or review criteria | Treating an external framework as project policy |
| Superpowers | Skills that direct design, planning, implementation and verification | A selected execution discipline | Repeated interviews, duplicate plans, competing completion steps |
| OpenSpec | Change artifacts, dependency schemas and updates to current specifications | A change lifecycle with requirement scenarios | Two canonical specifications or two progress trackers |
| Archcore | Typed project documents, relations and retrieval; optional document-producing runtime | Its own loop when selected; project context and durable results inside another process | Unrequested routing, repeated interviews, or a forced Archcore next step |
| Matt Pocock's grill-me | User-facing interview entry delegating to grilling | Resolve open design questions while other tools supply facts and memory | Restarting the interview; treating tentative answers as authorized implementation |
| Graphify | MCP queries over a repository graph | Find dependencies and navigate to source evidence | Treating derived or stale graph information as accepted project policy |
| Context7 | Library resolution and documentation lookup | Ground library-specific claims in the selected documentation | Invoking documentation lookup for unrelated tasks or using the wrong library version |

FPF's public interface separates lookup from project memory and workflow ownership. It provides snapshot metadata, but freshness describes the configured source, not proof of latest upstream content. A network reference provider and a packaged method are different dependencies. S1.

Superpowers' bootstrap activates relevant skills broadly and gives explicit project/user instructions precedence. Its design and plan skills allow user-selected output locations. These are integration seams, not a formal callback API. S2–S4.

OpenSpec keeps current behavior in `openspec/specs/` and proposed changes in change folders; archive merges deltas into current specs. Its schemas and configuration provide extension surfaces, but prompt guidance is distinct from an executable validator. S5–S6.

Graphify and Context7 supply lookup surfaces; neither lookup alone settles a project decision. Matt Pocock's grill-me delegates to grilling, while grill-with-docs composes grilling with domain-modeling. These are inspected seams, not a demonstrated Archcore integration. S18–S22.

**Inference:** one owner per concern and per phase is more useful than one owner for the entire stack. OpenSpec can own change progress, Superpowers implementation, FPF reference material, and Archcore project knowledge. The host still owns execution tools and permissions.

### 2. The existing FPF research answers a narrower question (Q1, Q2)

The plugin's route investigation excluded runtime coupling before comparing candidates. Its recommendation establishes a low-change citation convention; it does not evaluate an integration business or prove that a broader composition layer is undesirable.

The accepted store-not-method-engine decision currently excludes tool-naming gates and previously rejects optional method packs because of namespace and storage fragmentation. The engine/runtime decision nevertheless explicitly allows a swappable runtime over one engine.

Separate three proposals:

- A bridge uses the existing Archcore MCP and one writable corpus. It need not introduce another engine or storage owner.
- A host-side entry adapter hands work to another method and checks the returned artifact. It changes integration behavior, while the core document gates can remain method-neutral.
- Archcore's core selects and executes third-party methods as its own workflow. This changes the current product boundary and needs a new decision before implementation.

The recorded reason against fragmented method packs does not, by itself, establish that a thin adapter sharing one engine causes fragmentation. This is a boundary clarification to settle after a prototype, not an implicit repeal of the decision.

### 3. Comparison of composition models (Q2)

Costs below are relative engineering judgments, not measured estimates.

| Model | Concrete mechanism | Advantage | Cost or failure mode | Assessment |
|---|---|---|---|---|
| A. Instruction recipe | Project-owned instruction fragment names owner, read points and filing rules | Small installation footprint; useful baseline | Model may ignore it; no dependency or output validation | Build as baseline and fallback |
| B. Adaptive harness adapter | Enabled capability catalog plus host-specific activation and validation | Loads only relevant integration; can respond to actual tools | Host events and skill APIs differ; detection cannot imply consent | Add after baseline behavior is measured |
| C. Archcore embedded in another workflow | Agent follows the foreign workflow and uses Archcore MCP for context and selected results | Existing users keep their commands and task lifecycle | Capture can be skipped | One side of the required entry-point comparison |
| D. Existing Archcore command as entry point | Archcore fulfills its command contract using supplied results and selected external capabilities | Preserves the Archcore loop for users who choose it | Full foreign workflows can compete with its route | Test the original command; no replacement entry required |
| E. External workflow plus selected knowledge capture | Keep foreign files canonical; extract decisions, rules and reusable lessons | Avoids format conversion of the whole workflow | Requires semantic selection and provenance | Preferred initial artifact model |
| F. One canonical artifact plus generated views | Author once; export a read-only view for another tool | Can serve both readers without two editable truths | Meaning, status and task syntax do not map automatically | Experiment for one artifact, not all types |
| G. Separate integration assembler | Archcore-centered recipes supply project instructions and supported native configuration | Fits existing harnesses and can later assemble new setups | Distribution can grow into an unvalidated universal platform | Primary architecture hypothesis; behavior MVP precedes installer expansion |

A–G are composable. The selected baseline combines A with C or D according to the user's entry point and uses E for foreign-owned artifacts. A general tool-neutral composition service remains an alternative outside the confirmed initial product scope.

Adaptive integration has two distinct levels: the host detects declared capabilities; the agent selects relevant enabled capabilities. A filesystem marker establishes possible installation, not that the current session can call a tool. A selected capability failure should stop only its dependent step or use the recipe's declared fallback.

### 4. Candidate integration seams, without a commitment to three adapter implementations (Q1–Q3)

#### FPF: optional reference lookup

Proposed flow: read relevant Archcore context; when the user-selected workflow needs framework grounding, query FPF; record only the relied-on IDs, source locator and snapshot beside the conclusion. Promote materials to evidence under the active citation convention.

Installation, project enablement, and task selection are separate. Disabling FPF removes its active instructions and calls while leaving filed knowledge intact. If a selected exact-wording lookup is unavailable, report that missing evidence; do not invent a citation. An ordinary task can continue without FPF when it does not depend on that lookup.

Keep the lookup outside core write hooks. Passing a focused question avoids sending the entire repository context. Record the snapshot of the material actually read; independently deployed wiki content cannot inherit the MCP snapshot without verification. S1.

#### Superpowers: Archcore as project context and result store

Proposed flow: Superpowers leads its design and execution phases; its agent reads Archcore decisions and rules before planning. Native execution plans stay in their existing location. After a design decision or completed change, the adapter proposes only lasting decisions, constraints or recurring patterns for Archcore.

Do not run a second full Archcore planning interview. Do not simply rename a Superpowers plan to `.plan.md`: its detailed code/checklist format and Archcore's document contract have different purposes. A location override alone does not resolve that mismatch. S3–S4.

A stronger variant writes a jointly compatible artifact through Archcore MCP, but it needs a content contract and an execution test. Start with selected capture because it preserves each tool's native operation. Generated summaries remain derived records with source path and revision; they do not become a second implementation checklist.

#### OpenSpec: foreign specifications remain canonical

Proposed flow: OpenSpec owns current specs, deltas, tasks and archive. Archcore owns ecosystem decisions, research, constraints and experience. Before proposal/design, the adapter retrieves relevant Archcore context; after a durable decision or closeout, it files selected knowledge.

Project context/rules are an initial prompt seam; a community schema is the stronger package seam. Neither turns an arbitrary JSON configuration key into an executable integration. S5.

Keep `openspec/specs/` authoritative for behavior covered there. Cite paths and revisions from Archcore; do not copy each spec into a separately editable Archcore spec. Archcore relation endpoints do not currently accept arbitrary foreign files, so these references are body locators, not fabricated graph edges.

If unified search over external specs proves necessary, evaluate a read-only indexing adapter separately. Foreign OpenSpec files are not automatically valid Archcore global sources.

### 5. Existing bridges validate feasibility and challenge differentiation (Q2, Q4)

OpenSpec's community list already includes `superpowers-bridge`. Its README describes a prompt-layer schema that redirects outputs into a change folder and requires Superpowers capabilities. It also warns that natural-language entry can bypass the schema. Its stated OpenSpec 1.4.1 / Superpowers v5.1.0 baseline is the maintainer's declaration, not a compatibility result from this investigation. S5, S7.

The schema contains explicit skill invocations, a plan artifact, a coarse task tracker, and ordered verification, retrospective and archive instructions. This demonstrates composition expressed in an existing extension surface. It does not demonstrate universal host support or deterministic enforcement: much of the ordering is prose, and file dependencies alone do not prove work completion. S8.

For an all-four stack, build on this ownership split rather than adding a third parallel planner. Archcore could read prior context before change work and receive promotion candidates from the retrospective; FPF stays an optional source.

Counterexample to a weak positioning claim: `intent-driven` schemas already add long-lived ADRs to OpenSpec, and publish starter templates. Therefore “OpenSpec lacks durable decisions” and “we bundle existing tools” are insufficient differentiators. S14.

**Hypothesis:** the additional value is retrieval and maintenance of typed, related project knowledge across successive changes, combined with tested composition behavior. That value still needs observation.

### 6. A recipe records cooperation; the assembler installs its selected representation (Q3)

Proposed shared structure; none of these fields is an existing Archcore API:

| Package element | What it records |
|---|---|
| Identity | Integration ID, package version, maintainer, source revision, license |
| Compatibility | Tested Archcore, external tool and host versions; required capabilities |
| Activation | Disabled/explicit/task-selected behavior; conditions and exclusions |
| Ownership | Phase owner; authoritative files; sole writer for each artifact |
| Inputs | Repository root, branch/worktree, source paths or document IDs with revisions |
| Outputs | Expected artifacts, destination, validation and status policy |
| Handoff | Entry condition, return condition, continuation target, failure result |
| Installation | Files and host settings owned by this package; dependencies reused |
| Lifecycle | Update, removal, retry, resume and configuration migration |
| Verification | Fixture tasks, assertions, observed results and unsupported combinations |

A capability label can describe reference lookup, planning, execution, verification, or knowledge capture. Labels alone are not compatibility: a provider also needs a concrete input/output contract. Two “plan” capabilities can produce incompatible formats.

The first recipe can carry these facts as a human-readable card, a short instruction fragment, fixture descriptions, and a result record. A manifest and installer can be derived after repeated installation needs are observed. No general provider registry or universal intermediate representation is selected for the MVP.

A handoff includes the selected owner, target repository/worktree, accepted inputs, output locations and completion evidence. Never infer acceptance of an ADR from a completed external task. A source revision plus operation ID can support duplicate detection during retry; semantic equivalence still needs review. These are proposed safeguards, not guarantees of current tools.

### 7. Optionality and installation into an existing harness (Q3)

The product model has three switches: **installed**, **enabled for this project**, **selected for this task**. Capability discovery reads the actual session surface. User-selected owners take precedence over auto-selection. A running change keeps its chosen owners until an explicit handoff; a newly discovered plugin does not silently take over.

Agent Skills documents progressive disclosure, explicit activation, disabled-skill filtering and collision handling. These provide a portable prompt baseline, not shared lifecycle hooks across every host. S9.

For an existing harness, installation proposes a bounded diff: add the adapter, reuse existing engines, preserve unrelated instructions and settings, verify the target root, and record package-owned changes. Updating reconciles local edits; removal deletes only owned wiring, retaining documents and shared dependencies.

For a new setup, a recipe composes the same adapters with explicit default owners. Candidate offers are “Archcore + Superpowers” and “Archcore + OpenSpec + Superpowers, FPF optional.” These are Archcore-centered configurations. Their order in the catalog does not dictate the session's entry point.

A native plugin package can carry skills, hooks and MCP registration, but host names and scopes matter. Claude Code documents scoped MCP names for plugin hooks; hard-coded bare tool names can miss their target. S13. Every advertised host therefore needs an adapter and verification record.

### 8. What Archcore already supplies, and what needs building (Q3)

| Existing foundation | Evidence | Possible extension, only if the pilot needs it |
|---|---|---|
| Independent stdio MCP with explicit project binding | @cli/cmd/mcp.go:20; @cli/internal/mcp/server.go:286 | Cross-project target selection and validation in each adapter |
| Idempotent baseline instruction block | @cli/internal/agents/instructions.go:152 | Separate adapter-owned blocks; baseline reinstall replaces its own block |
| MCP configuration convergence for Archcore | @cli/internal/agents/mcp_helpers.go:63 | Arbitrary provider installation and deduplication |
| Shared lifecycle hooks | @cli/cmd/hook_command.go:54 | Ordering and failures across external integrations |
| Markdown instrument registry | @plugin/plugins/archcore/skills/_shared/delta-routing.md:117 | Runtime provider registry and selection contract |
| Draft state for Archcore tracks | @plugin/plugins/archcore/skills/_shared/gate-contract.md:61 | Cross-workflow handoff and foreign-state resume |
| Marketplace and delivery planner | @plugin/.claude-plugin/marketplace.json:9; @cli/internal/plugin/plan.go:14 | General package identity, dependency state and version pinning |

The engine can be consumed through MCP today. Its internal Go packages are not a published integration SDK. The existing `detect-integrations` grounding helper concerns application services, not harness composition.

Observed in this session: the MCP searches only the global repository's 46-document initial corpus, although several sibling repositories are writable in the workspace. An adapter cannot assume that a host workspace folder is the current MCP corpus. Pin the intended engine root and verify it before filing. Multiple roots and worktree switches belong in integration tests.

### 9. Integration marketplace and distribution strategy (Q4)

The user requested an integration marketplace as a distribution direction and subsequently fixed its initial scope to Archcore + a named tool or selected set. U1. The core offer is **Archcore-verified combinations, resolution of known conflicts, and an explainable assembled configuration — supported combinations with a stated verification level.**

[assumption] The first marketplace can be a curated recipe catalog maintained by Archcore. Paid transactions, open submissions, and a separate commercial platform are not prerequisites for testing that offer.

#### Product boundaries

[assumption] The marketplace, recipe, and assembler have distinct responsibilities:

| Element | User-facing responsibility | Boundary |
|---|---|---|
| Marketplace | Discover and compare Archcore-centered setups, understand their value and limits, and inspect verification evidence | A listing does not prove every host, version, or task works |
| Recipe | Describe selected cooperation rules, artifact ownership, conflict resolutions, and evaluated scenarios | A recipe does not require a new user-facing skill |
| Assembler | Apply the selected recipe to an existing setup and explain the resulting configuration | It does not become the permanent controller of the user's workflow |
| Existing harness | Run the user's selected skills and available tools | Product prominence does not assign Archcore exclusive workflow ownership |

Every initial offer includes Archcore. Candidate listings can describe Archcore + Superpowers, Archcore + OpenSpec, Archcore + Matt Pocock's grill-me, or a selected multi-tool set. These names illustrate the product scope; no listing is currently a tested release. FPF, Graphify, and Context7 remain candidate contributions under the same scope.

#### What a recipe listing exposes

[assumption] The listing gives the user enough information to decide whether the recipe fits their existing harness before applying it:

| Listing field | What the user can determine |
|---|---|
| Job and expected value | Which recurring problem the combination addresses |
| Participating tools and prerequisites | Which components already need to be installed and callable |
| Entry points and responsibilities | What happens when starting through Archcore or through the other tool |
| Artifact ownership | Where canonical decisions, specifications, and execution plans live |
| Behavior explanation | Which rule changes cooperation, why it exists, and which conflict it resolves |
| Setup effect | Which instruction fragments and native settings are added or changed |
| Verification record | Exact recipe/tool revisions, host, model, dates, scenarios, observed outcomes, and interventions |
| Known limits | Unchecked versions, unsupported routes, unavailable capabilities, and remaining conflicts |
| Maintenance | Recipe author, Archcore reviewer, update history, and current support status |
| Removal | How to remove recipe-owned wiring while retaining project knowledge and shared dependencies |

Authorship and verification are separate facts. A community-authored recipe would not acquire an Archcore-verified label merely by being listed [assumption]. The phrase “verified by Archcore” describes recorded checks by Archcore maintainers, not certification or endorsement by the upstream tool authors.

#### Existing setups and new setups

The user explicitly wants both adding integration to an existing harness and starting a new setup. U1. [assumption] The marketplace can present these as two paths to the same versioned recipe:

- Existing setup: select a recipe, inspect prerequisites and the proposed configuration effect, apply its rules, and verify the selected environment.
- New setup: select an Archcore-centered combination, establish the prerequisites, then apply and verify the same cooperation rules.

The behavior MVP covers original skills and MCP tools that are already installed and callable. A marketplace can publish its Markdown instructions with manual setup guidance before an automated assembler exists. Automated dependency installation for a new setup is a separate delivery milestone, not a property of the instruction-only MVP.

[assumption] The assembler's explanation names the selected recipe and revision, retained user entry points, effective rules and their reasons, canonical artifact locations, changed configuration, and any unresolved prerequisites. It explains declared policy and tested outcomes; it does not claim insight into a model's private reasoning.

#### Publication and maintenance

[assumption] A candidate publication process is authoring, source review, setup checks, scenario execution, and publication of the resulting evidence. These checks support different claims; the listing shows each recorded result rather than promoting a successful install to a blanket compatibility badge.

[assumption] Publication includes at least one named maintainer and the scope of the claim. An upstream release creates an unchecked version combination until the affected checks run again. A regression changes the support statement for affected versions while retaining historical results. It does not erase project documents or silently modify existing installations.

Open third-party submissions are a later option. [assumption] If introduced, their records would distinguish author-provided evidence, Archcore review, and Archcore-executed verification. Submission rules, review staffing, update obligations, and response expectations remain open.

#### Distribution and acquisition

Spec Kit already has extension manifests, dependency requirements, extension events, direct installation and organization-curated catalogs. Skills already distributes skill bundles. S10–S12. Ruler distributes instructions and MCP configuration across hosts; Skills CLI installs skills for multiple agents. S23–S24. These sources establish existing distribution mechanisms, not demand for this proposed marketplace.

[assumption] An Archcore catalog page can serve as the product entry point while existing native marketplaces and upstream directories distribute compatible packages. A proprietary package manager is not required to test discovery, adoption, and continued use.

Proposed acquisition messages remain hypotheses:

- Superpowers users: recover project decisions and constraints in the next task.
- OpenSpec users: carry research, decisions, and recurring lessons across changes while retaining native specifications.
- grill-me users: ground the interview in existing decisions and preserve significant agreed results.
- FPF users: preserve the project conclusion together with its cited source.

[assumption] Evaluate the path from discovering a recipe to using it on a task and retrieving useful project knowledge in a later task. Record setup completion, second-task reuse, repeated questions, duplicate artifacts, manual interventions, and maintenance effort alongside installation counts.

[assumption] Expansion beyond a maintained catalog becomes justified when repeated use and the supply of maintained recipes exceed what the initial publication process can serve. Payments, subscriptions, revenue sharing, paid support, ratings, and an author portal remain business hypotheses. No willingness-to-pay or marketplace demand measurements have been collected.


### 10. Markdown-first pilot and falsification (Q5)

These are proposed experiments, not completed tests. The behavioral MVP assumes that the original skills and MCP servers are already installed and callable. The initial assembler can be exercised as a reviewable installation diff; automatic dependency installation is a separate experiment.

| Comparison | Evidence sought | Finding that changes the design |
|---|---|---|
| Native workflow versus the same workflow with the recipe | Relevant prior context used; significant new decisions recoverable in a later task | Native documentation provides equal value with less work |
| Archcore entry versus foreign-tool entry | Both keep their selected task; each applicable contribution is fulfilled | One entry starts a competing interview or changes the requested result |
| Complete supplied information versus an intentionally missing fact | Archcore reuses sufficient inputs and identifies the specific gap | Full re-elicitation remains necessary or unsupported assumptions are filed |
| Markdown recipe versus a targeted host hook | Fewer missed reads or forgotten captures, with measured context and intervention cost | Added machinery does not improve the observed failure |
| Pair versus selected three-tool recipe | Artifact ownership remains explicit and results stay consistent | Pairwise compatibility fails to compose |
| Manual recipe application versus assembler output | Equivalent instructions, correct target root, explained changes and reversible wiring | The assembler changes semantics or overwrites project customization |

The selected first pair is Archcore + Superpowers. U1. Add Context7 for a bounded third-tool scenario, and use Archcore + Matt Pocock's grill-me to exercise interview ownership. FPF, Graphify, and OpenSpec remain in the research set; installing every candidate is not a pilot prerequisite.

Candidate fixtures include a feature, a small fix, a resumed task, a pre-existing conflicting ADR, insufficient input, an unavailable selected MCP, a worktree/root switch, and a project with edited instructions. Record host, model, tool revisions, recipe revision, fixtures, run counts, observed outcomes, and manual interventions. Thresholds and representative verification environments remain open; the product scope is harness-independent.

A compatibility claim is limited to the actual environment and scenarios run. Source review, successful configuration, and observed cooperation are separate evidence. Zero wrong-root writes, unintended canonical duplicates, or silent workflow takeovers is a proposed acceptance condition for the selected fixtures [assumption], not an observed result.

Suggested demand probe: three independent repositories use a recipe on two successive changes and retrieve a previously stored fact [assumption]. This is an exploratory sampling choice, not statistical validation.

### 11. Command meaning, host seams, and the optional composite skill (Q1–Q3)

The user confirmed a stable behavioral direction: Archcore accepts prepared information, checks its sufficiency, and fulfills its own responsibility. The project integration selects the external way of obtaining that information. This describes the intended contract; L6 still contains route execution and Archcore-specific continuation instructions, so bounded participation is not certified as implemented.

The two planning skills overlap without producing identical results: Archcore plan assembles a project-document package; Superpowers writing-plans expands implementation work into detailed steps. Recipe authors first compare required results, artifact formats, and completion boundaries. Running both complete workflows is not evidence of successful integration. L6, S4.

Claude Code documents UserPromptExpansion for a user-entered command and PreToolUse with Skill for model-invoked activation. These can add context without editing upstream skill files. They establish activation seams, not a semantic “decision completed” event or guaranteed call/return for a workflow. S16–S17.

A third composite plan is an optional user-selected workflow. It does not cover direct entry through either original command. Plugin command namespaces also prevent a new unqualified plan skill from automatically replacing namespaced plugin commands. S17. A mandatory wrapper is therefore outside the selected baseline.

### 12. The instruction-only MVP and its boundary (Q2, Q3)

The user selected a short instruction fragment, original skills, and existing MCP tools as the first behavioral prototype. The following text is the user-endorsed seed, not a claim of tested agent behavior:

```text
Сохраняй задачу явно вызванного пользователем скилла.

Перед проектным решением учитывай релевантные документы Archcore.
Используй результаты проведённого интервью; уточняй оставшиеся пробелы.

В процессе Superpowers сохраняй его рабочие артефакты.
Значимые согласованные решения фиксируй через Archcore.

Для документации библиотек используй Context7, когда это применимо.
```

All cooperation rules can be written in Markdown for the first prototype. The files do not themselves install servers, make tools callable, validate dependency versions, or guarantee that the model performs every action. Anthropic describes CLAUDE.md as model context rather than enforced configuration. Claude Code reads CLAUDE.md and documents importing AGENTS.md when the repository shares its instructions. S15.

The generic seed needs recipe-specific choices about authoritative artifacts, capture timing, insufficient inputs, and unavailable capabilities. A completed interview does not by itself authorize implementation or assign accepted status to an Archcore document. Matt Pocock's grilling explicitly waits for confirmation of shared understanding before acting on the result. S20.

Add hooks, scripts, or further skill changes against observed failures: missed context, repeated interviews, lost decisions, or incorrect artifact ownership. Their presence alone does not upgrade a recipe's verification level.


### 13. Harness independence separates cooperation from delivery (Q2, Q3, Q5)

U1 clarifies the product target: a user of any harness should have a way to use a recipe. Selecting one host for a test does not select the product's audience. [assumption] Define eligibility by required capabilities and provide a manual connection path for an unrecognized harness. Keep observed verification coverage separate.

The user further clarified that dedicated instructions for individual agents are acceptable. U1. Installation access is the priority, with particular attention to widely used agents. Universality does not require identical instruction text or an identical installation procedure for every host.

[assumption] Maintain shared cooperation rules plus versioned host-specific instructions where they improve installation or resolve a documented host difference. Explain and test any resulting behavioral difference. Provide complete installation guidance for prioritized agents and retain a capability-based path for other harnesses. The specific priority list remains open; no popularity ranking is established here.

#### What the inspected implementations establish

| Source | Observed behavior | Implication for the candidate |
|---|---|---|
| S15 | Claude Code reads CLAUDE.md and supports importing AGENTS.md | One authored fragment can be imported through a Claude-specific entry file |
| S26 | Gemini CLI defaults to GEMINI.md and allows configured context filenames | A fixed filename is not a common denominator |
| S27 | OpenCode reads AGENTS.md but does not automatically expand its file references; its configuration can load instruction files | An import-looking line alone does not establish that the recipe reached the model |
| S28 | Cursor reads root and nested AGENTS.md; rule coverage depends on the agent surface | A successful Agent setup does not certify every AI feature of the same application |
| S9 | A client can activate original skill instructions through file reads or a dedicated tool | A native Skill tool is not a universal prerequisite; full instructions and referenced resources still need delivery |
| S29 | Superpowers separates action descriptions from OpenCode's native tool names | Semantic instructions plus delivery mappings have an upstream precedent |

S25 supplies a shared Markdown convention, not identical instruction discovery, precedence, or persistence across clients. S15 also distinguishes model guidance from client-enforced settings.

L2 already writes the same Archcore instruction body into different host files while preserving text outside managed spans. L5 supplies native plugin installation mappings. These are foundations for delivery; they do not implement recipe composition.

#### Proposed separation

[assumption] Use three inputs to produce an explained installation:

- Recipe: participating tools, applicability, prepared inputs, requested outputs, artifact ownership, and known conflict resolutions.
- Environment binding: where instructions load, how original skills and their resources are reached, and how required tool actions resolve in that session.
- Project choices: repository root, existing artifact locations, selected optional contributions, and user preferences.

The environment binding does not select interview questions, change the result of a plan command, or appoint a permanent workflow owner. Those choices belong to the recipe and project policy. A new harness can supply the same capabilities without requiring a new Archcore + Superpowers workflow definition [assumption].

[assumption] The baseline export contains the complete selected cooperation text. Place it inline in the host's supported project-instruction surface; native imports are an optional delivery form. Generated copies retain the same recipe revision and are not independently authored sources. This avoids depending on common import syntax. A later assembler owns only its marked spans and records the applied representation for update and removal.

[assumption] An unrecognized harness gets the same downloadable text, prerequisites, and manual connection checklist. A session-only copy is another candidate for trying the rules where persistent instructions are unavailable; its scope ends with that session. Neither path requires a third plan skill. The catalog can prioritize dedicated setup paths for named agents alongside this common path without making host selection an admission gate.

#### Capability boundary and the strongest counterexample

[assumption] Full recipe execution requires a way to deliver user-selected instructions, access the complete original skill resources needed by the task, invoke the required Archcore operations against the intended project, and read or write the participating tools' artifacts within existing permissions. Hooks, marketplace support, native slash-command syntax, and a dedicated skill activation tool are not proposed baseline requirements.

A chat surface that cannot access project tools can read the explanation, but this investigation supplies no mechanism for it to update Archcore. A harness without native MCP needs an available tool bridge before it meets that prerequisite. Such a bridge is a separate delivery question; labeling the recipe universal does not create one. Missing capabilities remain explicit, with independent work still possible.

L7 tests one narrow boundary: launching `archcore mcp --project /Users/ivklgn/Documents/archcore/landing` through a stdio MCP client returned landing documents and the configured read-only global source. The probe used protocol version 2024-11-05, called list_documents, and terminated without document writes. It demonstrates explicit project binding independently of the session's global-bound MCP connection. It does not establish a released bridge, whole-workflow portability, or correct writes.

#### Workflow compatibility remains an independent hypothesis

S2 allows explicit user project instructions to take precedence over skill defaults. This supplies a place for a deliberately installed recipe to express cooperation. It does not show that any merged instructions are consistent. S3 has path-specific terminal states; L6 gives Archcore its own routing and continuation. Merely loading both does not resolve those transitions.

[assumption] Preserve the user's selected command result, reuse supplied inputs, and assign complementary contributions at task-relevant boundaries. Test the current skills before declaring this an implemented participation mode. If a selected method requires an unavailable execution capability, report that unmet prerequisite instead of silently translating it into another method.

[assumption] Maintain recipe semantics separately from host delivery code to reduce duplicated authoring. Do not reduce verification to independent recipe and host badges: instruction precedence, context compaction, artifact access, and third-tool interactions still need combined scenarios.

## Recommendation

**Refine** the architecture around an Archcore-centered catalog of verified recipes and a separate integration assembler hypothesis. Findings 1, 6, 9, 11, 12, and 13 support this direction. Findings 5 and 9 limit differentiation claims; Finding 10 identifies the missing behavioral evidence.

The current offer is Archcore + a named tool or selected set. Users retain either the Archcore loop or their foreign-tool entry. Archcore accepts supplied information, checks sufficiency, and performs its part; project integration rules determine external methods. Catalog centering and workflow control are separate choices confirmed by U1.

Use project Markdown instructions as the first cooperation layer over installed, callable tools. Document each recipe's responsibilities, artifact owners, rationale, limitations, and verification evidence. Treat “supported” as a bounded claim about tested combinations, not every version of every tool.

Treat the integration marketplace as the discovery, comparison, and evidence surface for Archcore-centered recipes. Begin with a maintained catalog; keep open submissions and commercial mechanics as later hypotheses. Finding 9 defines this product separation.

Keep the assembler separate from ongoing workflow control. Its delivery role is the primary hypothesis; a separate commercial product, package manager, implementation language, and runtime service have not been selected.

The earlier recommendation to ship three adapter implementations and two recipes is replaced by this narrower baseline. Defer mandatory wrappers, silent command replacement, bidirectional artifact synchronization, and universal tool-neutral composition. Add machinery only when the experiments identify an unmet requirement.

## Next Action

Use the recipe now added under @plugin/integrations/superpowers/ on real plugin work. The repository opts in through @plugin/AGENTS.md. Make the original Superpowers skills available in the chosen working session before describing a task as a joint run; they were not exposed in the session that added the recipe.

Record reused input, actual artifacts, conflicts, and manual correction with the task outcome. Refine the recipe from these observations. Release schema design, repeatable evaluation, broader installation checks, and the landing catalog follow initial use. The separate assembler remains a later hypothesis driven by concrete installation work.

## Open Gaps

- No end-to-end integration was executed; upstream source inspection is not a passing compatibility test.
- Upstream pages and main branches are mutable. Exact release commits and artifact digests need pinning for each prototype.
- FPF's reasoning benefit was not evaluated; only its integration surface was inspected.
- No user interviews, acquisition measurements, retention data or willingness-to-pay research were collected.
- Superpowers and OpenSpec content mappings need task-level tests; full round-trip equivalence is not assumed.
- Cross-host disabling, context compaction and missing-capability recovery need observed transcripts.
- Package licensing and redistribution boundaries need checking before bundling upstream material.
- The pilot may show that a short instruction recipe is sufficient. That would constrain the assembler to installation and verification rather than adding workflow execution.
- Recipe fields, evidence labels, support expiry, representative host/model environments, and maintenance ownership need a concrete pilot record.
- The manual path for an unrecognized harness and any bridge required by a client without native MCP remain untested.

- Marketplace publication criteria, maintainer obligations, regression handling, community participation, and commercial scope remain unselected.

## Clarifications

The following directions were explicitly confirmed by the user on 2026-09-08:

1. Center current offers on Archcore + a named tool or selected set. The customer comes for that setup, not a general service connecting arbitrary tools.
2. Provide combinations verified by Archcore maintainers, resolve known conflicts, and explain why the assembled configuration behaves as it does.
3. Describe support as “supported combinations with a stated verification level.”
4. Use a separate assembler as the primary architecture hypothesis: it installs tested cooperation rules into an existing harness.
5. Start behavioral validation with AGENTS.md or CLAUDE.md, original skills, and already installed, callable MCP tools.
6. Preserve the task of the explicitly selected skill. Entry through Archcore's own loop and entry through another tool are both supported design targets.
7. Let Archcore consume prepared information, check sufficiency, and fulfill its responsibility; project integration chooses the external method.
8. Add hooks and further components in response to observed failures rather than assuming them necessary.
9. Record this direction in global research and continue designing the recipes and verification model.
10. Record the integration marketplace as an additional product and distribution direction. This does not approve payment mechanics or open third-party publication.
11. Make recipes usable across harnesses, including ones not named by Archcore. Investigate missing portability mechanisms instead of selecting one harness as the product boundary.
12. Allow dedicated instructions and installation paths for individual agents. Prioritize users' ability to install the integration, particularly in widely used agents; identical instructions across hosts are not a requirement.
13. Add the recipe and integration directly to the plugin repository, then investigate through real tasks there. A separate fixture system and finalized release format are not prerequisites for this first use.

These confirmations establish the investigation's product direction. They do not establish empirical compatibility, a final implementation schema, or release readiness. Representative verification environments and exact upstream revisions remain open; they define evidence coverage, not an exclusive product host.

Stored in global because this question spans product positioning, engine responsibilities, runtime behavior, and distribution. The plugin's existing uncommitted FPF artifacts remain separate inputs.

On 2026-09-08, the user requested the remaining uncertainties, an implementation plan, and execution order. The resulting planning defaults remain draft; this update adds no executed integration result.
