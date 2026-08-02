# Instructions for Claude/AI Agents

## Working Style

- **Ask before guessing:** If README.md or docs/ is ambiguous about intended behavior, ask rather than assume.
- **Build incrementally:** Changes → local test → styling/content check. Test at each step.
- **Explain changes:** Summarize what you built and why, especially if deviating from the spec. Assume user has coding knowledge; be concise.
- **Keep it simple:** Prefer readable, straightforward code over clever solutions.
- **Be careful about Personal Information:** Ensure only minimum personal information necessary is included.
- **Prepare commit messages/pull request content but never commit or push code** User will review, commit, and push everything.
- **Never work directly on `main`:** see Git Workflow below.

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

The site is operational, not mid-migration. Typical work is incremental:

1. Understand the request against current code (`settings.json` for content/config, `src/components/` for structure, `docs/` for how things work)
2. Make the change on a feature branch (see Git Workflow)
3. Test locally (`npm run build` / `npm run dev`)
4. Summarize the change and prepare a commit message; user reviews, commits, pushes, and opens/merges the PR

## Git Workflow

Simple feature-branch flow — no `develop` or `release/*` branches, this is a solo personal-site repo:

- **`main` is always deployable.** Every push to `main` triggers the GitHub Pages deploy workflow (`.github/workflows/deploy.yml`), so nothing half-finished belongs there.
- **Do all work on a short-lived branch off `main`**, named by intent: `feature/*` (new capability), `fix/*` (bug fix), `chore/*` (docs, CI, cleanup, dependency bumps).
- **Merge back via PR** (preferred, gives a review point and keeps the Actions log per-change) or a direct local merge for trivial changes — the user decides which, and performs the merge/push themselves per the rule above.
- **Delete the branch after merging** to keep the branch list clean.
- Commit messages: short imperative summary line (e.g. "Add secret-scanning CI workflow"), body only if the "why" isn't obvious from the diff.

## Ambiguity Handling

- **Design/styling:** If not specified, use clean, minimal single-column layout with good typography
- **Component data:** If content source is unclear, ask whether it belongs in `settings.json`, a markdown content collection, or a component prop
- **Deployment:** Assume GitHub Pages, `[username].github.io` repo, deploys from `main`
- **Content updates:** Default assumption is the human edits `settings.json` directly, or adds/edits markdown files under `src/content/essays/` for blog posts

## Testing

- Build succeeds locally (`npm run build`)
- No console errors or warnings
- Manual check: homepage renders correctly in browser
- Links and navigation work

## When Done

User will push the feature branch, review/merge into `main` (which triggers GitHub Actions and deploys to GitHub Pages). Provide:
1. Summary of what was built (concise -- user can dive into details)
2. Any decisions made (e.g., styling approach, component structure)
3. Instructions for future content updates
4. Known limitations or next steps (if any)
