# SEO Page Audit

Perform a comprehensive SEO audit on the page file specified in `$ARGUMENTS`.

## Instructions

1. **Read the target file** at `$ARGUMENTS`
2. **Identify the page type** (product page, category page, static page, layout, etc.)
3. **Check each item** in the checklist below
4. **Read related files** if needed (layout files for shared metadata, components for image/link usage)
5. **Output the audit report** in the format shown below

## Audit Checklist

### Metadata Checks
- [ ] Has metadata implementation (App Router: `generateMetadata` / `metadata` export; Pages Router: `next/head`)
- [ ] Title is present and concise (Google truncates around ~50-60 chars on desktop)
- [ ] Title includes brand name (from site config)
- [ ] Title is not hardcoded (uses dynamic data for dynamic pages)
- [ ] Meta description is present and concise
- [ ] Canonical URL is set and absolute
- [ ] Canonical URL includes locale prefix
- [ ] Open Graph tags are present (title, description, image, url, type)
- [ ] Twitter card tags are present
- [ ] Locale is not hardcoded — derived from route params

### Structured Data Checks
- [ ] JSON-LD structured data is present (for pages that need it)
- [ ] Uses `@graph` pattern if multiple schemas on one page
- [ ] Product pages: has Product schema with price, availability, SKU, brand
- [ ] Product pages: price uses correct currency for locale
- [ ] BreadcrumbList schema present and matches visible breadcrumbs
- [ ] All URLs in structured data are absolute and include locale prefix

### Image Checks
- [ ] All images use `next/image` (no raw `<img>` tags)
- [ ] All meaningful images have descriptive alt text
- [ ] Alt text includes product name on product pages
- [ ] No generic alt text ("image", "photo", "banner")
- [ ] LCP image has `priority` prop
- [ ] All images have explicit width/height or use `fill`

### Link Checks
- [ ] Internal links use `next/link` (no raw `<a>` for internal URLs)
- [ ] No "click here" or "read more" as anchor text
- [ ] No hardcoded locale in link hrefs — uses dynamic locale param
- [ ] External links with `target="_blank"` — `rel="noopener"` is auto-added by modern browsers but explicit is fine for compatibility

### Crawlability Checks
- [ ] Page should be indexable (or has correct noindex if it shouldn't be)
- [ ] No critical content behind client-side fetch (`useEffect` + `useState`)
- [ ] Page renders critical content server-side (Server Component in App Router, or SSR/SSG in Pages Router)
- [ ] Hreflang handled (in this page or parent layout)

### E-Commerce Checks (product/category pages only)
- [ ] Product page has Product schema with price and availability
- [ ] Category page has introductory text content
- [ ] Faceted navigation/filters use canonical or noindex correctly
- [ ] Breadcrumb navigation visible on page

## Report Format

Output the audit as:

```
## SEO Audit: {filename}
Page type: {product|category|static|layout|etc.}

### Metadata
- PASS: Title present — "{actual title}" (N chars)
- FAIL: Meta description missing
- WARN: Title is 65 chars — may be truncated on some devices
...

### Structured Data
- PASS: Product schema present with price and availability
- FAIL: Missing BreadcrumbList schema
...

### Images
- PASS: All images use next/image
- WARN: Image at line N has generic alt text "product image"
...

### Links
- PASS: All internal links use next/link
...

### Crawlability
- PASS: Server Component — content rendered server-side
...

### Summary
- PASS: N items
- WARN: N items
- FAIL: N items

### Recommendations
1. {Most critical fix first}
2. {Next priority}
...
```

## Notes

- If the file is a layout, focus on metadata cascading and shared elements
- If the file imports components, check those components too for image/link issues
- Reference specific line numbers when reporting issues
- Prioritize FAIL items by SEO impact (metadata > structured data > images > links)
