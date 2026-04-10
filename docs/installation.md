# Installation Guide

## Prerequisites

- A Next.js project (15.x or 16.x — App Router or Pages Router)
- Claude Code installed ([claude.com/claude-code](https://claude.com/claude-code))
- Optionally: GitHub Copilot extension in VS Code

## Option A: Plugin Install (Recommended)

The fastest way to install — uses the Claude Code plugin system.

### Step 1: Add the marketplace

```
/plugin marketplace add mvstepanek/nextjs-ecommerce-seo-skills
```

### Step 2: Install the plugin

```
/plugin install nextjs-ecommerce-seo-skills@nextjs-ecommerce-seo
```

### Step 3: Verify

```
> What skills are available?
```

You should see all SEO skills listed. Try the slash commands:

```
> /seo-audit-page app/[locale]/products/[id]/page.tsx
> /seo-audit-component components/ProductCard.tsx
```

### Updating

```
/plugin marketplace update
```

## Option B: Manual Project Installation

Copy skills, commands, agents, and Copilot instructions into your Next.js project. This gives the whole team access via version control.

### Step 1: Clone the skills repo

```bash
git clone https://github.com/mvstepanek/nextjs-ecommerce-seo-skills.git /tmp/nextjs-seo-skills
```

### Step 2: Copy Claude Code skills and commands

```bash
# Create directories if they don't exist
mkdir -p /path/to/your-nextjs-project/.claude/skills
mkdir -p /path/to/your-nextjs-project/.claude/commands

# Copy all SEO skills
cp -r /tmp/nextjs-seo-skills/skills/* /path/to/your-nextjs-project/.claude/skills/

# Copy slash commands (audit tools)
cp -r /tmp/nextjs-seo-skills/commands/* /path/to/your-nextjs-project/.claude/commands/

# Copy agent persona
cp -r /tmp/nextjs-seo-skills/agents/ /path/to/your-nextjs-project/agents/
```

### Step 3: Copy GitHub Copilot instructions

```bash
# Create .github directory if needed
mkdir -p /path/to/your-nextjs-project/.github/instructions

# Copy Copilot instructions
cp /tmp/nextjs-seo-skills/.github/copilot-instructions.md /path/to/your-nextjs-project/.github/
cp /tmp/nextjs-seo-skills/.github/instructions/* /path/to/your-nextjs-project/.github/instructions/
```

### Step 4: Commit to version control

```bash
cd /path/to/your-nextjs-project
git add .claude/ .github/ agents/
git commit -m "Add SEO skills for AI coding assistants (Claude Code + Copilot)"
```

### Step 5: Verify

Open Claude Code in your project and test:

```
> What skills are available?
```

### Updating (manual)

```bash
cd /tmp/nextjs-seo-skills
git pull

# Re-copy to your project
cp -r skills/* /path/to/your-project/.claude/skills/
cp -r commands/* /path/to/your-project/.claude/commands/
cp -r agents/ /path/to/your-project/agents/
cp .github/copilot-instructions.md /path/to/your-project/.github/
cp .github/instructions/* /path/to/your-project/.github/instructions/
```

## Option C: Global Skills Only

Install site-agnostic SEO skills that work across all your Next.js projects.

```bash
git clone https://github.com/mvstepanek/nextjs-ecommerce-seo-skills.git /tmp/nextjs-seo-skills

# Copy global skills to your home directory
cp -r /tmp/nextjs-seo-skills/global-skills/* ~/.claude/skills/
```

These 4 skills (seo-metadata, seo-structured-data, seo-images, seo-performance) are now available in every project you open with Claude Code.

## Option D: Cherry-Pick Specific Skills

Browse the [skill reference](skill-reference.md) and copy only the skills you need:

```bash
# Example: just metadata and images skills
cp -r /tmp/nextjs-seo-skills/skills/seo-metadata /path/to/project/.claude/skills/
cp -r /tmp/nextjs-seo-skills/skills/seo-images /path/to/project/.claude/skills/
```

## How Skills Work

### Auto-triggered skills (10 skills)

These skills activate automatically when Claude detects you're working on relevant files:

- Working on a `page.tsx`? Claude loads **seo-metadata**, **seo-performance**
- Adding an image component? Claude loads **seo-images**
- Editing `middleware.ts`? Claude loads **seo-hreflang**, **seo-urls-routing**

You don't need to invoke them — Claude applies the guidelines as context.

### Slash commands (2 audit commands)

These run only when you invoke them:

- `/seo-audit-page path/to/page.tsx` — full SEO audit with PASS/WARN/FAIL checklist
- `/seo-audit-component path/to/component.tsx` — component SEO review

### Agent persona

The `seo-auditor` agent provides a senior SEO engineer perspective when reviewing code. Claude Code can use it automatically or you can reference it in conversations.

### GitHub Copilot instructions

Copilot instructions load automatically based on the file you're editing:
- Editing a page file → `pages.instructions.md` applies
- Editing a component → `components.instructions.md` applies
- Editing an API route → `api.instructions.md` applies

The main `copilot-instructions.md` applies to all files.

## Customization

### Adding custom rules

To add project-specific SEO rules, edit the relevant SKILL.md or create a new skill:

```bash
mkdir -p .claude/skills/seo-custom/
# Create .claude/skills/seo-custom/SKILL.md with your rules
```
