# Contributing to Goobercraft Documentation

<!-- markdownlint-disable MD013 -->

Thank you for your interest in improving the Goobercraft documentation! This guide will help you contribute effectively.

## How to Contribute

### 🚀 New to Contributing? Start Here!

**Not technical? No problem!** You can edit documentation directly in your web browser without installing anything.

👉 **See [QUICK_EDIT_GUIDE.md](QUICK_EDIT_GUIDE.md) for a beginner-friendly guide**

Key points:

- Edit files directly on GitHub (no installation needed)
- Use VS Code for a better editing experience (optional)
- Templates are available in `_templates/` to get started quickly
- The linter will help fix formatting issues automatically

**Choose your path:**

- **Simple edits** (typos, small changes) → Use GitHub's web editor
- **Larger contributions** → Follow the full setup below

---

### Reporting Issues

Found a typo, broken link, or outdated information?

1. Check if an issue already exists
2. Open a new issue with:
   - Clear title describing the problem
   - Location of the issue (file and line if possible)
   - What's wrong and what it should be
   - Screenshots if helpful

### Suggesting Improvements

Have ideas for new documentation or improvements?

1. Open an issue first to discuss major changes
2. Explain the benefit to the community
3. Be open to feedback and alternatives

### Making Changes

#### Prerequisites

Before you start, you'll need:

- Git installed
- Ruby 3.2+ and Bundler
- Node.js 20+ and npm (for markdown linting)
- A GitHub account
- A text editor

#### Setup

1. **Fork the repository** on GitHub

2. **Clone your fork**:

   ```bash
   git clone https://github.com/YOUR-USERNAME/docs.goobercraft.com.git
   cd docs.goobercraft.com
   ```

3. **Install dependencies**:

   ```bash
   # Install Ruby dependencies
   bundle install

   # Install Node.js dependencies (for linting)
   npm install
   ```

4. **EditorConfig support** (automatic):
   - Most editors will automatically detect and use [.editorconfig](.editorconfig)
   - VS Code: Built-in support (no setup needed)
   - Other editors: May need a plugin (check [EditorConfig.org](https://editorconfig.org/#download))
   - Handles indentation, line endings, and encoding automatically

5. **Create a branch**:

   ```bash
   git checkout -b your-descriptive-branch-name
   ```

#### Making Your Changes

1. **Edit the markdown files** in your text editor
   - Follow the existing style and structure
   - Use clear, concise language
   - Include relevant links

2. **Update front matter**:

   ```yaml
   ---
   title: "Page Title"
   last_modified_at: YYYY-MM-DD  # Update this!
   ---
   ```

3. **Test locally**:

   ```bash
   bundle exec jekyll serve
   ```

   Then visit `http://localhost:4000` to preview your changes

#### Markdown Linting

We use [markdownlint](https://github.com/DavidAnson/markdownlint) to maintain consistent markdown formatting.

**Before committing, lint your changes:**

```bash
# Check for linting errors
npm run lint

# Auto-fix many common issues
npm run lint:fix
```

**Common linting rules:**

- Use ATX-style headings (`#` not underlines)
- Use dashes for unordered lists (`-` not `*` or `+`)
- Maximum line length: 120 characters (except code blocks and tables)
- No trailing whitespace
- Blank line before and after headings, lists, code blocks
- Consistent indentation (2 spaces for nested lists)

**Linter configuration:**

The linter is configured in [.markdownlint.json](.markdownlint.json). If you think a rule should be changed, open an issue to discuss it.

**Ignoring linting rules:**

If you absolutely need to disable a rule for a specific line:

```markdown
<!-- markdownlint-disable MD033 -->
<div>Some inline HTML that would normally trigger a warning</div>
<!-- markdownlint-enable MD033 -->
```

Use this sparingly!

#### Commit Your Changes

1. **Stage your changes**:

   ```bash
   git add .
   ```

2. **Commit with a clear message**:

   ```bash
   git commit -m "Fix typo in server connection guide"
   ```

   Good commit messages:
   - `Fix typo in community rules`
   - `Update Minecraft version to 1.20.4`
   - `Add section about redstone guidelines`
   - `Improve formatting in FAQ`

3. **Push to your fork**:

   ```bash
   git push origin your-descriptive-branch-name
   ```

#### Open a Pull Request

1. Go to the original repository on GitHub
2. Click "New Pull Request"
3. Select your fork and branch
4. Fill out the PR template:
   - **Title**: Clear, descriptive summary
   - **Description**: What changed and why
   - **Related Issues**: Link any related issues

5. Submit and wait for review

## Contribution Guidelines

### Writing Style

- **Clear and Concise**: Get to the point
- **Active Voice**: "Click the button" not "The button should be clicked"
- **Inclusive Language**: "They" not "he/she"
- **Beginner-Friendly**: Explain jargon, don't assume knowledge
- **Consistent Tone**: Friendly but professional

### Documentation Structure

- **Front Matter**: Every page needs proper YAML front matter
- **Headings**: Use logical hierarchy (H1 → H2 → H3)
- **Links**: Use relative links for internal pages
- **Code Blocks**: Specify language for syntax highlighting
- **Lists**: Use for scannable information
- **Examples**: Show, don't just tell

### Code Examples

When including code or commands:

```bash
# Good: Include comments explaining what the command does
bundle exec jekyll serve --livereload

# Show expected output when helpful
# => Server address: http://127.0.0.1:4000/
```

### Markdown Best Practices

1. **Use Reference Links** for repeated URLs:

   ```markdown
   [Community Rules][rules]
   [Code of Conduct][rules]

   [rules]: /docs/community-rules/overview/
   ```

2. **Format Lists Properly**:

   ```markdown
   - First item
   - Second item
     - Nested item (2 space indent)
     - Another nested item
   - Third item
   ```

3. **Use Tables for Data**:

   ```markdown
   | Feature | Supported |
   |---------|-----------|
   | PvP     | Yes       |
   | Grief   | No        |
   ```

4. **Add Alt Text to Images**:

   ```markdown
   ![Server spawn area showing the welcome plaza](path/to/image.jpg)
   ```

### File Naming

- Use lowercase with hyphens: `getting-started.md`
- Be descriptive: `server-connection-guide.md` not `guide.md`
- Match the content: filename should reflect the page title

### Front Matter Requirements

All documentation pages must include:

```yaml
---
title: "Human-Readable Title"
permalink: /docs/category/page-name/
excerpt: "Brief 1-2 sentence description"
last_modified_at: YYYY-MM-DD
toc: true  # Include table of contents
---
```

## Review Process

### What to Expect

1. **Automated Checks**:
   - Markdown linting runs automatically
   - Jekyll build must succeed
   - All checks must pass before merge

2. **Manual Review**:
   - A maintainer will review your changes
   - They may request changes or ask questions
   - Be responsive to feedback

3. **Approval and Merge**:
   - Once approved, a maintainer will merge
   - Your contribution will go live with the next deployment!

### Getting Feedback

- Be patient - reviews take time
- Ask questions if feedback is unclear
- Don't take criticism personally
- Iterate based on feedback

## Need Help?

Stuck? Have questions?

- **Check existing docs**: [README.md](README.md), [SETUP.md](SETUP.md)
- **Ask in Discord**: (Add Discord link)
- **Open an issue**: Describe what you're trying to do
- **Tag maintainers**: In your PR if you need help

## Recognition

Contributors are valued members of our community! Your contributions help everyone.

## License

By contributing, you agree that your contributions will be licensed under the same license as this project.

---

Thank you for helping make Goobercraft documentation better! 🎉
