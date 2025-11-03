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

- Current season: Season 3
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

## GitHub Actions Workflow Guidelines

When working with `.github/workflows/*.yml` files, follow these best practices:

### Security

- **Never hardcode secrets**: Use GitHub secrets (`${{ secrets.SECRET_NAME }}`)
- **Minimal permissions**: Only grant necessary GITHUB_TOKEN permissions
  ```yaml
  permissions:
    contents: read  # Only what's needed
    pages: write    # For deployment
  ```

### Performance

- **Use caching**: Cache dependencies to speed up workflows
  ```yaml
  - uses: actions/setup-node@v6
    with:
      cache: 'npm'  # Automatic caching

  - uses: ruby/setup-ruby@v1
    with:
      bundler-cache: true  # Automatic gem caching
  ```
- **Add timeouts**: Prevent stuck workflows
  ```yaml
  jobs:
    build:
      timeout-minutes: 10
  ```
- **Use matrices**: Test across multiple environments efficiently
  ```yaml
  strategy:
    matrix:
      ruby-version: ['3.2', '3.3']
  ```

### Best Practices

- **Descriptive names**: Use clear job and step names
  ```yaml
  name: Deploy to GitHub Pages  # Clear workflow name
  jobs:
    lint:
      name: Lint markdown files  # Clear job name
  ```
- **Standard triggers**: Include common event triggers
  ```yaml
  on:
    push:
      branches: ["master"]
    pull_request:
      branches: ["**"]
    workflow_dispatch:  # Manual trigger
  ```
- **Cleanup steps**: Use `if: always()` for cleanup that must run
  ```yaml
  - name: Cleanup
    if: always()
    run: rm -rf temp-files
  ```

### Workflow Structure for This Project

**validate.yml** (for PRs and feature branches):
- Runs on: All pull requests, pushes to non-master branches
- Purpose: Validate changes before merge
- Jobs: lint (markdown), build (Jekyll test build)
- Does NOT deploy

**jekyll.yml** (for production):
- Runs on: Only master branch pushes
- Purpose: Build and deploy to production
- Jobs: lint, build, deploy to GitHub Pages
- Requires all checks to pass before deploy

### Workflow Best Practices for Documentation

- Always lint before building
- Verify build output exists after Jekyll build
- Use `JEKYLL_ENV: production` for production builds
- Test with temporary baseurl in validation (`--baseurl "/test"`)
- Use production baseurl for deployment (`${{ steps.pages.outputs.base_path }}`)

## Testing & Validation Guidelines

This project uses validation instead of traditional unit tests. Treat linting and builds as "tests."

### Validation Structure

Follow the "Arrange, Act, Assert" pattern adapted for documentation:

1. **Arrange**: Set up environment (checkout, install dependencies)
2. **Act**: Run validation (lint, build)
3. **Assert**: Verify results (check for errors, verify output exists)

### Markdown Linting as Tests

Treat markdown linting like unit tests:

```yaml
- name: Run markdownlint  # "Test"
  run: npm run lint

# This tests:
# - No duplicate H1 headings (MD025)
# - Blank lines around fences (MD031)
# - Alt text on images (MD045)
# - Descriptive links (MD059)
# - Proper heading hierarchy (MD001)
```

### Build Verification

Jekyll build = integration test:

```yaml
- name: Build with Jekyll
  run: bundle exec jekyll build

- name: Verify build output  # Assert
  run: |
    if [ ! -d "_site" ]; then
      echo "Error: _site directory not created"
      exit 1
    fi
    echo "✅ Build successful"
```

### Test Edge Cases

Don't just test happy paths. Test problematic scenarios:

**Good validation coverage:**
- ✅ Valid markdown with proper front matter
- ✅ Missing front matter fields (should fail)
- ✅ Circular navigation references (should fail)
- ✅ Broken internal links (should fail)
- ✅ Invalid YAML in front matter (should fail)
- ✅ Missing parent pages (should fail)

**Test both success and failure:**
```yaml
# Test that valid markdown passes
- run: npm run lint

# Test that invalid markdown fails (in separate test file)
- run: |
    echo "# Test" > test.md
    echo "# Duplicate H1" >> test.md
    ! npm run lint  # Expect failure
```

### Validation Checklist

Every PR should validate:

1. **Markdown linting passes**: No MD* rule violations
2. **Jekyll builds successfully**: No build errors
3. **Build output complete**: _site directory contains expected files
4. **Navigation valid**: No circular references, all parents exist
5. **Links resolve**: Internal links point to existing pages
6. **Front matter complete**: All required fields present

### Mocking External Dependencies

For this documentation project, "mocking" means:

