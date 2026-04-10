# Skill Reference

Quick reference for all available SEO skills.

## Project-Level Skills

Located in `skills/`. When installed via plugin, these are available automatically. For manual install, copy to your project's `.claude/skills/`.

### Auto-Triggered Skills

These activate automatically when you work on matching files.

| Skill | Command | Triggers on | What it covers |
|-------|---------|-------------|----------------|
| **seo-metadata** | `/seo-metadata` | Page/layout files | Title tags, meta descriptions, OG tags, canonical URLs, Twitter cards |
| **seo-structured-data** | `/seo-structured-data` | Page/schema files | JSON-LD for Product, BreadcrumbList, Organization, FAQ, WebSite |
| **seo-hreflang** | `/seo-hreflang` | i18n/locale/middleware files | Hreflang tags for multi-locale sites, x-default, language switcher |
| **seo-images** | `/seo-images` | TSX/JSX files | next/image, alt text, sizing, WebP/AVIF, LCP priority |
| **seo-performance** | `/seo-performance` | Page/layout/config files | Core Web Vitals (LCP/CLS/INP), GTM, fonts, bundle size |
| **seo-urls-routing** | `/seo-urls-routing` | Page/middleware/config files | URL patterns, locale prefixes, slugs, pagination |
| **seo-crawlability** | `/seo-crawlability` | robots/sitemap/middleware files | robots.txt, noindex, sitemaps, SSR |
| **seo-ecommerce** | `/seo-ecommerce` | Product/category/cart files | Product pages, category SEO, faceted nav, pricing markup |
| **seo-internal-linking** | `/seo-internal-linking` | Nav/breadcrumb/footer files | Breadcrumbs, anchor text, cross-linking, language switcher |
| **seo-redirects** | `/seo-redirects` | Config/middleware/redirect files | 301/308, chains, 404 handling, locale redirects |

## Slash Commands

Invoke these directly when you need an audit. Located in `commands/`.

| Command | What it does |
|---------|-------------|
| `/seo-audit-page [file]` | Full SEO audit of a page file — PASS/WARN/FAIL checklist |
| `/seo-audit-component [file]` | SEO review of a component — images, links, headings, SSR |

## Agent Persona

Copy from `agents/` to your project root.

| Agent | Role |
|-------|------|
| **seo-auditor** | Senior SEO engineer that reviews code across metadata, structured data, images, links, crawlability, and performance |

## Supporting Files

| Skill | File | Content |
|-------|------|---------|
| seo-structured-data | `schemas/product.json` | Product schema JSON-LD template |
| seo-structured-data | `schemas/breadcrumb.json` | BreadcrumbList schema template |
| seo-structured-data | `schemas/organization.json` | Organization schema template |
| seo-structured-data | `schemas/faq.json` | FAQPage schema template |
| seo-hreflang | `locale-matrix.md` | Complete locale/country/currency mapping |
| seo-crawlability | `reference.md` | Current robots.txt and sitemap structure |
| seo-ecommerce | `reference.md` | E-commerce SEO patterns and priorities |
| seo-audit-page (command) | `checklist.md` | Detailed audit checklist criteria |

## Global Skills

Copy from `global-skills/` to `~/.claude/skills/`. These are site-agnostic and work on any Next.js project.

| Skill | What it covers |
|-------|---------------|
| **seo-metadata** | Generic metadata rules (title, description, canonical, OG) |
| **seo-structured-data** | Generic schema.org JSON-LD guidance |
| **seo-images** | Generic image optimization (next/image, alt text, sizing) |
| **seo-performance** | Generic Core Web Vitals rules |

## GitHub Copilot Instructions

Copy from `.github/` to your project's `.github/`.

| File | Applies to | Content |
|------|-----------|---------|
| `copilot-instructions.md` | All files | Condensed SEO rules for the full project |
| `instructions/pages.instructions.md` | `page files` | Page-specific: metadata, structured data, SSR |
| `instructions/components.instructions.md` | `**/components/**/*.tsx` | Component-specific: images, links, headings |
| `instructions/api.instructions.md` | `API route files` | API-specific: status codes, cache, redirects |
