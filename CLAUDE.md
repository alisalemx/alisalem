# CLAUDE.md

Guidance for Claude Code when working in this repository.

Single-page Astro static site for [alisalem.ca](https://alisalem.ca), deployed to Cloudflare Pages.

## Tech stack

- **Astro** `^6.3.1` (static build, no SSR)
- **Tailwind CSS** `^4.3.0` via `@tailwindcss/vite` — no `tailwind.config.js`; config lives in `src/styles/global.css` using `@theme` and `@layer`
- **TypeScript** strict (`astro/tsconfigs/strict`)
- **@phosphor-icons/core** for SVG icons

## Dev commands

```sh
npm run dev      # Astro dev server
npm run build    # Static build → dist/
npm run preview  # Preview production build locally
```

No test, lint, or format scripts exist. Do not add them unless requested. Use `npm run build` as the main verification step.

## Entrypoints and structure

- **`src/pages/index.astro`** — sole page. Imports profile data from `src/content/profile.md` via `frontmatter` export.
- **`src/layouts/BaseLayout.astro`** — root layout. Loads Google Fonts and `src/styles/global.css`.
- **`src/content/profile.md`** — single source of truth for name, title, summary, links, and work history (YAML frontmatter). `descriptionHtml` keys allow inline HTML.
- **`src/styles/global.css`** — Tailwind v4 entrypoint. Defines custom theme colors/fonts and component layers (`home-logo-link`, `contact-link`, `gradient-link`).
- **`public/as-logo.svg`** — favicon and home logo asset.

## Notable patterns

- **SVG icons are imported as raw strings** using the `?raw` query:
  `import githubIcon from "@phosphor-icons/core/regular/github-logo.svg?raw"`
- **Icons are manipulated via string replacement** in frontmatter to inject Tailwind classes, SVG gradients, and SMIL animations. Do not treat them as components.
- **Tailwind v4 syntax**: uses `@import "tailwindcss"`, `@theme { ... }`, and `@layer components { ... }`. No `tailwind.config.js`.
- **No CI config in repo** — use `npm run build` as the main verification step.

## Deployment

- Deployed as a static Astro site to Cloudflare Pages from the `main` branch.
- Build command: `npm run build`.
- Build output directory: `dist/`.

## Content and design conventions

- The current page structure is intentionally minimal: intro/contact links plus Experience. Do not reintroduce a standalone About section unless requested.
- Put biographical proof points and role context into the relevant `roles` entries in `src/content/profile.md`.
- For longer YAML frontmatter text, prefer folded scalars (`>-`) so copy edits stay readable and parse safely.
- Use `descriptionHtml` (not `description`) only when a role needs inline links.
- Preserve the user's preferred League framing: Ali shapes the product experience through AI-driven design workflows that use the design system; do not imply ownership of healthcare workflows.
- Keep text links underlined by default. On hover/focus, links should shift to the animated gradient color behavior used by `.gradient-link`, matching the icon hover pattern without flicker.

## Environment

- `baseUrl: "."` in `tsconfig.json` enables absolute imports from repo root.
