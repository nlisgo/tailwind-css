# eLife Website - BEM + Tailwind Hybrid Demo

This is a demonstration of the eLife Sciences website recreated using the BEM + Tailwind CSS hybrid approach.

## Files Created

- **src/elife.html** - Clean HTML using semantic BEM class names
- **src/css/elife.css** - Tailwind utilities applied via `@apply` directive
- **src/css/elife-compiled.css** - Compiled CSS output (auto-generated)

## What This Demonstrates

### Clean HTML with BEM Methodology
Instead of long utility class strings like:
```html
<div class="bg-white border border-gray-200 rounded overflow-hidden hover:shadow-lg transition-shadow duration-300">
```

We use semantic BEM classes:
```html
<article class="article-card">
```

### Tailwind Power in CSS
All styling is done in the CSS using Tailwind's `@apply` directive:
```css
.article-card {
  @apply bg-white border border-gray-200 rounded overflow-hidden;
  @apply hover:shadow-lg transition-shadow duration-300;
}
```

## Components Included

1. **Site Header** - Sticky navigation with logo and search
2. **Hero Section** - Large title with CTAs and category filter
3. **Highlights Grid** - Featured research articles in card layout
4. **Latest Research** - Numbered list with metadata and badges
5. **Magazine Section** - Insights, editorials, and collections
6. **Categories** - Browse by research discipline
7. **Footer** - Multi-column links and legal information

## Build Commands

```bash
# Build once
npm run build:elife

# Watch mode (auto-rebuild on changes)
npm run dev:elife

# Build both main site and eLife
npm run build:all
```

## Viewing the Page

### Locally
Simply open `src/elife.html` in your browser.

### GitHub Pages
The eLife demo is automatically deployed to GitHub Pages via the workflow:
- The main showcase will be at: `https://[username].github.io/[repo]/`
- The eLife demo will be at: `https://[username].github.io/[repo]/elife.html`

You can also navigate between pages:
- From the main showcase: Click the "eLife Demo" button in the navigation
- From the eLife page: Click "← Tailwind Showcase" in the navigation

The page is fully functional with:
- Clean, semantic HTML
- Responsive design (mobile-first)
- Hover states and transitions
- eLife brand colors and typography

## Key Benefits

✅ **Readable HTML** - Easy to understand component structure
✅ **Maintainable** - BEM naming convention everyone knows
✅ **Powerful** - Full access to Tailwind utilities
✅ **Flexible** - Easy to modify and extend
✅ **Team-Friendly** - Clear separation of concerns

## eLife Brand Colors

- Primary Blue: `#087acc`
- Dark Text: `#212121`
- Light Background: `#edf5fa`
- Gray Border: `#e0e0e0`

## Fonts

- **Noto Sans** - Headings, labels, and UI elements
- **Noto Serif** - Body text and article content

Both fonts are loaded from Google Fonts in the HTML.
