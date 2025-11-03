# GitHub Copilot Instructions for GooberCraft Documentation

## Project Overview

This is a Jekyll-based documentation site for GooberCraft. The site uses the Just the Docs theme with dark mode and is deployed to GitHub Pages.

## Technology Stack

- **Static Site Generator**: Jekyll 4.3.4
- **Theme**: Just the Docs (dark color scheme)
- **Deployment**: GitHub Pages via GitHub Actions
- **Linting**: markdownlint-cli
- **Languages**: Markdown, YAML, Ruby (Gemfile)

## Code Style & Conventions

### Markdown

- Use ATX-style headings (`#` syntax, not underline style)
- Maximum line length: 120 characters
- Use dashes (`-`) for unordered lists, not asterisks
- No trailing whitespace
- Proper spacing: blank line before/after headings and lists
- All markdown must pass markdownlint validation

### Front Matter Requirements

Every documentation page MUST have this front matter structure:

```yaml
---
layout: default
title: Page Title
parent: Parent Page Title
nav_order: 1
permalink: /docs/category/page/
last_modified_at: YYYY-MM-DD
---
```

**Critical Rules:**
- `title` must be unique and NOT match the parent page title (avoid circular references)
- `parent` must match exactly (case-sensitive) the title of the parent page
- `grand_parent` is used for 3rd level pages only (max depth is 3 levels)
- `permalink` should follow the pattern `/docs/{category}/{page}/`
- `layout` should be `default` for all docs pages, `home` for homepage

### Navigation System

Just the Docs uses **front matter-based navigation**:

- Navigation hierarchy is automatic based on `parent`, `grand_parent`, and `nav_order`
- NO separate `_data/navigation.yml` file (it was deleted during theme migration)
- Parent pages should have `has_children: true`
- Verify no circular references where a page's title matches its parent

## File Organization

```
_docs/                 # All documentation content
  *-parent.md          # Parent pages for top-level sections
  server-rules/        # Server rules documentation
  server-info/         # Server information (mods, specs, etc.)
  gameplay/            # Gameplay features
    commands/          # Nested commands documentation
  plugins/             # Plugin documentation
  streaming/           # Content creation guidelines
  faq/                 # Frequently asked questions
_pages/                # Static pages (about, 404, etc.)
assets/images/         # Image assets
```

## Common Issues to Watch For

### 1. Circular Navigation References
**Problem**: Page has same title as its parent
```yaml
# BAD - Circular reference
title: Server Rules
parent: Server Rules
```

**Solution**: Child pages need distinct titles
```yaml
# GOOD
title: Overview
parent: Server Rules
```

### 2. Missing Navigation Fields
**Problem**: Documentation page without proper navigation
```yaml
# BAD - Missing parent and nav_order
---
layout: default
title: Some Page
---
```

**Solution**: Include all required fields
```yaml
# GOOD
---
layout: default
title: Some Page
parent: Parent Section
nav_order: 2
permalink: /docs/section/page/
---
```

### 3. Incorrect Layout
**Problem**: Using old Minimal Mistakes layouts
```yaml
layout: single  # Old theme
layout: splash  # Old theme
```

**Solution**: Use Just the Docs layouts
```yaml
layout: default  # For docs pages
layout: home     # For homepage only
```

## Documentation Guidelines

### Content Standards

- Use clear, concise language
- Write in present tense
- Address readers directly ("you can...", not "users can...")
- Include code examples where applicable
- Keep paragraphs short (3-4 sentences max)

### Images

- Store in `/assets/images/`
- Always include descriptive alt text
- Use lowercase filenames with hyphens (not spaces)
- Supported formats: PNG (screenshots), JPG (photos), SVG (logos)

### Links

- Internal links: Use permalinks `/docs/section/page/`
- External links: Use full URLs with HTTPS
- Link text should be descriptive, not "click here" or "here"

## Git & Commit Conventions

### Commit Messages

- Use imperative mood ("Fix bug" not "Fixed bug")
- First line: brief summary (50 chars max)
- Include detailed description for complex changes
- Reference issues/PRs where applicable
- **Never include Claude attribution or authoring messages**

### Branch Strategy

- `master` - production branch, auto-deploys to GitHub Pages
- Feature branches: descriptive names (`migrate-gitbook-season2`, `add-new-section`)
- Theme changes: separate branch (`migrate-just-the-docs-theme`)

## Testing Requirements

Before merging:

1. **Markdown Linting**: `npm run lint` must pass with no errors
2. **Jekyll Build**: Site must build successfully in GitHub Actions
3. **Navigation**: Verify all parent/child relationships work
4. **Links**: Check internal links resolve correctly
5. **Search**: Confirm new pages appear in search

## Special Considerations

### Season-Specific Content

- Current season: Season 2
- This is a modded Forge server (not vanilla Minecraft)
- Update `last_modified_at` when editing existing pages
- Preserve staff roster accuracy

### Theme-Specific Features

Just the Docs provides:

- Automatic navigation from front matter
- Built-in search (Lunr.js)
- Dark mode (`color_scheme: dark` in config)
- Heading anchors
- Back-to-top links
- GitHub edit links
- Breadcrumbs

Do NOT try to add these features manually - they're automatic.

## Review Priorities

When reviewing PRs, focus on:

1. **Navigation integrity**: Check for circular references
2. **Front matter completeness**: All required fields present
3. **Markdown quality**: Linting rules followed
4. **Link validity**: Internal and external links work
5. **Content accuracy**: Factual information about server/mods
6. **Consistency**: Matches existing documentation style

## Repository-Specific Commands

- `npm run lint` - Check markdown formatting
- `npm run lint:fix` - Auto-fix markdown issues
- `bundle exec jekyll serve` - Run local development server
- `bundle exec jekyll build` - Build static site

## Contact & Support

- Repository: https://github.com/MDW-Gaming/docs.goobercraft.com
- Issues: Use GitHub Issues for bugs/suggestions

---

*These instructions help Copilot understand the project structure and provide better suggestions for the GooberCraft documentation site.*
