---
title: "Host Static Web Properties on GitHub Pages"
status: accepted
tags:
  - "web"
---

## Context

Archcore's public web properties — the documentation site (`docs.archcore.ai`, Astro + Starlight) and the landing site (`archcore.ai`, Vite + React SPA) — are both **fully static**: no SSR, edge functions, or middleware. They were originally hosted on Vercel.

Vercel is blocked or unreliable for a portion of users in Russia, so potential users could not reach the documentation or the landing page / install instructions. With no server-side requirement, there is no technical reason to stay on a platform with access restrictions.

## Decision

**Host all static web properties on GitHub Pages, deployed via GitHub Actions.**

- Each site builds to a static `dist/` and deploys on every push to `main` via `.github/workflows/deploy.yml`.
- Custom domains are configured via `public/CNAME` (`docs.archcore.ai`, `archcore.ai`).
- Vercel config and deploy scripts are removed.

This decision applies to every current and future static web property in the ecosystem; each repo implements only its own framework-specific build wrinkles (below).

## Per-repo implementation notes

These belong in each repo's `.archcore/`, not here:

- **docs (Astro + Starlight):** Astro emits static HTML for all routes, so no SPA fallback is needed.
- **landing (Vite SPA):** a Vite post-build plugin copies `index.html` → `404.html` (GitHub Pages serves it for unknown paths, enabling client-side routing). `/install.sh` is served as a real POSIX script from `public/install.sh` so `curl -fsSL archcore.ai/install.sh | sh` works. Per-route social previews require a `closeBundle` plugin that emits `dist/<route>/index.html` with rewritten OG tags (see `web/og-image-generation`).

## Consequences

**Positive**
- Accessible to users behind Vercel restrictions; no platform access barrier.
- Free hosting, simple CI, no vendor lock-in for a static workload.

**Negative / trade-offs**
- GitHub Pages has a soft bandwidth limit (100 GB/month) — not a concern at current scale.
- SPA properties need an explicit 404 fallback and a per-route prerender step for social scrapers, since Pages serves only static files.
