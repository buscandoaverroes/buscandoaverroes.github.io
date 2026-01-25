# Personal Landing Page

A clean, minimal personal landing page built with Astro. Features dark/light mode support, responsive design, and accessibility-first approach.

## Tech Stack

- **Framework**: Astro (latest stable)
- **Styling**: Plain CSS with custom properties
- **Deployment**: GitHub Pages via GitHub Actions
- **Accessibility**: Semantic HTML, skip links, keyboard navigation

## Project Structure

```
/
├── public/
│   └── favicon.svg          # Site favicon (can be replaced)
├── src/
│   ├── components/          # Reusable Astro components
│   │   ├── Hero.astro
│   │   ├── WorkHistory.astro
│   │   ├── About.astro
│   │   ├── Essays.astro
│   │   ├── Links.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Layout.astro     # Base HTML layout
│   ├── pages/
│   │   └── index.astro      # Homepage (assembles all components)
│   └── styles/
│       └── global.css       # Design tokens & global styles
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Actions deployment
└── astro.config.mjs         # Astro configuration
```

## Development Commands

All commands are run from the root of the project:

| Command           | Action                                      |
| :---------------- | :------------------------------------------ |
| `npm install`     | Install dependencies                        |
| `npm run dev`     | Start dev server at `localhost:4321`        |
| `npm run build`   | Build production site to `./dist/`          |
| `npm run preview` | Preview production build locally            |

## Settings Configuration

**All site content and visual settings are centralized in `settings.json`** at the project root. This makes updating your site simple - edit one file instead of hunting through multiple components.

### Configuration File: `settings.json`

The settings file controls:
- **Site metadata** (name, title, language)
- **Hero section** (name, subtitle, background image, CTA button)
- **Feature toggles** (enable/disable sections like Essays, Work History, etc.)
- **Color schemes** (timeline colors)
- **Content** (work history, about section, links)

**Example structure:**
```json
{
  "site": { "name": "Tom Mosher", "title": "Tom Mosher", "language": "en" },
  "hero": {
    "name": "[Your Name]",
    "subtitle": "Your tagline here",
    "backgroundImage": {
      "enabled": true,
      "src": "/images/sakura3.jpg",
      "opacity": 0.15,
      "position": "center"
    },
    "showCTA": false
  },
  "theme": { "colorScheme": "blue" },
  "features": { "essays": false, "workHistory": true }
}
```

### Quick Updates

**Change your name/subtitle:**
```json
"hero": {
  "name": "Jane Doe",
  "subtitle": "Engineer, Writer, Explorer"
}
```

**Toggle the hero background image:**
```json
"hero": {
  "backgroundImage": {
    "enabled": false  // Set to false to hide background
  }
}
```

**Switch color schemes:**
```json
"theme": { "colorScheme": "purple" }  // Options: blue, purple, green
```

**Add/edit work history:**
```json
"workHistory": [
  {
    "role": "Software Engineer",
    "organization": "Tech Company",
    "location": "San Francisco, CA",
    "description": "Built amazing things...",
    "current": true,
    "category": "work"  // Options: work, education, teaching
  }
]
```

**Add new links:**
```json
"links": [
  { "name": "GitHub", "url": "https://github.com/username", "description": "Code" },
  { "name": "LinkedIn", "url": "https://linkedin.com/in/username", "description": "Professional" }
]
```

### Color Schemes

Three pre-defined color schemes control the timeline marker colors:

- **blue** (default): Blue for work, green for education, orange for teaching
- **purple**: Purple for work, teal for education, orange for teaching
- **green**: Green for work, cyan for education, yellow for teaching

To switch schemes, edit `settings.json`:
```json
"theme": { "colorScheme": "purple" }
```

**Adding custom color schemes:**
1. Add a new scheme to the `colorSchemes` object in `settings.json`:
```json
"colorSchemes": {
  "blue": { ... },
  "custom": {
    "timeline-work": "#FF5733",
    "timeline-education": "#33FF57",
    "timeline-teaching": "#3357FF"
  }
}
```
2. Set `theme.colorScheme` to `"custom"`
3. Rebuild the site

### Hero Background Image

The hero section supports a background image with automatic overlay for text readability.

**To change the background image:**
1. Place your image in `public/images/` (e.g., `public/images/mountains.jpg`)
2. Update `settings.json`:
```json
"hero": {
  "backgroundImage": {
    "enabled": true,
    "src": "/images/mountains.jpg",
    "opacity": 0.15,           // 0.0 (invisible) to 1.0 (fully visible)
    "position": "center"        // CSS background-position value
  }
}
```

