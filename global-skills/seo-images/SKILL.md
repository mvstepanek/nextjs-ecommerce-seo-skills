---
name: seo-images
description: Image SEO and optimization rules for Next.js. Use when adding images, product photos, or working with next/image. Covers alt text, sizing, formats, lazy loading, and LCP optimization.
paths: "**/*.tsx, **/*.jsx"
---

# Image SEO & Optimization Guidelines

Follow these rules when adding or modifying images in a Next.js project.

## Always Use next/image

**Never use raw `<img>` tags** — always use `<Image>` from `next/image`.

Benefits: automatic WebP/AVIF conversion, lazy loading, responsive sizing, blur placeholders.

```typescript
import Image from 'next/image';

// GOOD
<Image src="/photo.jpg" alt="Descriptive alt text" width={800} height={600} />

// BAD
<img src="/photo.jpg" alt="photo" />
```

## Alt Text Rules

| Image Type | Alt Text | Example |
|-----------|----------|---------|
| Product | `{Name} - {Key Detail}` | "Widget Pro - 500W motor" |
| Category hero | Describe the content | "Collection of industrial widgets" |
| Decorative only | Empty string | `alt=""` |
| Logo | `{Company} logo` | "Acme Corp logo" |
| Icon with meaning | Describe the meaning | "Warning: out of stock" |

### Rules
- Every meaningful image MUST have descriptive alt text
- Never use generic text: "image", "photo", "banner", "placeholder"
- Empty `alt=""` ONLY for purely decorative images
- Include relevant keywords naturally (product name, category)

## Sizing

- **Always specify `width` and `height`** — or use `fill` with a sized container
- Missing dimensions cause CLS (Cumulative Layout Shift) — hurts Core Web Vitals

```typescript
// Explicit dimensions
<Image src={url} alt={alt} width={800} height={600} />

// Fill mode
<div className="relative aspect-[4/3] w-full">
  <Image src={url} alt={alt} fill className="object-cover" />
</div>
```

## Priority (LCP)

- Use `priority` on the main above-the-fold image (1-2 per page max)
- This is the LCP (Largest Contentful Paint) element — preloading it improves the core metric

```typescript
<Image src={heroImage} alt={alt} width={1200} height={600} priority />
```

## Image Formats

```javascript
// next.config.js
module.exports = {
  images: {
    formats: ['image/avif', 'image/webp'],
  },
};
```

## Blur Placeholder

Reduces perceived loading time and CLS:

```typescript
<Image src={url} alt={alt} width={800} height={600} placeholder="blur" blurDataURL={blurHash} />
```

## Common Mistakes

1. Raw `<img>` tags — always use next/image
2. Generic alt text — describe what's in the image
3. Missing dimensions — causes layout shift
4. `priority` on every image — only 1-2 per page
5. Empty alt on meaningful images — only decorative images get `alt=""`
