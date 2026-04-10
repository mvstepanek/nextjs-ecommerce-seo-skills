# Next.js E-commerce SEO Skills Repository

This repository provides SEO-focused skills for AI coding assistants (Claude Code and GitHub Copilot), targeting Next.js e-commerce sites.

## Advisory Only

These skills are **suggestions and guidelines only**. The AI assistant should:
- **Not auto-fix code** based on these rules — only flag potential issues
- **Not make unsolicited changes** — wait for the developer to explicitly request SEO improvements
- **Present recommendations** when asked, not impose them

Skills inform the assistant about SEO best practices so it can give good advice when asked. They are not a license to modify code unprompted.

## Compatibility

- **Next.js**: 15.x and 16.x
- **Routers**: App Router and Pages Router

Code examples primarily use App Router conventions. For Pages Router projects, adapt accordingly:

| App Router | Pages Router |
|-----------|-------------|
| `generateMetadata()` / `metadata` export | `<Head>` from `next/head` + `getStaticProps` / `getServerSideProps` |
| `app/[locale]/page.tsx` | `pages/[locale]/index.tsx` |
| Server Components (default) | `getServerSideProps` / `getStaticProps` for server-side data |
| `generateStaticParams` | `getStaticPaths` |
| `app/robots.ts` / `app/sitemap.ts` | `public/robots.txt` + API route or build-time generation |
| `app/[locale]/not-found.tsx` | `pages/404.tsx` |
| `loading.tsx` (Suspense boundary) | Manual `<Suspense>` or loading states |

API details (e.g. async `params` in Next.js 15+) may vary between versions — consult the Next.js documentation for your version.

## Project Structure

- `.claude-plugin/` - Plugin and marketplace metadata (`plugin.json`, `marketplace.json`)
- `skills/` - Auto-triggered SEO skills (10 skills)
- `commands/` - Slash commands for SEO audits (`/seo-audit-page`, `/seo-audit-component`)
- `agents/` - Agent personas (SEO auditor)
- `global-skills/` - Global skills (copy to `~/.claude/skills/`)
- `.github/` - GitHub Copilot instructions
- `docs/` - Documentation and installation guide

## Conventions

- Skills use YAML frontmatter with the fields: name, description, paths, disable-model-invocation, allowed-tools
- Skill content is advisory only: checklists, guidelines, warnings — no auto-fix code
- Keep each SKILL.md under 500 lines; use supporting files for detailed reference
- All SEO rules must cite the reasoning (why it matters, what happens if you skip it)
- Global skills are framework-specific but site-agnostic
- Use generic e-commerce examples where relevant (URL patterns, locale codes, schema patterns)

## Code Examples

Code examples throughout the skills use **illustrative names and patterns** — they are not prescriptive. Adapt them to your project's actual structure:

- **URL patterns** (`/products/{id}/{slug}`, `/categories/{slug}`) — examples only. Your project may use different paths.
- **Config imports** (`@/config/site`, `SITE_URL`, `BRAND_NAME`) — represent the concept of centralizing site config. Use whatever config pattern your project already has.
- **Function names** (`getProduct()`, `getCurrencyForLocale()`) — placeholders for your actual data-fetching and utility functions.
- **Component names** (`JsonLd.tsx`, `Breadcrumbs.tsx`) — example implementations. Name and structure components however fits your project.

The SEO principles matter, not the specific names or paths used in examples.
