---
title: "Build-Time OG Image Generation (Satori + resvg)"
status: accepted
tags:
  - "og-images"
  - "web"
---

## Overview

The shared technique Archcore's web properties use to generate Open Graph / Twitter Card images (1200×630 PNG) **at build time**, with no Figma and no headless browser. Layouts are defined as code and rendered during the build. This guide is framework-agnostic; the docs site (Astro) and landing site (Vite SPA) each apply it with their own page-discovery and meta-injection mechanics (see "Per-repo specifics").

## How it works

- **Satori** renders a JSX/object node tree → SVG (Flexbox-only CSS subset).
- **@resvg/resvg-js** rasterizes SVG → PNG (Rust/WASM, works in CI).
- **tsx** runs the TypeScript generator script (`scripts/generate-og-image.mts`).
- The script runs automatically via a `prebuild` npm hook, so CI needs no manual step — `npm run build` produces the images.

## Steps

1. **Install:** `npm i -D satori @resvg/resvg-js tsx`.
2. **Add fonts:** place raw `.ttf` files in `scripts/fonts/` (Satori cannot use OTF). Google Fonts has no direct TTF download — use the font's GitHub releases (e.g. `https://github.com/rsms/inter/releases`).
3. **Write the generator** (`scripts/generate-og-image.mts`): build a Satori node tree, then for each image `satori()` → SVG string → `new Resvg(svg)` → `.render().asPng()` → write the PNG. Keep shared visual constants (colors, grid, width/height, logo) at the top; the brand palette is the project's `DESIGN.md`.
4. **Wire the build:** add `"og:generate"` and run it from `prebuild` so it executes before the framework build.
5. **Inject per-page meta** so social scrapers see the right `og:image` per route (see per-repo specifics — scrapers do not execute JS, so client-side updates alone are invisible to them).

## Satori constraints

- Flexbox only — no CSS Grid, no `position: absolute`, no `calc()`/`clamp()`.
- Images must be base64 data URIs or remote URLs; fonts passed as ArrayBuffers.
- Long text: allow wrapping or reduce font size; truncate descriptions to avoid overflow.

## Verification

After deploy, check each URL with **opengraph.xyz**, and by pasting into Telegram / X / Discord. Social platforms cache aggressively — to refresh: Facebook Sharing Debugger → "Scrape Again"; Telegram → `@WebpageBot`; Twitter expires on its own within hours.

## Common issues

| Symptom | Cause | Fix |
|---------|-------|-----|
| Build fails "Unsupported OpenType signature" | OTF instead of TTF | Use `.ttf` fonts in `scripts/fonts/` |
| Image not showing on social | File missing from build output | Confirm the PNG exists in the build output |
| Layout broken | Unsupported CSS | Satori is Flexbox-only — remove Grid/absolute/calc |
| Stale preview | Platform cached old image | Use platform-specific cache purge |

## Per-repo specifics

- **docs (Astro + Starlight):** auto-discovers pages from `src/content/**`, derives slug + title from frontmatter, emits `public/og/<slug>.png`; a custom `src/components/Head.astro` injects per-page `og:image`. See `docs/.archcore/og-image-generation.guide`.
- **landing (Vite SPA):** a `VARIANTS` array drives one image per route; `scripts/prerender-routes.mts` (`closeBundle` plugin) bakes per-route static HTML with rewritten OG tags for scrapers, and `src/hooks/use-page-meta.ts` updates tags on client navigation. Keep `VARIANTS`, `ROUTES`, and `usePageMeta` in sync. See `landing/.archcore/landing/og-image-generation.guide`.
