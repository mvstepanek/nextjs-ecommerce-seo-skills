# Next.js E-Commerce SEO Skills for AI Coding Assistants

SEO-focused skills for **Claude Code** and **GitHub Copilot** that help developers maintain good SEO practices on Next.js e-commerce sites — without requiring SEO expertise.

Works with any Next.js e-commerce project. Skills provide preventive guidelines that developers follow while coding, covering metadata, structured data, images, performance, and more.

## Compatibility

- **Next.js 15.x and 16.x** — App Router and Pages Router
- Code examples use App Router conventions with a mapping table for Pages Router (see individual skills)
- These skills are **advisory only** — they inform the AI assistant about SEO best practices but do not trigger automatic code changes. The developer must explicitly request fixes.
- Code examples use **illustrative names** (URL patterns, config imports, function names) — adapt to your project's actual structure

## What's Included

### Claude Code Skills (10 auto-triggered)

| Skill | Trigger | Focus |
|-------|---------|-------|
| seo-metadata | Auto | Title, description, OG, canonical, Twitter cards |
| seo-structured-data | Auto | JSON-LD for Product, Breadcrumb, Organization, FAQ |
| seo-hreflang | Auto | Hreflang for multi-locale variants |
| seo-images | Auto | next/image, alt text, WebP, LCP optimization |
| seo-performance | Auto | Core Web Vitals, GTM, fonts, bundle size |
| seo-urls-routing | Auto | URL structure, slugs, locale prefixes |
| seo-crawlability | Auto | robots.txt, noindex, sitemaps |
| seo-ecommerce | Auto | Product pages, categories, pricing markup |
| seo-internal-linking | Auto | Breadcrumbs, anchor text, cross-linking |
| seo-redirects | Auto | 301/308, chains, next.config, 404 handling |

**Auto-triggered** skills activate automatically when Claude detects you're working on relevant files.

### Slash Commands (2 audit commands)

| Command | What it does |
|---------|-------------|
| `/seo-audit-page [file]` | Full page SEO audit with PASS/WARN/FAIL checklist |
| `/seo-audit-component [file]` | Component SEO review for images, links, headings, SSR |

### Agent Persona

| Agent | Role |
|-------|------|
| `seo-auditor` | Senior SEO engineer that reviews code across metadata, structured data, images, links, crawlability, and performance |

### GitHub Copilot Instructions

- `copilot-instructions.md` — repository-wide SEO rules
- Path-specific instructions for pages, components, and API routes

### Global Skills (site-agnostic)

4 framework-focused skills (metadata, structured data, images, performance) without any site specifics — usable on any Next.js project.

> **Note**: If you install the full project skills (Option A), you don't need global skills — the project-level skills are a superset. Global skills are for developers who want lightweight SEO guidance across all their projects without copying the full skill set.

## Installation

### Option A: Plugin install (recommended)

Add the marketplace and install the plugin:

```bash
# Add the marketplace
/plugin marketplace add mvstepanek/nextjs-ecommerce-seo-skills

# Install the plugin
/plugin install nextjs-ecommerce-seo-skills@nextjs-ecommerce-seo
```

### Option B: Manual project installation

Copy the skills, commands, agents, and Copilot instructions into your Next.js project:

```bash
# Clone this repo
git clone https://github.com/mvstepanek/nextjs-ecommerce-seo-skills.git /tmp/nextjs-seo-skills

# Copy Claude Code skills and commands into your project
cp -r /tmp/nextjs-seo-skills/skills/ /path/to/your-nextjs-project/.claude/skills/
cp -r /tmp/nextjs-seo-skills/commands/ /path/to/your-nextjs-project/.claude/commands/

# Copy agent persona
cp -r /tmp/nextjs-seo-skills/agents/ /path/to/your-nextjs-project/agents/

# Copy GitHub Copilot instructions
cp -r /tmp/nextjs-seo-skills/.github/ /path/to/your-nextjs-project/.github/

# Commit to version control so the whole team benefits
cd /path/to/your-nextjs-project
git add .claude/ .github/ agents/
git commit -m "Add SEO skills for AI coding assistants"
```

### Option C: Global skills only

```bash
# Copy global skills to your home directory
cp -r /tmp/nextjs-seo-skills/global-skills/* ~/.claude/skills/
```

These skills are now available in all your projects.

### Option D: Cherry-pick specific skills

Browse the [skill reference](docs/skill-reference.md) and copy individual skill directories.

## Verification

1. Open Claude Code in your project
2. Ask: *"What skills are available?"* — should list all SEO skills
3. Say: *"I'm adding a new product page"* — Claude should auto-load relevant skills
4. Run: `/seo-audit-page app/[locale]/products/[id]/page.tsx`
5. Run: `/seo-audit-component components/ProductCard.tsx`

## Documentation

- [Installation Guide](docs/installation.md)
- [Skill Reference](docs/skill-reference.md)
