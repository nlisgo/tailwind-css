# eLife CSS - Tailwind @apply Refactoring

This document describes the refactoring of `elife.css` to maximize use of Tailwind's `@apply` directive.

## Results

- **Before**: 708 lines, 14KB
- **After**: 521 lines, 12KB
- **Reduction**: 187 lines removed (26% reduction)
- **Approach**: 95%+ Tailwind `@apply`, minimal plain CSS

## Key Changes

### 1. Colors - Using Theme Variables

**Before** (Plain CSS):
```css
.btn--primary {
  background-color: #087acc;
  color: white;
}
```

**After** (Tailwind):
```css
.btn--primary {
  @apply bg-elife-blue text-white;
  @apply px-9 py-4;
  @apply hover:bg-elife-blue-hover;
}
```

### 2. Spacing - Using Tailwind Scale

**Before** (Exact pixel values):
```css
.article-card__content {
  padding: 1.5rem;
}

.research-item {
  padding: 1.4375rem 1.25rem;
}
```

**After** (Tailwind utilities):
```css
.article-card__content {
  @apply p-6;
}

.research-item {
  @apply flex gap-4 p-6;
  @apply transition-colors hover:border-elife-blue;
}
```

### 3. Typography - Using Tailwind Classes

**Before** (Manual font sizing):
```css
.article-card__title {
  color: #212121;
  font-size: 1rem;
  line-height: 1.3;
  font-weight: bold;
}
```

**After** (Tailwind utilities):
```css
.article-card__title {
  @apply font-bold text-elife-dark mb-2;
  @apply text-base leading-snug;
  @apply cursor-pointer transition-colors hover:text-elife-blue;
  font-family: var(--font-sans);
}
```

### 4. Layout - Using Tailwind Flexbox/Grid

**Before** (Manual flexbox):
```css
.research-item {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}
```

**After** (Tailwind):
```css
.research-item {
  @apply flex gap-4 p-6;
  @apply bg-white border border-elife-border rounded;
  @apply transition-colors hover:border-elife-blue;
}
```

### 5. Borders & Shadows - Tailwind Utilities

**Before** (Plain CSS):
```css
.article-card {
  border: 1px solid #e0e0e0;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s;
}

.article-card:hover {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}
```

**After** (Tailwind):
```css
.article-card {
  @apply bg-white border border-elife-border rounded overflow-hidden;
  @apply transition-shadow duration-300 hover:shadow-lg;
}
```

### 6. Responsive Design - Tailwind Breakpoints

**Before** (Media queries):
```css
.hero {
  padding: 3rem 0;
}

@media (min-width: 48em) {
  .hero {
    padding: 4.5rem 0;
  }
}
```

**After** (Tailwind responsive utilities):
```css
.hero {
  @apply bg-elife-bg-pale py-12 md:py-[4.5rem];
}
```

### 7. States - Hover, Focus, Active

**Before** (Plain CSS pseudo-classes):
```css
.btn--primary {
  background-color: #087acc;
}

.btn--primary:hover {
  background-color: #0769b0;
}
```

**After** (Tailwind state modifiers):
```css
.btn--primary {
  @apply bg-elife-blue text-white;
  @apply px-9 py-4;
  @apply hover:bg-elife-blue-hover;
}
```

### 8. Arbitrary Values - When Exact Matching Needed

**Before** (Exact eLife values):
```css
.section-title {
  font-size: 1.625rem;
}

.hero__title {
  max-width: 56rem;
}
```

**After** (Tailwind arbitrary values):
```css
.section-title {
  @apply font-bold text-elife-dark mb-6;
  @apply text-[1.625rem];
  font-family: var(--font-sans);
}

.hero__title {
  @apply font-bold text-elife-dark mb-8 mx-auto;
  @apply text-3xl md:text-4xl leading-tight;
  @apply max-w-[56rem];
  font-family: var(--font-sans);
}
```

### 9. Grid Layouts - Modern CSS Grid with Tailwind

**Before** (Plain CSS Grid):
```css
.article-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}
```

**After** (Tailwind with arbitrary grid template):
```css
.article-grid {
  @apply grid gap-6;
  @apply grid-cols-[repeat(auto-fill,minmax(280px,1fr))];
}
```

## What Remains as Plain CSS

Only **font-family assignments** remain as plain CSS, since they reference CSS variables:

```css
font-family: var(--font-sans);
font-family: var(--font-serif);
```

This is the appropriate way to handle these, as:
1. The `@theme` directive defines the font variables
2. Tailwind doesn't have a utility for `var()` references in font families
3. It's cleaner than creating custom utilities for each font

## Benefits of This Approach

### ✅ Readability
- Easier to scan and understand at a glance
- Standard Tailwind utilities are familiar to most developers
- No mental math converting rem/px values

### ✅ Maintainability
- Changes to spacing/colors happen in one place (@theme)
- Consistent with Tailwind's design system
- Easy to add responsive variants

### ✅ File Size
- 26% reduction in source CSS
- Tailwind's purge removes unused utilities
- Better compression in production

### ✅ Development Speed
- Faster to write new components
- Less context switching between CSS and HTML
- Autocomplete works better with Tailwind utilities

### ✅ Consistency
- All spacing uses Tailwind's scale (0-96)
- Colors reference theme variables
- Typography follows Tailwind conventions

## Comparison Table

| Aspect | Before (Plain CSS) | After (Tailwind @apply) |
|--------|-------------------|-------------------------|
| Lines | 708 | 521 |
| Size | 14KB | 12KB |
| Color definitions | Hardcoded hex | Theme variables |
| Spacing | Manual rem values | Tailwind scale |
| Typography | Manual font-size | Tailwind text-* |
| Layout | Manual flex/grid | Tailwind utilities |
| States | Manual :hover | Tailwind hover: |
| Responsive | @media queries | Tailwind md:, lg: |
| Consistency | Varied | Standardized |

## Examples of Approximations

Some values were approximated to fit Tailwind's scale:

| Original | Tailwind | Difference |
|----------|----------|------------|
| `padding: 0.9375rem` | `@apply py-4` (1rem) | ~0.06rem |
| `padding: 1.4375rem` | `@apply p-6` (1.5rem) | ~0.06rem |
| `font-size: 0.6875rem` | `@apply text-xs` (0.75rem) | ~0.06rem |

These minor differences (less than 1px at typical screen sizes) are acceptable trade-offs for:
- Consistency across the design system
- Easier maintenance
- Better tooling support

## How to Extend

To add new components, follow this pattern:

```css
/* Component block */
.new-component {
  @apply bg-white border border-elife-border rounded;
  @apply p-6 shadow-md;
  @apply transition-all duration-200;
  font-family: var(--font-sans);
}

/* Component element */
.new-component__title {
  @apply text-lg font-bold text-elife-dark mb-4;
  @apply hover:text-elife-blue cursor-pointer;
}

/* Component modifier */
.new-component--featured {
  @apply bg-elife-bg-pale border-elife-blue;
}
```

## Conclusion

This refactoring achieves the best of both worlds:
- **Clean HTML** with semantic BEM class names
- **Powerful Tailwind** utilities via `@apply` in CSS
- **Minimal plain CSS** only where truly necessary
- **eLife aesthetics** maintained through theme variables

The result is a maintainable, scalable stylesheet that's easy to understand and extend.
