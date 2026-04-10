---
applyTo: "**/app/api/**/*.ts, **/app/api/**/*.tsx, **/pages/api/**/*.ts, **/pages/api/**/*.tsx"
---

# API Route SEO Requirements

When building API routes:

1. **Status codes**: Use correct HTTP status codes:
   - 200 for success
   - 301/308 for permanent redirects (SEO-relevant)
   - 302/307 for temporary redirects
   - 404 for not found (never redirect to homepage)
   - 410 for permanently removed resources

2. **Cache headers**: Set appropriate cache headers for SEO-relevant data:
   - Product data: `Cache-Control: public, s-maxage=300, stale-while-revalidate=600`
   - Category data: `Cache-Control: public, s-maxage=600, stale-while-revalidate=1200`
   - User-specific data: `Cache-Control: private, no-cache`

3. **Redirect responses**: If an API route performs redirects, use the correct status code (301 for permanent, 302 for temporary). Never use 302 for permanent URL changes.

4. **Sitemap/robots endpoints**: If generating sitemap.xml or robots.txt via API routes:
   - Sitemap: only include canonical, indexable URLs
   - robots.txt: always reference sitemap_index.xml
   - Set `Content-Type` correctly (`application/xml` for sitemaps, `text/plain` for robots.txt)
