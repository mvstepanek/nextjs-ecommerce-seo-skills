---
name: seo-performance
description: Core Web Vitals and performance SEO rules for Next.js. Use when optimizing page load, working with third-party scripts, fonts, bundle size, or addressing LCP/CLS/INP issues.
paths: "**/layout*.tsx, **/page*.tsx, **/next.config.*, **/loading*.tsx"
---

# Performance & Core Web Vitals SEO Guidelines

Core Web Vitals are a Google ranking factor. Follow these rules for optimal performance.

## Targets

| Metric | Target | Measures |
|--------|--------|----------|
| **LCP** | < 2.5s | Main content load speed |
| **CLS** | < 0.1 | Visual stability during load |
| **INP** | < 200ms | Interaction responsiveness |

## Server-Side Rendering by Default

- Render critical content server-side — App Router: use Server Components; Pages Router: use `getServerSideProps`/`getStaticProps`
- Only use client-side rendering (`"use client"` / `useEffect`) when truly needed for interactivity
- Server-rendered content: faster LCP, zero JS bundle cost for display-only content
- Data-display components (product info, specs, lists) should be Server Components

```typescript
// GOOD — Server Component (default)
export default async function Page({ params }: Props) {
  const data = await getData(params.id);
  return <h1>{data.title}</h1>;
}

// Client component ONLY for interactive parts
"use client";
export function InteractiveWidget() { /* state, effects, handlers */ }
```

## LCP Optimization

1. Preload hero images with `priority` prop on next/image
2. Fetch above-fold data server-side (never behind useEffect)
3. Use ISR for frequently accessed pages: `export const revalidate = 300;`

## CLS Prevention

1. Always size images (width/height or fill with container)
2. Use `next/font` with `display: 'swap'` — prevents font-related layout shift
3. Reserve space for dynamic content loading

```typescript
import { Inter } from 'next/font/google';
const inter = Inter({ subsets: ['latin'], display: 'swap', weight: ['400', '700'] });
```

## Third-Party Scripts

```typescript
import Script from 'next/script';

// Analytics, tag managers — after page is interactive
<Script id="analytics" strategy="afterInteractive" src="..." />

// Non-critical (chat, surveys) — lazy load
<Script id="chat" strategy="lazyOnload" src="..." />

// NEVER use beforeInteractive for analytics — blocks rendering
```

## Bundle Size

1. Dynamic imports for below-fold components
2. Import specific functions, not entire libraries
3. Use `@next/bundle-analyzer` to monitor

```typescript
import dynamic from 'next/dynamic';
const HeavyComponent = dynamic(() => import('./HeavyComponent'));
```

## Streaming with Suspense

```typescript
import { Suspense } from 'react';

export default function Page() {
  return (
    <>
      <FastContent />
      <Suspense fallback={<Skeleton />}>
        <SlowContent />
      </Suspense>
    </>
  );
}
```

## Common Mistakes

1. Client-side rendering of data-display components — keep them server-rendered
2. `beforeInteractive` for analytics — blocks page render
3. Loading fonts via `<link>` — use next/font
4. Fetching data in useEffect for above-fold content — fetch on server
5. Not using Suspense — entire page waits for slowest query
