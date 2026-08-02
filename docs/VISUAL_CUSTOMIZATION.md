# Visual Customization

Three visual features are built into the site. All are controlled through `settings.json` and/or `src/styles/global.css` — no component code changes needed for normal use.

## Background zones

Alternating sections (Work History, Essays) get a subtle alternate background for visual rhythm; Hero, About, and Links use the default background.

To change the alternate color, edit `--color-bg-alt` in `src/styles/global.css` — it's set once for light mode (`:root`) and once for dark mode (inside the `@media (prefers-color-scheme: dark)` block).

## Timeline colors

Work History entries show a colored marker based on their `category` field (`work`, `education`, or `teaching`), set per-entry in `settings.json` → `workHistory[]`.

The actual colors come from `settings.json` → `theme.colorScheme`, which selects a palette from `settings.json` → `colorSchemes`. Three palettes ship by default: `blue` (default), `purple`, `green`. Switch between them with:

```json
"theme": { "colorScheme": "purple" }
```

To add a custom palette, add a new entry to `colorSchemes` with `timeline-work`, `timeline-education`, and `timeline-teaching` hex values, then set `theme.colorScheme` to its key. `Layout.astro` injects these as CSS custom properties (`--timeline-work`, etc.) at build time — no component edits needed.

To add a new category beyond the three built in, you'd also need to add a matching `.marker-<category>` rule in `src/components/WorkHistory.astro`'s `<style>` block.

## Photo accents

A small circular photo can appear next to a section heading. Currently used on About (`settings.json` → `about.enablePhotoAccents`, `about.photoSrc`, `about.photoAlt`).

```json
"about": {
  "enablePhotoAccents": true,
  "photoSrc": "/images/your-photo.jpg",
  "photoAlt": "A short, real description of the photo"
}
```

Place the image in `public/images/`; keep it optimized (roughly 100–300KB) since it's served as-is with no build-time image processing. Always fill in `photoAlt` with a real description — it's not decorative.

The same pattern (photo next to a heading) could be added to other sections by following `About.astro`'s `about-header` / `about-image` structure.

## After any change

Visual/settings changes require a rebuild to see in production:

```bash
npm run build
npm run preview
```
