# SEO Component Audit

Review the React component at `$ARGUMENTS` for SEO implications.

## Instructions

1. **Read the target component** at `$ARGUMENTS`
2. **Identify the component type** (navigation, product card, image gallery, breadcrumbs, footer, etc.)
3. **Check each relevant item** below
4. **Output a focused review** with actionable recommendations

## Checks

### Images
- [ ] Uses `<Image>` from `next/image` — no raw `<img>` tags
- [ ] Every meaningful image has a descriptive `alt` prop
- [ ] Alt text is not generic ("image", "photo", "icon", "banner", "placeholder")
- [ ] Product images include the product name in alt text
- [ ] Decorative-only images use `alt=""`
- [ ] Images have `width`/`height` or use `fill` with sized container
- [ ] Hero/main images use `priority` prop

### Links
- [ ] Internal links use `<Link>` from `next/link` — no raw `<a>` for internal URLs
- [ ] Anchor text is descriptive (no "click here", "read more")
- [ ] No hardcoded locale in href — uses dynamic locale param or relative paths
- [ ] External links with `target="_blank"` — `rel="noopener"` is auto-added by modern browsers but explicit is fine for compatibility
- [ ] No `rel="nofollow"` on internal links

### Headings
- [ ] Heading hierarchy is correct — no skipping levels (h1 > h3 without h2)
- [ ] Only one `<h1>` per page (if this component contains an h1, verify it's the only one)
- [ ] Headings use semantic HTML (`<h2>`, `<h3>`), not styled `<div>` or `<span>`

### Semantic HTML
- [ ] Navigation uses `<nav>` with `aria-label`
- [ ] Lists use `<ul>`/`<ol>` + `<li>`, not `<div>` chains
- [ ] Buttons use `<button>`, not `<div onClick>`
- [ ] Form elements have associated `<label>` elements
- [ ] Main content areas use `<main>`, `<section>`, `<article>` where appropriate

### Server vs Client Rendering
- [ ] Component only uses client-side rendering (`"use client"` / `useEffect`) if it needs interactivity
- [ ] Data-display components (product info, specs, breadcrumbs) are server-rendered
- [ ] Critical SEO content (product name, description, headings) is not behind `useEffect`
- [ ] If `"use client"` is used, could any part be split into a Server Component?

### Accessibility (SEO-relevant)
- [ ] Interactive elements are keyboard accessible
- [ ] Images have alt text (redundant with images check, but important)
- [ ] Color contrast is sufficient (affects usability metrics which correlate with SEO)
- [ ] `aria-label` on icon-only buttons and links
- [ ] Skip navigation link present if this is a nav component

## Report Format

```
## Component SEO Review: {filename}
Component type: {navigation|product-card|image-gallery|breadcrumbs|footer|form|etc.}

### Issues Found
1. FAIL: Line N — Raw <img> tag used instead of next/image
2. WARN: Line N — Generic alt text "product thumbnail"
3. FAIL: Line N — "use client" but component only displays data, no interactivity

### Good Practices
- Uses next/link for all internal navigation
- Proper heading hierarchy (h2 > h3)

### Recommendations
1. {Highest priority fix}
2. {Next priority}
```

## Notes

- Reference specific line numbers for each finding
- If the component imports sub-components, note which ones may also need review
- Focus on SEO-impactful issues — don't nitpick non-SEO styling concerns
- Be pragmatic — a `"use client"` component that has one click handler is fine even if most of it displays data
