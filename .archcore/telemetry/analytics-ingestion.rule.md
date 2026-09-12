---
title: "Analytics Ingestion, Identity, and Opt-Out Across Every Archcore Surface"
status: accepted
tags:
  - "architecture"
  - "telemetry"
  - "web"
---

## Rule

Six surfaces report analytics into one project: the marketing routes, the content routes, the documentation site, the two installer scripts, the CLI binary, and one scheduled release-counter job. They live in four repositories, and every cross-surface question — how many installs became sessions, whether a reader continued into the docs — depends on them agreeing. The obligations below bind all of them.

1. Every surface MUST report into the single shared analytics project, and MUST distinguish itself by a property on the event rather than by a separate project.
2. The shipped ingestion host MUST be the neutral first-party proxy subdomain, and a surface MUST NOT ship the vendor's own ingest host or a subdomain named after the vendor or after tracking.
3. A legacy ingestion host MUST be kept alive while any released binary hardcodes it, and a new build MUST NOT ship against it.
4. WHEN a deploy ships an analytics host, the pipeline MUST prove that host reachable before the build, and the probe MUST confirm the ingestion handler itself rather than a name that merely resolves.
5. A repository that vendors a copy of the analytics core or of the reachability probe MUST gate its own build with the same probe.
6. The pipeline MUST re-run the reachability probe on a schedule, because a proxy whose backing deployment disappears fails long after the last deploy.
7. The ingestion key MUST NOT be committed to a source repository. A script MUST carry a placeholder that the deploy substitutes, and a binary MUST receive the key at release build time.
8. A surface MUST NOT send unless the key it holds carries the vendor's key prefix, so a clone, a fork, a local build, and a CI run are inert by construction rather than by an opt-out flag.
9. The release pipeline MUST assert that a published artifact is non-inert before the artifact is downloadable.
10. Every surface that identifies a machine MUST resolve its identifier from the one shared identifier file, in the one shared format, so a machine that ran an installer and later ran the binary counts once.
11. A surface MUST honour `DO_NOT_TRACK` and `ARCHCORE_TELEMETRY_OPTOUT`, and MUST evaluate both before it reads or creates the identifier file, so an opt-out leaves no trace on disk.
12. A browser surface MUST respect the browser's own do-not-track signal, and MUST pin that setting explicitly because the library's default disagrees with it.
13. A surface MUST NOT transmit an error message, a filesystem path, a directory or user or host name, or repository content.
14. The published privacy page MUST enumerate what every surface collects, and a surface MUST NOT begin collecting a category the page does not list.
15. WHEN a surface reports without a runtime disclosure a reader can see, the privacy page MUST carry the disclosure that surface cannot print.
16. IF ingestion times out, fails to resolve, or returns a non-2xx status, THEN the surface MUST discard the outcome, MUST NOT change its exit code, and MUST NOT print an error.

## Rationale

Requirement 1 is what makes a cross-surface funnel possible at all; separate projects per surface break every join, and the properties that tell surfaces apart are cheaper to add than the joins are to rebuild.

Requirement 4 exists because the failure it prevents is silent by construction. One ingestion host was dead for the whole period after a hosting migration: the name still resolved through a wildcard DNS record and answered with a deployment error, five of six surfaces reported nothing, and nothing failed anywhere. A build with a dead analytics host is indistinguishable from a healthy one, and an empty dashboard is indistinguishable from a product nobody uses.

Requirement 5 exists because the sharpest instance of that failure was the documentation site: it sat in a separate repository with its own copy of the host variable, so fixing the site that was noticed did not touch it, and it was found only when someone enumerated the whole set.

Requirements 7 and 8 pair deliberately. Deploy-time substitution plus a prefix guard means the off switch cannot be rewritten by the substitution that turns it on, and no CI opt-out plumbing is needed to keep test runs out of the data.

Requirement 10 is why the installer and the binary share one identifier file and one format, including on the platform where that path is not idiomatic: without it, "installed" and "used" are two populations that cannot be joined.

Requirement 11 orders the guards against the file read for a reason. An opt-out that writes an identifier first has already recorded the machine it was told not to record.

## Examples

**Good** — the two probes a reachability check runs, where only the vendor's own handler can answer the second:

```
GET  <host>/array/<key>/config   → the config JSON
POST <host>/i/v0/e/  (empty body) → 400, missing event name
```

**Good** — an inert build, with no flag involved:

> The key variable lacks the vendor prefix, so a `go build`, a fork, and a CI run send nothing.

**Bad** — a subdomain named after the vendor or after tracking, which is exactly what filter lists target.

**Bad** — an identifier file written before the opt-out variables are read.

**Bad** — a second analytics project for one surface, because that surface is built by a different framework.

## Enforcement

- **Engine** — the installer beacon, the key placeholder, and the identifier file: `cli/.archcore/telemetry/install-analytics-via-installer-beacon.adr`. The binary's own events, guards, and disclosure line: `cli/.archcore/telemetry/cli-update-telemetry.spec`. Provider choice: `cli/.archcore/telemetry/telemetry-provider-selection.rfc`.
- **Site** — the ingestion hosts, the reachability probe and where it runs, and the DNS and certificate records behind it: `landing/.archcore/infrastructure/analytics-host-must-reach-posthog.adr`. The event map, the shared analytics core, the vendored copy, and the per-surface configuration: `landing/.archcore/landing/analytics-event-taxonomy.doc`.
- Adding a surface, an event, or a host updates this rule first, then the owning repository's document, then the privacy page.
