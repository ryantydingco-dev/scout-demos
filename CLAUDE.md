# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Static demo landing pages for a postcard campaign. Each top-level directory is an independent, single-file static site for one business (landscaping, plumbing, roofing, etc. in the Sumter / Columbia, SC area). There is no shared code, no build step, and no dependencies.

The root `index.html` and `README.md` are placeholders — the real content lives in the per-business subdirectories.

## Project layout

- `<business-slug>/index.html` — one self-contained HTML file per business. Slugs are kebab-cased from the business name.
- `video-<name>/index.html` — shorter message/landing pages (a different, simpler template) used for video-driven outreach.
- No `package.json`, no lockfile, no CI config, no linter config. Do not add tooling unless asked.

## The two page templates

There are two distinct templates in use — match the existing one when editing.

1. **Business landing page** (~870 lines, e.g. `a-notch-above-tree-lawn-care/index.html`)
   - Single `index.html` with inline `<style>` and inline `<script>`.
   - Dark theme using CSS custom properties defined in `:root` (`--color-bg: #0a0a0a`, `--color-accent: #22c55e`, etc.). Reuse these variables instead of hardcoding colors.
   - Fonts loaded from Google Fonts: Inter (sans) + Playfair Display (serif headings).
   - BEM-ish class naming (`.nav__links`, `.service-card`, `.contact__block`).
   - Inline JS at the bottom handles: scroll-aware nav (`#nav` gets `.scrolled`), mobile menu close on link click, and IntersectionObserver fade-in for `.service-card`, `.review-card`, `.about__detail`.
   - Sections are delimited by `<!-- ═══════ NAME ═══════ -->` banner comments — preserve this style.
   - Footer copyright year is currently `2026`.

2. **Video message page** (~154 lines, the three `video-*` directories)
   - Much simpler: centered single-column message, Inter font only, dark background.

## Conventions when editing business pages

- Keep each page fully self-contained — no shared CSS/JS files, no relative imports between sibling directories.
- Business-specific data to update per page: `<title>`, meta description, `tel:` links, street address, Google Maps `cid=...` URL, business hours, service-area copy, footer business name.
- External links to Google Maps and `tel:` numbers should keep `target="_blank" rel="noopener"` where already present.
- When cloning a page for a new business, copy an existing business page (not the `video-*` template) and replace the business-specific fields listed above.

## Commands

There is nothing to build, lint, or test. To preview a page locally, open the file directly or serve the repo root:

```
python3 -m http.server 8000
# then visit http://localhost:8000/<business-slug>/
```

## Git workflow

Recent history shows bulk deploy commits (e.g. "Deploy 69 demo sites for postcard campaign", "Deploy 3 video pages"). When adding or updating many pages at once, a single commit describing the batch is consistent with the existing style.
