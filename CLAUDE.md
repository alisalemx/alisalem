# CLAUDE.md

Guidance for Claude Code when working in this repository.

The full project reference — tech stack, structure, patterns, and conventions —
lives in **AGENTS.md**. Read it first:

@AGENTS.md

## Quick reference

Single-page Astro static site for [alisalem.ca](https://alisalem.ca), deployed
to Cloudflare Pages from `main`.

```sh
npm run dev      # local dev server
npm run build    # static build → dist/  (main verification step)
npm run preview  # preview production build
```

There are **no lint, format, or test scripts** — do not add them unless asked.
Verify changes with `npm run build`.

## Working notes for Claude

- **Content edits go in `src/content/profile.md`**, not in `index.astro`. That
  file's YAML frontmatter is the single source of truth for name, title,
  summary, links, and work history. Use `descriptionHtml` (not `description`)
  only when a role needs inline links; prefer folded scalars (`>-`) for long copy.
- **Tailwind v4, no config file.** Theme tokens and component classes
  (`.gradient-link`, `.contact-link`, `.home-logo-link`) live in
  `src/styles/global.css` via `@theme` and `@layer`. There is no `tailwind.config.js`.
- **Phosphor icons are raw SVG strings**, imported with `?raw` and modified by
  string replacement in `.astro` frontmatter — never treated as components.
- **Keep the page minimal**: intro/contact links plus Experience. Do not
  reintroduce a standalone About section unless requested.
- **Link styling**: underlined by default, animated gradient on hover/focus
  (matching `.gradient-link`) — no flicker.
- **League framing**: Ali shapes the product experience through AI-driven design
  workflows that use the design system; do not imply ownership of healthcare workflows.
