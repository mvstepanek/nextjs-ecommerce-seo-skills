# Full SEO Audit Checklist

Detailed descriptions for each audit item. Use this as reference when performing `/seo-audit-page`.

## Metadata

### Title Tag
- **What to check**: Look for `title` in `metadata` export or `generateMetadata` return value
- **PASS criteria**: Present, concise, includes brand name suffix from config, uses dynamic data for dynamic pages
- **WARN criteria**: Excessively long (may be truncated in search results), or missing brand name
- **FAIL criteria**: Missing entirely, or duplicated across pages

### Meta Description
- **What to check**: Look for `description` in metadata
- **PASS criteria**: Present, concise, unique per page
- **WARN criteria**: Present but very long (may be truncated)
- **FAIL criteria**: Missing entirely

### Canonical URL
- **What to check**: Look for `alternates.canonical` in metadata
- **PASS criteria**: Absolute URL with locale prefix, self-referencing
- **WARN criteria**: Relative URL (missing domain)
- **FAIL criteria**: Missing entirely, or hardcoded locale

### Open Graph Tags
- **What to check**: Look for `openGraph` in metadata
- **PASS criteria**: Has title, description, image, url, type, siteName, locale
- **WARN criteria**: Partially complete (e.g., missing image)
- **FAIL criteria**: Missing entirely

### Twitter Cards
- **What to check**: Look for `twitter` in metadata
- **PASS criteria**: Has card type, title, description, image
- **WARN criteria**: Partially complete
- **FAIL criteria**: Missing entirely

## Structured Data

### JSON-LD Presence
- **What to check**: Look for `<script type="application/ld+json">` or a JsonLd component
- **PASS criteria**: Present and valid JSON
- **FAIL criteria**: Missing on product/category pages, or malformed JSON

### Product Schema
- **What to check**: On product pages, verify Product schema has required fields for rich result eligibility
- **PASS criteria**: Has `name`, `image[]`, offers with `price` + `priceCurrency` + `availability`; also has recommended fields (`sku`, `brand`, `description`)
- **WARN criteria**: Present with required fields but missing recommended fields (`sku`, `brand`, `mpn`, `gtin`, reviews, additionalProperty)
- **FAIL criteria**: Missing entirely, or missing required fields (`name`, `image`, `offers.price`, `offers.priceCurrency`, `offers.availability`)

### BreadcrumbList Schema
- **What to check**: Look for BreadcrumbList in structured data
- **PASS criteria**: Present, positions sequential, URLs absolute, matches visible breadcrumbs
- **FAIL criteria**: Missing on non-homepage pages

### Currency Check
- **What to check**: If Product schema has offers.priceCurrency
- **PASS criteria**: Currency matches locale (GBP for en-GB, EUR for de-DE, etc.)
- **FAIL criteria**: Wrong currency for locale, or currency hardcoded instead of derived

## Images

### next/image Usage
- **What to check**: Look for `<img` tags (raw) vs `<Image` (next/image)
- **PASS criteria**: All images use next/image
- **FAIL criteria**: Any raw `<img>` tags found

### Alt Text Quality
- **What to check**: Every `<Image` component's `alt` prop
- **PASS criteria**: Descriptive, includes product name on product images
- **WARN criteria**: Alt text is present but generic ("product image", "banner")
- **FAIL criteria**: `alt` prop missing or empty string on meaningful images

### Dimensions
- **What to check**: width/height props or fill mode
- **PASS criteria**: All images have explicit dimensions or use fill with sized container
- **WARN criteria**: Using fill without obvious sized parent container
- **FAIL criteria**: Missing width/height and not using fill

### LCP Priority
- **What to check**: First/main image has `priority` prop
- **PASS criteria**: Main above-fold image has priority
- **WARN criteria**: No image has priority (may be fine if page has no hero image)
- **FAIL criteria**: Priority on below-fold or thumbnail images (incorrect usage)

## Links

### next/link Usage
- **What to check**: Internal links using `<Link>` vs `<a>`
- **PASS criteria**: All internal links use next/link
- **FAIL criteria**: Raw `<a>` tags for internal navigation

### Anchor Text Quality
- **What to check**: The visible text of link elements
- **PASS criteria**: Descriptive text related to the target page
- **WARN criteria**: Generic text like "click here", "read more", "learn more"

### Locale Handling
- **What to check**: Link href values for hardcoded locale strings
- **PASS criteria**: Locale derived from params or context
- **FAIL criteria**: Hardcoded `/en-GB/` in link paths

## Crawlability

### Indexability
- **What to check**: Does the page type warrant indexing? Is robots set correctly?
- **PASS criteria**: Indexable pages have no noindex; non-indexable pages (search, cart) have noindex
- **FAIL criteria**: Product/category page has noindex, or search/cart page is indexable

### Server-Side Rendering
- **What to check**: "use client" directive, useEffect for data fetching
- **PASS criteria**: Critical content rendered server-side (no useEffect for product data)
- **WARN criteria**: Minor dynamic content client-side (e.g., stock count)
- **FAIL criteria**: Product name/description/price behind client-side fetch

### Hreflang
- **What to check**: alternates.languages in metadata or parent layout
- **PASS criteria**: Present with all locale variants + x-default
- **WARN criteria**: Present but potentially missing some locales
- **FAIL criteria**: Missing entirely on an indexable page
