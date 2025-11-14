# eLife CSS Refactoring - Matching Native Patterns

This document describes how the `elife.css` file was refactored to replicate the actual CSS patterns from `https://elifesciences.org/assets/patterns/css/all.d18120fb.css`.

## Key Changes Made

### 1. **Exact Color Matching**
Replaced approximate colors with exact values from elifesciences.org:

```css
--color-elife-blue: #087acc;           /* Primary brand blue */
--color-elife-blue-hover: #0769b0;     /* Hover state */
--color-elife-dark: #212121;            /* Main text */
--color-elife-gray-text: #757575;       /* Secondary text */
--color-elife-border: #e0e0e0;          /* Border color */
--color-elife-bg-pale: #edeff4;         /* Pale background */
--color-elife-bg-light: #f7f7f7;        /* Light gray background */
--color-elife-bg-highlight: #f8f9fb;    /* Highlighted sections */
--color-elife-success: #629f43;         /* Success/green */
--color-elife-alert: #cf0c4e;           /* Alert/red */
```

### 2. **Typography System**
Matched eLife's exact font stacks and sizes:

```css
/* Fonts */
--font-family-sans: "Noto Sans", Arial, Helvetica, sans-serif;
--font-family-serif: "Noto Serif", Georgia, serif;
--font-family-mono: "Courier 10 Pitch", Courier, monospace;

/* Heading Sizes */
h1: 2.25rem
h2: 1.625rem (with padding: 1.3125rem 0)
h3: 1.375rem (with padding: 0.75rem 0)
```

### 3. **Button Patterns**
Replicated exact button padding and styling from eLife:

```css
/* Primary Button (button--default) */
.btn--primary {
  padding: 0.9375rem 2.25rem 0.875rem;
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.025em;
}

/* Secondary Button */
.btn--secondary {
  padding: 0.875rem 2.1875rem 0.8125rem;
  background-color: #f7f7f7;
  border: 1px solid #e0e0e0;
}

/* Outline Button */
.btn--outline {
  padding: 0.875rem 2.1875rem 0.8125rem;
  border: 1px solid #087acc;
}

/* Small Button */
.btn--small {
  padding: 0.1875rem 0.75rem;
}
```

### 4. **Container/Wrapper Width**
Used eLife's exact max-width:

```css
.wrapper,
.container {
  max-width: 69.625rem; /* 1114px - exact from eLife */
  padding: 0 1.5rem;
}

@media (min-width: 30em) {
  .wrapper,
  .container {
    padding: 0 3rem;
  }
}
```

### 5. **Link Styling with Dotted Underlines**
Added eLife's signature dotted underline on paragraph links:

```css
p a:not(.btn):not(.badge) {
  color: #212121;
  border-bottom: 1px dotted #212121;
  transition: colors;
}

p a:not(.btn):not(.badge):hover {
  color: #087acc;
  border-bottom-color: #087acc;
}
```

### 6. **Spacing System**
Used eLife's rem-based spacing:

```css
/* Section Padding */
padding: 3rem 0;          /* Base */
padding: 4.5rem 0;        /* Desktop (48em+) */

/* Common Gaps */
gap: 1.5rem;              /* 24px */
gap: 2.25rem;             /* 36px */
gap: 3rem;                /* 48px */
gap: 4.5rem;              /* 72px */
```

### 7. **Research Item (annotation-teaser pattern)**
Matched the exact padding and styling:

```css
.research-item {
  padding: 1.4375rem 1.25rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}

.research-item__number {
  width: 2.5rem;
  height: 2.5rem;
  background-color: #edeff4;
  color: #087acc;
}
```

### 8. **Badge Styling**
Exact badge patterns from eLife:

```css
.badge {
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.025em;
  padding: 0.25rem 0.75rem;
}

.badge--reviewed {
  color: #087acc;
  background-color: #e3f2fd;
}

.badge--research {
  color: #629f43;
  background-color: #e8f5e9;
}
```

### 9. **Grid Layouts**
Used CSS Grid with auto-fill patterns:

```css
.article-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.category-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 0.75rem;
}
```

### 10. **Footer Styling**
Matched exact footer colors:

```css
.site-footer {
  background-color: #212121;  /* Exact dark gray */
  color: #9e9e9e;             /* Link color */
}

.footer-column__title {
  color: #ffffff;
}

.site-footer__bottom {
  border-top-color: #424242;
  color: #757575;
}
```

## Design Patterns Replicated

### BEM Naming
All classes follow strict BEM methodology matching eLife:
- `.article-card` (Block)
- `.article-card__title` (Element)
- `.article-card--featured` (Modifier)

### Component Patterns
1. **block-link** → `article-card`
2. **annotation-teaser** → `research-item`
3. **button variants** → `.btn--primary`, `.btn--secondary`, `.btn--outline`
4. **teaser--main** → `magazine-card`

### Responsive Breakpoints
Used em-based media queries like eLife:
- `30em` (480px) - Increase container padding
- `48em` (768px) - Increase section padding
- `56.25em` (900px) - Grid adjustments
- `75em` (1200px) - Desktop layout

## Before vs After

### Before (Generic Tailwind)
```css
.btn--primary {
  @apply bg-blue-500 hover:bg-blue-600 text-white;
  @apply px-6 py-3 rounded-lg;
}
```

### After (eLife Exact Pattern)
```css
.btn--primary {
  background-color: #087acc;
  padding: 0.9375rem 2.25rem 0.875rem;
  font-size: 0.6875rem;
  text-transform: uppercase;
  letter-spacing: 0.025em;
  border-radius: 4px;
}

.btn--primary:hover {
  background-color: #0769b0;
}
```

## Benefits

1. **Pixel-Perfect Match**: Colors, spacing, and typography exactly match elifesciences.org
2. **Maintained BEM**: Clean, semantic class names in HTML
3. **Tailwind Power**: Still using `@apply` for reusable utilities
4. **Authentic Patterns**: Button padding, link styling, and component structure match production
5. **Proper Spacing**: rem-based system matches their design tokens

## Testing

To verify the styles match, compare:
- Button padding and text styling
- Link hover states with dotted underlines
- Heading sizes and line heights
- Container max-width (69.625rem)
- Color values throughout

The refactored CSS now accurately replicates eLife's design system while maintaining the BEM + Tailwind hybrid approach.
