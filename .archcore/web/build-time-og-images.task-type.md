---
title: "Add Build-Time OG Image Generation to a Static Site"
status: accepted
---

## What

Add programmatic Open Graph / Twitter Card image generation (1200×630 PNG) to a static site using **Satori + @resvg/resvg-js** at build time. Produces branded social-preview cards with no Figma and no headless browser — the layout is code, rendered during the build. Reusable pattern across any static web property; for the full technique and gotchas see `web/og-image-generation`.

## When to use

- A static site (e.g. on GitHub Pages) needs OG / Twitter Card previews.
- No SSR or edge functions are available.
- Images should auto-regenerate when content or branding changes.

## Steps

1. **Install** dev deps: `satori`, `@resvg/resvg-js`, `tsx`.
2. **Add `.ttf` fonts** to `scripts/fonts/` (Satori rejects OTF; download from the font's GitHub releases).
3. **Write `scripts/generate-og-image.mts`** — render `satori()` → SVG → `new Resvg(svg).render().asPng()` → write PNG. Define one entry per image (single image, or one per route via a `VARIANTS` array). Keep shared visual constants (palette from `DESIGN.md`, grid, dimensions, logo) at the top.
4. **Wire the build** — add `og:generate` and call it from `prebuild` so `npm run build` regenerates images.
5. **Inject per-route meta** so scrapers see the correct `og:image` per page — scrapers do not run JS, so a static/per-route layer is required (framework-specific; see per-repo notes in the guide).
6. **Exclude `scripts/` from lint** if your ESLint config type-checks the project.

## Expected outcome

One ~60 KB 1200×630 PNG per image, generated on every build; branded preview cards on shared links; image content version-controlled and edited by changing the script.

## Pitfalls

- **OTF fonts don't work** — TTF only.
- **Social platforms cache aggressively** — use platform debuggers to force refresh after deploy.
- **Client-side meta isn't enough for scrapers** — they don't execute JS; a static per-route layer is mandatory for distinct previews.
- **Satori CSS subset** — Flexbox only; no Grid, absolute positioning, `calc()`/`clamp()`.
- **Multi-layer drift** — when per-route previews exist, keep the generator's variants, the prerender route config, and any client meta hook in agreement.