- Use test baseurl instead of production (`--baseurl "/test"`)
- Build without deploying (validate.yml doesn't have deploy job)
- Verify structure without checking actual content accuracy

### Parameterized Testing

Test multiple scenarios efficiently:

```yaml
strategy:
  matrix:
    test-case:
      - name: "Valid documentation"
        path: "_docs/server-rules/overview.md"
        should-pass: true
      - name: "Circular reference"
        path: "_docs/test-circular.md"
        should-pass: false
```

### When Validation Fails

Treat validation failures like test failures:

1. **Identify the issue**: What validation failed? (lint, build, etc.)
2. **Locate the cause**: Which file or line caused the failure?
3. **Fix the root cause**: Don't just fix symptoms
4. **Verify the fix**: Run validation locally before pushing
5. **Add a check**: Consider if new validation rules are needed

## Code Review Guidelines

When reviewing pull requests, act as a thorough code reviewer following these principles:

### Review Objectives

1. **Ensure correctness**: Verify changes work as intended and don't break existing functionality
2. **Maintain quality**: Check for adherence to project standards and best practices
3. **Improve clarity**: Suggest improvements to documentation readability
4. **Catch issues early**: Identify potential problems before they reach production

### What to Review

#### Critical Issues (Must Fix)

- **Circular navigation references**: `title` must NOT match `parent` value
- **Missing required front matter**: Every page needs `layout`, `title`, `parent` (if applicable), `nav_order`, `permalink`
- **Broken internal links**: All `/docs/...` links must resolve to actual pages
- **Markdown linting failures**: Code must pass `npm run lint`
- **Build failures**: Jekyll must build successfully without errors
- **Security concerns**: No exposed credentials, API keys, or sensitive information

#### Important Issues (Should Fix)

- **Inconsistent formatting**: Headings, lists, spacing should match existing docs
- **Missing alt text**: All images should have descriptive alt text
- **Non-descriptive link text**: Avoid "click here", "here", use descriptive text
- **Outdated information**: Check if content reflects current server state
- **Missing `last_modified_at`**: Should be updated when editing existing pages
- **Incorrect parent/child relationships**: Verify navigation hierarchy makes sense

#### Suggestions (Nice to Have)

- **Improved clarity**: More concise or clearer wording
- **Better examples**: Add code examples or screenshots where helpful
- **Consistent tone**: Match existing documentation voice (direct, present tense)
- **Enhanced organization**: Better heading structure or content flow

### Review Process

1. **Start with critical issues**: Check navigation, front matter, links first
2. **Verify build success**: Ensure CI/CD validation workflow passes
3. **Review content changes**: Check accuracy and clarity
4. **Check markdown quality**: Verify linting rules followed
5. **Test locally if significant**: For major changes, recommend local testing
6. **Provide constructive feedback**: Be specific, helpful, and respectful

### Review Comments Format

When leaving comments, be:

- **Specific**: Point to exact lines and explain the issue
- **Clear**: Explain what's wrong and why it matters
- **Helpful**: Suggest a solution or provide an example
- **Respectful**: Assume good intent, be encouraging

**Good comment example:**
```
This creates a circular reference where the page title matches its parent.
The navigation system won't work correctly with this setup.

Suggestion: Change the title to "Overview" to differentiate from the parent page.
```

**Bad comment example:**
```
This is wrong.
```

### Review Priorities

When reviewing PRs, focus on these areas in order:

1. **Navigation integrity**: Check for circular references, missing parent relationships
2. **Front matter completeness**: All required fields present and correct
3. **Build success**: Verify CI/CD workflows pass (validate.yml for branches, jekyll.yml for master)
4. **Markdown quality**: Linting rules followed (no MD025, MD031, MD045, MD059, MD001 errors)
5. **Link validity**: Internal links use permalinks and resolve correctly
6. **Content accuracy**: Factual information about server, mods, plugins, gameplay
7. **Consistency**: Matches existing documentation style and conventions
8. **Completeness**: Documentation is thorough and addresses the topic fully

### Red Flags to Watch For

- Page with same title as its parent (circular reference)
- Missing `layout: default` in documentation pages
- Using old layouts (`single`, `splash`) instead of `default`/`home`
- Links to files instead of permalinks (`/docs/page.md` vs `/docs/page/`)
- Images without alt text
- H1 headings in content when title is in front matter (causes MD025 error)
- Missing blank lines around code fences (causes MD031 error)
- Skipped heading levels (H2 → H4, causes MD001 error)
- Pushing to master without PR review

### Things to Approve Quickly

- Simple typo fixes
- `last_modified_at` updates
- Documentation improvements that don't change structure
- Adding alt text to images
- Fixing broken links
- Markdown formatting fixes

### When to Request Changes

- Critical issues present (circular references, broken builds, missing fields)
- Multiple important issues that should be addressed
- Security or safety concerns
- Changes that would break existing functionality

### When to Approve with Comments

- Only minor suggestions or nice-to-haves
- Changes are good but could be enhanced
- Non-blocking improvements identified

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
