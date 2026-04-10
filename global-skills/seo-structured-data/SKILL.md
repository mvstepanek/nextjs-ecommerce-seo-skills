---
name: seo-structured-data
description: Schema.org structured data rules for JSON-LD markup in Next.js. Use when adding or modifying structured data, product schemas, breadcrumbs, or FAQ markup.
paths: "**/schema*.ts, **/structured*.ts, **/jsonld*.tsx, **/page*.tsx"
---

# Structured Data (JSON-LD) Guidelines

Follow these rules when implementing schema.org structured data.

## General Rules

- **Always use JSON-LD** — Google's preferred format (not Microdata or RDFa)
- **Render server-side** — ensure JSON-LD is in the initial HTML (Server Components in App Router, or rendered in the page component with SSR in Pages Router)
- **Validate** — test with Google Rich Results Test before deploying
- **Prefer one script tag per page** — use `@graph` to combine multiple schemas. Multiple tags are valid but harder to maintain.
- **Data must match visible content** — Google penalizes mismatches

## Implementation Pattern

```typescript
export function JsonLd({ data }: { data: Record<string, unknown> }) {
  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  );
}
```

## Common Schema Types

### Product (e-commerce pages)

```typescript
{
  "@type": "Product",
  name: product.name,
  description: product.description,
  sku: product.sku,
  brand: { "@type": "Brand", name: siteConfig.brandName },
  image: product.images,
  offers: {
    "@type": "Offer",
    price: product.price,
    priceCurrency: getCurrencyForLocale(locale),
    availability: "https://schema.org/InStock", // or OutOfStock, PreOrder
    seller: { "@type": "Organization", name: siteConfig.brandName },
  }
}
```

Required for rich results: `name`, `image`, `offers.price`, `offers.priceCurrency`, `offers.availability`.

### BreadcrumbList

```typescript
{
  "@type": "BreadcrumbList",
  itemListElement: [
    { "@type": "ListItem", position: 1, name: "Home", item: `${siteConfig.url}/` },
    { "@type": "ListItem", position: 2, name: "Category", item: `${siteConfig.url}/category` },
    { "@type": "ListItem", position: 3, name: "Current Page" }, // No item URL for current page
  ]
}
```

### FAQPage

**Note**: Since August 2023, Google has progressively restricted FAQ rich results to a small number of well-known, authoritative government and health websites. For e-commerce sites, FAQ schema provides essentially **zero value from Google**. Other search engines (Bing) may still use it, but the ROI is minimal. **Skip FAQ schema on e-commerce sites** unless you have a specific non-Google reason.

```typescript
{
  "@type": "FAQPage",
  mainEntity: [
    { "@type": "Question", name: "Q text", acceptedAnswer: { "@type": "Answer", text: "A text" } },
  ]
}
```

Only add FAQ schema on pages with visible Q&A content. Min 2 questions. Implementation is optional given the restricted eligibility above.

### WebSite (with Search)

```typescript
{
  "@type": "WebSite",
  name: siteConfig.brandName,
  url: siteConfig.url,
  potentialAction: {
    "@type": "SearchAction",
    target: { "@type": "EntryPoint", urlTemplate: `${siteConfig.url}/search?q={query}` },
    "query-input": "required name=query"
  }
}
```

## Combining Schemas

Use `@graph` when a page has multiple schema types:

```typescript
<JsonLd data={{
  "@context": "https://schema.org",
  "@graph": [productSchema, breadcrumbSchema]
}} />
```

## Common Mistakes

1. **Missing price/availability on Product** — prevents rich results
2. **FAQ schema without visible FAQ** — Google considers this spam
3. **Breadcrumbs don't match visible UI** — must be identical
4. **Multiple script tags** — prefer `@graph` to keep structured data organized (multiple tags are valid but harder to maintain)
5. **Relative URLs in schema** — always use absolute URLs
