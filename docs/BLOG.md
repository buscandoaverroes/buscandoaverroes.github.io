# Writing a Blog Post (Essays)

The site's blog is called "Essays" and is a Markdown-based content collection. Writing and publishing a post takes three steps.

## 1. Write the file

Create a new `.md` file in `src/content/essays/`. Name it with lowercase and hyphens — the filename becomes the URL:

```
src/content/essays/my-first-essay.md  →  /essays/my-first-essay
```

Start the file with frontmatter, then the post body in standard Markdown:

```markdown
---
title: "My First Essay"
description: "A one-line subtitle (optional)"
date: 2026-08-02
draft: false
---

Your content goes here. Standard Markdown is supported: **bold**, *italic*,
[links](https://example.com), `code`, code blocks, lists, blockquotes, and images
(place images in `public/images/` and reference them as `/images/filename.jpg`).
```

### Frontmatter fields

Schema is defined in [`src/content/config.ts`](../src/content/config.ts):

| Field         | Required | Type    | Notes                                      |
| ------------- | -------- | ------- | ------------------------------------------- |
| `title`       | Yes      | string  | Displayed as the page and list heading      |
| `date`        | Yes      | date    | `YYYY-MM-DD`, used for sort order           |
| `description` | No       | string  | Optional subtitle shown under the title     |
| `draft`       | No       | boolean | Defaults to `false`. Set `true` to hide it  |

## 2. Preview locally

```bash
npm run dev
```

Visit `http://localhost:4321` — non-draft essays appear under "Essays & Reflections" on the homepage, newest first, and each links to its own page at `/essays/<filename>`.

## 3. Publish

Commit the new file on a branch (see `CLAUDE.md`'s Git Workflow), push, and let the user review/merge to `main`. The deploy workflow builds and publishes automatically.

## Drafts

Leave `draft: true` while a post is a work in progress — it's excluded from both the homepage list and page generation, so half-written essays are safe to commit without going live. Flip it to `false` when ready.

## Notes

- The essay feature is toggled at `settings.json` → `features.essays` (currently `true`). This is the *only* place it's toggled — there is no per-component flag to edit.
- Essay page styling (typography, code blocks, blockquotes) lives in [`src/layouts/EssayLayout.astro`](../src/layouts/EssayLayout.astro).
- Sort order and date formatting are set in [`src/components/Essays.astro`](../src/components/Essays.astro), if you ever want to change them (e.g. oldest-first, or a different date format).
