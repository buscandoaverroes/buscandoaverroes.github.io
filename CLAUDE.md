# Instructions for Claude/AI Agents

## Working Style

- **Ask before guessing:** If MIGRATION.md or ARCHITECTURE.md is ambiguous, ask rather than assume.
- **Build incrementally:** Scaffold → components → content → styling → deployment. Test at each step.
- **Explain changes:** Summarize what you built and why, especially if deviating from the spec. Assume user has coding knowledge; be concise.
- **Keep it simple:** Prefer readable, straightforward code over clever solutions.
- **Be careful about Personal Information:** Ensure only minimum personal information necessary is included.
- **Prepare commit messages/pull request content but never commit or push code** User will review, commit, and push everything.

## Code Preferences

- **Language/Format:** JavaScript/TypeScript for Astro components
- **Indentation:** 2 spaces
- **Naming:** camelCase for JS, PascalCase for Astro component files
- **No external dependencies** unless discussed (keep `package.json` lean)
- **Accessibility:** Semantic HTML, alt text for images, keyboard navigation

## Project Specifics

- **Astro version:** Latest stable
- **CSS:** Plain CSS preferred (Tailwind optional if you want it, but not required)
- **Responsive:** universal-first design (works on phone, tablet, desktop)
- **Performance:** Lazy-load images, minimize JavaScript bundles (Astro default is fine)

## Workflow

1. Create Astro scaffold with folder structure from ARCHITECTURE.md
2. Build components (Hero, WorkHistory, About, Links) as `.astro` files
3. Populate with content from `docs/newcontent.md`
4. Add GitHub Actions deploy workflow (`.github/workflows/deploy.yml`)
5. Test locally, ensure no build errors
6. Ready to push and deploy

## Ambiguity Handling

- **Design/styling:** If not specified, use clean, minimal single-column layout with good typography
- **Component data:** If content source is unclear, ask whether to hardcode, import from markdown, or accept props
- **Deployment:** Assume GitHub Pages, `[username].github.io` repo, `main` branch
- **Content updates:** Default assumption is human edits `.astro` component props or markdown directly

## Testing

- Build succeeds locally (`npm run build`)
- No console errors or warnings
- Manual check: homepage renders correctly in browser
- Links and navigation work

## When Done

User will push to `main` and start GitHub Actions runs, site deploys to GitHub Pages. Provide:
1. Summary of what was built (concise -- user can dive into details)
2. Any decisions made (e.g., styling approach, component structure)
3. Instructions for future content updates
4. Known limitations or next steps (if any)
