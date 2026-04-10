# SEO Guidelines for Next.js E-Commerce

> **Advisory only**: These are suggestions. Do not auto-fix code based on these rules — only recommend changes when the developer asks. Compatible with Next.js 15.x/16.x, App Router and Pages Router.

This is a Next.js e-commerce site with multi-locale support. It serves multiple locale variants using `/{lang}-{COUNTRY}/` URL patterns (e.g. `/en-GB/`, `/de-DE/`, `/fr-CH/`).

## Metadata — Every Page Needs This

- Use the Next.js Metadata API (`generateMetadata` / `metadata` export in App Router, `next/head` in Pages Router) — never hardcode in JSX
- **Title**: Keep concise (truncated ~50-60 chars on desktop), format `{Content} | {Brand}`, include model number on product pages
- **Description**: Keep concise and unique per page, include CTA for e-commerce ("Buy online", "Order now")
- **Canonical URL**: Required on every page, absolute URL with locale prefix, self-referencing
- **Open Graph**: og:title, og:description, og:image (min 1200x630), og:url (matches canonical), og:type, og:locale
- **Twitter**: twitter:card (summary_large_image for products), twitter:title, twitter:description

## Structured Data (JSON-LD)

- Always use `<script type="application/ld+json">` — never Microdata
- Render server-side for immediate crawler access
- Use `@graph` array to combine multiple schemas on one page

**Product pages MUST include** (required for rich results):
- `name`, `image` (array of URLs)
- `offers.price` (numeric value, no currency symbols — both `39.99` and `"39.99"` are valid), `offers.priceCurrency` (locale-dependent)
- `offers.availability` (https://schema.org/InStock or OutOfStock)

**Strongly recommended**: `sku`, `brand` (from site config), `description`. Provide `gtin` if available; otherwise `brand` + `mpn` for product identification.

**BreadcrumbList** on every non-homepage page (if breadcrumbs are used) — must match visible breadcrumbs.

## Hreflang (Multi-Locale)

- Every page needs `<link rel="alternate" hreflang="xx-YY">` for ALL locale variants + `x-default`
- Self-referencing required — page must include its own locale in hreflang set
- Implement hreflang via Metadata API (App Router) or `next/head` (Pages Router)
- Language switcher must link to the same page in other locales, not just the homepage

## Images

- **Always use `<Image>` from `next/image`** — never raw `<img>`
- **Alt text**: Descriptive, include product name on product images
- Never use generic alt: "image", "photo", "banner", "product image"
- Empty `alt=""` only for purely decorative images
- Always specify `width`/`height` or use `fill` — prevents CLS
- Use `priority` on the main above-fold image (LCP element) — 1-2 per page max

## URLs & Routing

- Every URL must have locale prefix: `/{lang}-{COUNTRY}/`
- Slugs: lowercase, hyphen-separated, no special characters
- Never hardcode locale — derive from route params
- Search pages (`/*/search/`) are blocked by robots.txt — always add `noindex` too
- Page 1 canonical: no `?page=1`, just the clean URL

## Links

- **Always use `<Link>` from `next/link`** for internal navigation — never raw `<a>`
- Descriptive anchor text — never "click here" or "read more"
- No `rel="nofollow"` on internal links
- External links with `target="_blank"`: modern browsers auto-add `rel="noopener"`, but adding it explicitly is still harmless and ensures compatibility with older browsers

## Performance (Core Web Vitals = Ranking Factor)

- **Server-side rendering by default** — only client-side JS for interactivity
- Critical content (product name, price, description) must be server-rendered
- Analytics/tag managers: `strategy="afterInteractive"` — never `beforeInteractive`
- Use `next/font` with `display: 'swap'` — never load fonts via `<link>`
- Dynamic imports for below-fold components

## Redirects

- 301 for permanent URL changes — never 302 for permanent moves
- 302 for locale detection redirects (temporary)
- No redirect chains (A→B→C) — always redirect to final URL
- Custom 404 page with navigation — never redirect 404s to homepage

## DO NOT

- Use raw `<img>` tags — use next/image
- Use raw `<a>` for internal links — use next/link
- Hardcode locale strings (`/en-GB/`) — use params
- Add `nofollow` to internal links
- Put critical content behind `useEffect` — server-render it
- Use `beforeInteractive` for analytics scripts
- Create redirect chains
- Set price to 0 when hidden — omit the field
- Add FAQ schema on e-commerce sites — since 2023 Google restricts FAQ rich results to government/health sites, making FAQ schema essentially worthless for e-commerce
- Use generic alt text on product images