**Background image notes:**
- Image is automatically cropped to fit (`background-size: cover`)
- No distortion - aspect ratio is preserved
- Overlay opacity can be adjusted (0.10-0.20 recommended for readability)
- For large images (>1MB), consider optimizing with tools like [Squoosh](https://squoosh.app/)

## Updating Content (Legacy)

**Note:** With v0.1, most content is now in `settings.json`. The instructions below apply if you need to customize component logic.

### Hero Section
Edit `src/components/Hero.astro`:
- `name`: Update placeholder "[Your Name]"
- `subtitle`: Update tagline
- `ctaText` / `ctaLink`: Update call-to-action

**Adding a second button:**
To add a second button/link below the hero (e.g., "Resume" or "Contact"), edit the frontmatter and template:

```astro
---
const name = "[Your Name]";
const subtitle = "Software Engineer, Researcher, Educator, Non-profit Leader";
const ctaText = "Learn more about my work";
const ctaLink = "#about";

// Add these lines for second button
const ctaText2 = "View Resume";
const ctaLink2 = "/resume.pdf";  // or external link: "https://..."
---

<section class="hero">
  <div class="container">
    <h1 class="hero-title">{name}</h1>
    <p class="hero-subtitle">{subtitle}</p>
    <div class="hero-cta-group">
      <a href={ctaLink} class="hero-cta">{ctaText}</a>
      <a href={ctaLink2} class="hero-cta hero-cta-secondary">{ctaText2}</a>
    </div>
  </div>
</section>
```

Then add this CSS to the `<style>` section:

```css
.hero-cta-group {
  display: flex;
  gap: var(--space-md);
  justify-content: center;
  flex-wrap: wrap;
}

.hero-cta-secondary {
  background-color: transparent;
  color: var(--color-accent);
  border: 2px solid var(--color-accent);
}

.hero-cta-secondary:hover {
  background-color: var(--color-accent);
  color: white;
}
```

### Work History
Edit `src/components/WorkHistory.astro`:
- Add/remove/edit items in the `workHistory` array
- Set `current: true` for your current role

### About Section
Edit `src/components/About.astro`:
- `humanLanguages`: Add/remove languages
- `programmingLanguages`: Add/remove languages
- `interests`: Update hobbies
- `currentInterests`: Add/remove/edit current interests
- `favoriteLibraries`: Add/remove/edit favorite tools

### Essays (Markdown System)

The site includes a full markdown-based essay publishing system (currently disabled).

**To enable and use:**
1. Set `enableMarkdownEssays = true` in `src/components/Essays.astro` (line 6)
2. Create `.md` files in `src/content/essays/`
3. Set `draft: false` in essay frontmatter
4. Rebuild the site

**Demo essay included:** `src/content/essays/demo-hello-world.md` (currently a draft)

**Full documentation:** See `ESSAYS_GUIDE.md` for complete instructions on:
- Writing essays in Markdown
- Managing drafts
- Customizing essay layout
- Adding features (tags, reading time, etc.)

### Links
Edit `src/components/Links.astro`:
- Add new links to the `links` array
- Structure: `{ name, url, description }`

## Styling

Customize design tokens in `src/styles/global.css`:
- **Colors**: Update CSS custom properties in `:root`
- **Dark mode**: Edit `@media (prefers-color-scheme: dark)` section
- **Typography**: Adjust font sizes, families, and line heights
- **Spacing**: Modify spacing scale (8px base unit)

## Deployment

### First-Time Setup

**1. Configure GitHub Pages:**
   - Go to your repository on GitHub
   - Navigate to **Settings** > **Pages** (in the left sidebar)
   - Under "Source", select **GitHub Actions**
   - Save (GitHub will now use the workflow in `.github/workflows/deploy.yml`)

**2. Verify workflow file exists:**
   - Check that `.github/workflows/deploy.yml` is present in your repository
   - This file is already configured for GitHub Pages deployment

**3. Push to main branch:**
   ```bash
   git add .
   git commit -m "Deploy Astro site to GitHub Pages"
   git push origin main
   ```

**4. Monitor the deployment:**
   - Go to the **Actions** tab in your GitHub repository
   - You should see a "Deploy to GitHub Pages" workflow running
   - Wait for both "build" and "deploy" jobs to complete (usually 1-2 minutes)
   - Green checkmark = successful deployment

**5. Access your live site:**
   - Once deployed, visit: `https://buscandoaverroes.github.io`
   - First deployment may take a few extra minutes to propagate

### Continuous Deployment

After initial setup, updates are automatic:

1. **Edit content** (usually just `settings.json`)
2. **Test locally** (optional but recommended):
   ```bash
   npm run build
   npm run preview
   # Visit http://localhost:4321
   ```
3. **Commit and push:**
   ```bash
   git add .
   git commit -m "Update hero subtitle"
   git push origin main
   ```
4. **GitHub Actions automatically builds and deploys** - check the Actions tab to monitor progress

### Troubleshooting Deployment

**Build fails:**
- Check the Actions tab for error messages
- Common issues:
  - Syntax error in `settings.json` (validate JSON at [jsonlint.com](https://jsonlint.com))
  - Missing image files referenced in settings
  - Typo in color scheme name

**Site doesn't update:**
- Hard refresh your browser (Cmd+Shift+R on Mac, Ctrl+Shift+R on Windows)
- Check that the workflow completed successfully in Actions tab
- Verify you pushed to the `main` branch

**404 error:**
- Confirm GitHub Pages source is set to "GitHub Actions" in repository settings
- Check that the `site` and `base` values in `astro.config.mjs` match your repository name

## Design Principles

- **Simplicity**: Clean, minimal design with simple colors
- **Adaptability**: Responsive (mobile/tablet/desktop), dark/light mode
- **Accessibility**: Semantic HTML, keyboard navigation, WCAG AA contrast
- **Performance**: No external dependencies, optimized assets
- **Universal Design**: Language-agnostic aesthetics

## Features

- ✅ CSS-only dark/light mode (respects system preference)
- ✅ Responsive design (mobile-first)
- ✅ Accessibility (skip links, focus indicators, semantic HTML)
- ✅ Timeline visualization for work history
- ✅ Minimal JavaScript (only what Astro needs)
- ✅ Fast builds and deployments

## Version History

### Version 0.1 ✅ (Completed)
- ✅ Added hero background image with automatic overlay
- ✅ Removed SEO metadata and analytics (site is minimal by default)
- ✅ Comprehensive deployment documentation
- ✅ Color scheme system with 3 pre-defined palettes
- ✅ Centralized `settings.json` for all content and configuration
- ✅ Removed "Learn more about my work" CTA button (controlled by `hero.showCTA`)

### Version 0.2 (Future)
- Internationalization (language switcher)



## License

See LICENSE file for details.

## Acknowledgements
Thanks to Claude 4.5!
