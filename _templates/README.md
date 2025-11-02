# Documentation Templates

This folder contains templates for common documentation page types. These templates help ensure consistency and make it easier for new contributors to create well-structured pages.

## Available Templates

### 1. Documentation Page (`documentation-page.md`)

**Use for:** General documentation pages

**Best for:**

- Feature descriptions
- System explanations
- Reference documentation
- Overview pages

### 2. Guide Page (`guide-page.md`)

**Use for:** Step-by-step tutorials and guides

**Best for:**

- How-to guides
- Setup instructions
- Walkthrough tutorials
- Process documentation

### 3. Rule Page (`rule-page.md`)

**Use for:** Community rules and policies

**Best for:**

- Rule explanations
- Policy documentation
- Guidelines with examples
- Compliance requirements

## How to Use Templates

### Method 1: Copy and Paste

1. Open the template file that matches your needs
2. Copy all the content
3. Create your new file in the appropriate `_docs/` subfolder
4. Paste the template content
5. Fill in your content, replacing template placeholders
6. Update the front matter (title, permalink, date)

### Method 2: Command Line

```bash
# Copy template to new location
cp _templates/documentation-page.md _docs/category/your-page-name.md

# Edit the new file
# Update front matter and replace template content
```

### Method 3: VS Code

1. Open the template file
2. Right-click → Copy
3. Navigate to your target folder
4. Right-click → Paste
5. Rename the file appropriately
6. Edit the content

## Template Sections

All templates include:

- **Front matter** - YAML configuration at the top
- **Headings structure** - Logical organization
- **Common sections** - Standard sections most pages need
- **Examples** - Formatting examples you can follow
- **Placeholders** - Text in [brackets] or "Your X Here" to replace

## Customizing Templates

Feel free to:

- Remove sections you don't need
- Add new sections specific to your content
- Adjust heading levels as needed
- Modify the structure for your use case

But always keep:

- The front matter block (with correct values)
- Proper heading hierarchy
- Consistent formatting

## Front Matter Fields

Every page needs this at the top:

```yaml
---
title: "Page Title"              # Human-readable title
permalink: /docs/category/page/  # URL path
excerpt: "Brief description"     # Used in previews/search
last_modified_at: YYYY-MM-DD    # Today's date
toc: true                        # Table of contents (usually true)
---
```

**Important:**

- `title`: The page title as shown to readers
- `permalink`: Must match the file location pattern
- `excerpt`: Keep it to 1-2 sentences
- `last_modified_at`: Update whenever you edit the page
- `toc`: Set to `false` only for short pages

## Naming Conventions

### File Names

- Use lowercase
- Separate words with hyphens
- Be descriptive: `server-connection-guide.md` not `guide.md`
- Match the content: filename should reflect the page title

### Permalinks

- Follow the pattern: `/docs/category/page-name/`
- Use hyphens, not underscores
- Keep them short but descriptive
- Don't include file extensions

## Common Patterns

### Documentation Structure

```
_docs/
├── category-1/
│   ├── overview.md           (category introduction)
│   ├── topic-1.md           (specific topic)
│   ├── topic-2.md           (specific topic)
│   └── faq.md               (category FAQs)
├── category-2/
│   └── ...
```

### Heading Hierarchy

```markdown
# Page Title (automatically from front matter)
## Main Section
### Subsection
#### Sub-subsection (use sparingly)
```

## Tips for Success

1. **Start with the right template** - Choose the one that matches your content type
2. **Fill in all sections** - Don't leave template placeholders
3. **Update the date** - Always set `last_modified_at` to today
4. **Check the permalink** - Make sure it matches your folder structure
5. **Preview locally** - Test with `bundle exec jekyll serve`
6. **Run the linter** - Use `npm run lint:fix` before submitting

## Questions?

- See [QUICK_EDIT_GUIDE.md](../QUICK_EDIT_GUIDE.md) for editing basics
- See [CONTRIBUTING.md](../CONTRIBUTING.md) for full contribution guidelines
- Ask in Discord if you need help choosing a template
- Look at existing pages for examples

---

Remember: Templates are starting points. Adapt them to fit your content's needs!
