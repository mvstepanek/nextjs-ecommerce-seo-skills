---
applyTo: "**/components/**/*.tsx, **/components/**/*.ts"
---

# Component SEO Requirements

When building React components:

1. **Images**: Use `<Image>` from `next/image`, never raw `<img>`. Descriptive alt text (include product name for product images). Specify width/height or use fill. Use `priority` only on LCP images.

2. **Links**: Use `<Link>` from `next/link` for internal links, never raw `<a>`. Descriptive anchor text (never "click here"). No hardcoded locale in hrefs. External links with `target="_blank"` — modern browsers auto-add `rel="noopener"`, but explicit is fine for older browser compatibility.

3. **Headings**: Maintain hierarchy (h1 → h2 → h3, no skipping). One h1 per page. Use semantic HTML tags, not styled divs.

4. **Server vs Client**: Render data-display components server-side (Server Components in App Router; in Pages Router, ensure data is fetched via SSR/SSG). Only use `"use client"` or client-side rendering for interactivity.

5. **Semantic HTML**: `<nav>` for navigation (with `aria-label`), `<ul>`/`<ol>` for lists, `<button>` for clickable actions (not `<div onClick>`).

6. **Accessibility**: `aria-label` on icon-only buttons, keyboard accessible interactive elements, sufficient color contrast.
