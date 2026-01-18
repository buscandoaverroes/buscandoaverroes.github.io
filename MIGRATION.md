# Website Migration: Blogdown → Astro

## Overview
Migrating a professional landing page from blogdown (RMarkdown-based) to Astro. This is a rewrite opportunity—not a 1:1 port. Old site is being sunset; temporary downtime is acceptable.

## Scope

### In Scope
- Astro project scaffold with modern tooling
- Convert `docs/newcontent.md` into Astro pages/components
- Static site: no CMS, no database
- GitHub Pages deployment via GitHub Actions
- Responsive design (mobile-friendly)

### Out of Scope
- Analytics/tracking integrations (can add later)
- Blog/dynamic content
- Comments, forms, or user interactions
- SEO optimization beyond basics (titles, meta, sitemap)

## Content Structure

Source: `docs/newcontent.md` (already rewritten)

Sections to implement:
1. **Hero** — Brief intro + call-to-action
2. **Work History** — Mini CV / role timeline
3. **About** — Bio paragraph(s)
4. **Links** — Portfolio, GitHub, LinkedIn, email, etc.
5. **Footer** — Copyright, optional social links

## Technical Requirements

### Stack
- **Framework:** Astro (latest, with markdown support)
- **Styling:** CSS (Tailwind optional, but recommended for responsive design)
- **Hosting:** GitHub Pages via `[username].github.io` repo
- **Deployment:** GitHub Actions workflow (build on push to `main`, deploy to Pages)

### Project Structure
```
src/
  ├── layouts/
  │   └── Layout.astro          # Base layout wrapper
  ├── components/
  │   ├── Hero.astro
  │   ├── WorkHistory.astro
  │   ├── About.astro
  │   └── Links.astro
  ├── pages/
  │   └── index.astro           # Homepage (only page)
  └── styles/
      └── global.css            # Global styles

public/
  └── (favicon, images if any)

.github/workflows/
  └── deploy.yml               # GitHub Pages deployment action
```

### Key Decisions
- **Single page:** All sections on `src/pages/index.astro`
- **Content as components:** Each section (`Hero.astro`, `WorkHistory.astro`, etc.) receives data/props and renders
- **Markdown for content:** Keep content readable; consider `docs/newcontent.md` as structured data or convert sections to `.astro` components
- **No dynamic imports:** Everything static, zero JavaScript by default

## Done Criteria

- [ ] Astro project created and dependencies installed
- [ ] GitHub Actions workflow builds and deploys to GitHub Pages without errors
- [ ] Homepage renders at `https://[username].github.io` with all 5 sections
- [ ] Content matches `docs/newcontent.md` layout and messaging
- [ ] Mobile responsive (readable on phone/tablet)
- [ ] Links work (portfolio, GitHub, email, etc.)
- [ ] Page loads with good performance (Lighthouse > 90)
- [ ] Future content updates are trivial (markdown edits or component prop changes)

## Getting Started

1. Agent creates Astro scaffold (`npm create astro@latest`)
2. Implements component structure from `ARCHITECTURE.md`
3. Populates components with content from `docs/newcontent.md`
4. Adds GitHub Actions deploy workflow
5. Tests locally, then pushes to repo

## Notes

- Old repos (`[old-source-repo]`, `[username].github.io` old) are archived, not deleted
- Site will be down during migration—acceptable
- Design can be minimal/clean; prioritize readability over complexity
- If unsure on styling, use a simple single-column layout with clear hierarchy
