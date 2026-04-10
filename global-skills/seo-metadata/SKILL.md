---
name: seo-metadata
description: SEO metadata rules for Next.js pages. Use when creating or modifying page metadata, title tags, meta descriptions, Open Graph tags, canonical URLs, or Twitter cards.
paths: "**/page*.tsx, **/page*.ts, **/layout*.tsx, **/layout*.ts, **/metadata*.ts"
---

# SEO Metadata Guidelines (Next.js)

> Compatible with Next.js 15.x/16.x, App Router and Pages Router. Code examples use App Router conventions — for Pages Router, use `next/head` with `getStaticProps`/`getServerSideProps`.

Follow these rules when creating or modifying page metadata.

## Title Tags

- **Keep concise** — Google truncates to fit device width, typically ~50-60 characters on desktop
- **Format**: `{Page Content} | {Brand Name}` — put the most important words first
- **Must be unique** per page — no two pages should share the same title
- **Dynamic pages**: use `generateMetadata` (App Router) or `next/head` with SSR/SSG data (Pages Router) to create titles from data

## Meta Description

- **Keep concise** — Google may truncate long snippets. No official limit, but focus on making them unique and relevant.
- **Include a call-to-action** where relevant ("Buy online", "Learn more", "Get started")
- **Must be unique** per page
- **Summarize the page value** — what will the user find on this page?

## Canonical URLs

- **Every indexable page MUST have a canonical URL**
- **Must be absolute** — include full protocol + domain
- **Self-referencing** — a page's canonical should point to itself
- **Pagination**: page 1 canonical has no `?page=1`; subsequent pages should have a self-referencing canonical
- **Filter params**: set the canonical to the base URL without filters

## Open Graph Tags

Required on every page:

| Tag | Rule |
|-----|------|
| `og:title` | Same as or adapted from title tag |
| `og:description` | Same as meta description |
| `og:url` | Must match canonical URL exactly |
| `og:type` | `website` (or `product`, `article` as appropriate) |
| `og:image` | Representative image, min 1200x630px |
| `og:site_name` | Your site/brand name |

## Twitter Card Tags

| Tag | Rule |
|-----|------|
| `twitter:card` | `summary_large_image` (for pages with images) or `summary` |
| `twitter:title` | Same as og:title |
| `twitter:description` | Same as og:description |

## Next.js Implementation

### Dynamic pages (App Router: `generateMetadata`, Pages Router: `next/head` + SSR):

```typescript
export async function generateMetadata({ params }: Props): Promise<Metadata> {
  const data = await getData(params.id);
  return {
    title: `${data.name} | Brand`,
    description: data.summary,
    alternates: { canonical: `${siteConfig.url}/page/${data.slug}` },
    openGraph: {
      title: `${data.name} | Brand`,
      description: data.summary,
      url: `${siteConfig.url}/page/${data.slug}`,
      type: 'website',
      images: [{ url: data.imageUrl, width: 1200, height: 630 }],
    },
  };
}
```

### Static pages — use `metadata` export:

```typescript
export const metadata: Metadata = {
  title: 'About Us | Brand',
  description: 'Learn about our company and mission.',
};
```

### Rules
- **Never hardcode metadata in JSX** — always use the Metadata API
- **Layout metadata cascades** — set defaults in root layout, override in pages
- **Never duplicate** — if layout sets og:site_name, pages don't need to repeat it

## Common Mistakes

1. **Same title on every page** — each page needs a unique title
2. **Missing description** — every indexable page needs one
3. **No canonical URL** — causes duplicate content issues
4. **Missing OG image** — results in ugly social media previews
5. **Title too long** — check character count
