---
applyTo: "**/app/**/page.tsx, **/app/**/page.ts, **/pages/**/*.tsx, **/pages/**/*.ts"
---

# Page File SEO Requirements

Every page file must have:

1. **Metadata** — App Router: `generateMetadata` / `metadata` export; Pages Router: `next/head`:
   - Title: keep concise, format `{Content} | {Brand}`
   - Description: concise, unique, with CTA where relevant
   - Canonical URL: absolute, with locale prefix
   - Open Graph: title, description, image, url, type
   - Hreflang: `alternates.languages` with all locale variants + x-default

2. **Structured data (JSON-LD)** where applicable:
   - Product pages: Product schema — required for rich results: `name`, `image`, `offers.price`, `offers.priceCurrency`, `offers.availability`; strongly recommended: `sku`, `brand`, `description`
   - Category pages: CollectionPage or ItemList schema
   - FAQ pages: Skip FAQ schema on e-commerce sites — Google restricts FAQ rich results to government/health sites, making it essentially worthless for e-commerce
   - All non-homepage pages: BreadcrumbList schema

3. **Server-side rendering** — critical content (product name, price, description) must be in the initial HTML. App Router: use Server Components; Pages Router: use `getServerSideProps`/`getStaticProps`.

4. **Noindex** (via `noindex` meta tag, not robots.txt) on non-SEO pages: search results, cart, checkout, account. For filtered views: noindex granular multi-filter combinations, but keep useful single-filter pages indexable if they match real search intent.

5. **No hardcoded locale** — derive from `params.locale`.
