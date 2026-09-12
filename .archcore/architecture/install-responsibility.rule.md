---
title: "Install Responsibility: Who Installs What, and Where the Installer Comes From"
status: accepted
tags:
  - "architecture"
  - "integrations"
  - "product"
---

## Rule

Installation crosses every repository in the ecosystem: the engine ships the installer scripts, the marketing site serves them, the engine installs the runtime, and four public surfaces describe the result. The obligations below bind all of them. Each repository holds its own enforcement detail and does not restate these.

1. The engine MUST install the runtime for each host the user selected, and the selection screen MUST state that selecting a host is the consent to install the runtime there.
2. IF a host was not selected, THEN the engine MUST NOT install the runtime for it.
3. The runtime MUST NOT contain code that downloads, caches, or installs the engine. The runtime invokes `archcore` from `PATH`, and IF the binary is absent, THEN the runtime MUST print the install command and stop.
4. A public surface MUST NOT state or imply that installing the runtime delivers the engine.
5. A public surface MUST present one install path — the platform install script, then `archcore init` — per `architecture/one-product-two-entry-points`.
6. WHEN a surface offers the per-host runtime install as well, the surface MUST offer it as a secondary link and MUST NOT offer it as a branch of the primary path.
7. The engine repository MUST hold the only source of truth for `install.sh` and `install.ps1`, and every other copy MUST be a build artifact re-synced from it at deploy time.
8. WHEN either installer script changes on the engine's default branch, the engine MUST notify the site repository so the served copy does not wait for the next unrelated deploy.
9. IF a re-synced installer is empty or is not a script, THEN the site deploy MUST fail loudly rather than publish the previous copy.
10. A path a visitor or an installer can trigger MUST NOT call `api.github.com`. Version resolution MUST use the release redirect, and repository facts a page displays MUST be fetched at build time.
11. WHEN the engine or the runtime changes a public install identifier — the repository, the marketplace, or the plugin id — the change MUST ship in step with the other side, per `architecture/plugin-cli-compatibility`.

## Rationale

Requirements 1 to 4 exist because the install story was stated four different ways on four surfaces while the mechanism had only ever worked in one direction. A runtime-only install leaves a reader with a command surface and no engine behind it, which is the one install outcome that looks successful and is not.

Requirement 3 is a standing ban, not a preference. A runtime-side engine fetcher shipped once and was withdrawn after producing offline failures, version coupling, cache pollution, and security-patch lag; the official installer already does that job without coupling the two release trains.

Requirements 7 to 9 exist because the "single source of truth" arrangement failed silently once: one installer was served as a redirect while the other was a divergent stale copy, and nobody noticed until the stale one was read. A generated artifact that can be edited by hand will be.

Requirement 10 exists because the unauthenticated GitHub REST budget is per originating IP. That is invisible to a single visitor and fatal behind shared egress — mobile CGNAT, corporate NAT, coworking Wi-Fi — where a few dozen visitors exhaust it and every later one sees a frozen placeholder.

## Examples

**Good** — one path, and the second step is a link:

```
curl -fsSL https://archcore.ai/install.sh | sh
archcore init
```

**Good** — the selection screen carries the consent, so nothing installs behind the user's back:

> A checked host is also the consent to install the Archcore plugin on it. Nothing is installed for a host you leave unchecked.

**Bad** — a tab pair that asks the reader to pick a component, where one tab omits the engine.

**Bad** — "The plugin runs on the CLI under the hood, so installing the plugin gets you both." The second clause was never true.

**Bad** — a star count or a latest-version lookup fetched from `api.github.com` in the browser or inside an installer.

## Enforcement

- **Engine** — the delivery surface, the selection screen, and the per-host actions: `cli/.archcore/integrations/plugin-delivery.spec` and `cli/.archcore/update/updating-the-plugin.spec`. Release-redirect version resolution: `cli/.archcore/update/resolve-latest-via-github-redirect.adr`.
- **Runtime** — the ban on an engine fetcher: `plugin/.archcore/plugin/stack-and-tooling.rule`, item 13.
- **Site** — installer re-sync, the build-time fetch, and the removal of `api.github.com`: `landing/.archcore/infrastructure/keep-github-api-out-of-visitor-paths.adr`. Per-surface copy obligations: `landing/.archcore/messaging-alignment.rule`.
- A change to who installs what updates this rule first, then the per-repository enforcement documents and the public surfaces together.
