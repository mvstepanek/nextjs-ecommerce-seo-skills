# Contributing

Thanks for your interest in improving these SEO skills! Here's how to help.

## Reporting Issues

- Open a [GitHub issue](https://github.com/mvstepanek/nextjs-ecommerce-seo-skills/issues)
- Include the skill name (e.g. `seo-metadata`) and what's wrong or missing
- If it's a false positive (rule triggers when it shouldn't), include a code snippet

## Suggesting New Rules

- Open an issue describing the SEO rule and why it matters
- Link to documentation (Google, schema.org, web.dev) supporting the rule
- Note which skill it belongs to, or propose a new skill

## Pull Requests

1. Fork the repo
2. Create a branch (`git checkout -b fix/metadata-title-length`)
3. Make your changes
4. Test by copying the modified skill into a project and verifying it triggers correctly
5. Open a PR with a clear description of the change

### Guidelines

- Keep SKILL.md files under 500 lines
- Every rule should explain **why** it matters (not just what to do)
- Use generic e-commerce examples — no company-specific references
- Code examples are illustrative — use placeholder names
- Skills are advisory only — they should never auto-fix code

## Skill Structure

Each skill is a directory with a `SKILL.md` file using YAML frontmatter:

```yaml
---
name: skill-name
description: One-line description
paths:
  - "glob/pattern/**/*.tsx"
---
```

See existing skills for reference.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
