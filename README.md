# Goobercraft Documentation

Official documentation site for GooberCraft Season 3 - A modded Forge Minecraft server. This repository contains all documentation for server rules, gameplay features, mod information, and more.

## About

This is a [Jekyll](https://jekyllrb.com/) site using the [Just the Docs](https://just-the-docs.com/) theme, automatically deployed to GitHub Pages.

**Live Site**: [https://docs.goobercraft.com](https://docs.goobercraft.com)

## Features

- Dark theme by default
- Full-text search functionality (Lunr.js)
- Front matter-based navigation (no separate navigation file needed)
- Responsive design optimized for documentation
- Automatic deployment via GitHub Actions
- Markdown linting for consistent formatting
- EditorConfig for cross-editor consistency
- Automated dependency updates via Dependabot
- Version-controlled documentation
- GitHub edit links on every page

## Documentation Structure

```
_docs/                 # Documentation content
  server-rules/        # Server rules and content etiquette
  server-info/         # Server information, mods, and specs
  gameplay/            # Gameplay features (ModCoin, shopping, etc.)
    commands/          # Command documentation
  plugins/             # Plugin documentation
  streaming/           # Streaming and content creation guidelines
  faq/                 # Frequently asked questions
_pages/                # Static pages (about, etc.)
assets/                # Images, CSS, and other assets
  images/              # Image files
_config.yml            # Jekyll site configuration
index.md               # Homepage
```

## Local Development

### Prerequisites

- Ruby 3.2 or higher
- Bundler gem
- Node.js 20+ and npm (for markdown linting)
- Git

### Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/GooberCraft/docs.goobercraft.com.git
   cd docs.goobercraft.com
   ```

2. Install dependencies:

   ```bash
   # Install Ruby dependencies
   bundle install

   # Install Node.js dependencies (for linting)
   npm install
   ```

3. Run the local development server:

   ```bash
   bundle exec jekyll serve
   ```

4. Open your browser to `http://localhost:4000`

### Markdown Linting

We use [markdownlint](https://github.com/DavidAnson/markdownlint) to ensure consistent markdown formatting across all documentation.

**Lint your markdown files:**

```bash
# Check for linting errors
npm run lint

# Auto-fix many common issues
npm run lint:fix
```

**Key linting rules:**

- ATX-style headings (`#` syntax)
- Maximum line length: 120 characters
- Consistent list formatting with dashes
- No trailing whitespace
- Proper spacing around headings and lists

Configuration is in [.markdownlint.json](.markdownlint.json). The linter runs automatically in CI/CD.

### EditorConfig

We use [EditorConfig](https://editorconfig.org/) to maintain consistent formatting across all editors and IDEs.

**Automatic formatting:**

- Your editor automatically applies formatting rules from [.editorconfig](.editorconfig)
- Works with VS Code, Sublime, Atom, Vim, IntelliJ, and more
- No configuration needed - just open files and edit!

**What it handles:**

- Indentation (2 spaces for YAML, JSON, Ruby)
- Line endings (Unix-style LF)
- Character encoding (UTF-8)
- Trailing whitespace removal
- Final newline insertion

Most modern editors support EditorConfig natively or via a simple plugin installation.

### Live Reload

The local server supports live reload - changes to content will automatically refresh in your browser.

## Contributing

We welcome contributions to improve our documentation!

**For detailed contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md)**

Quick start:

1. Fork the repository
2. Create a new branch
3. Make your changes
4. Run `npm run lint:fix` to auto-fix markdown issues
5. Test locally with `bundle exec jekyll serve`
6. Open a Pull Request

**Key requirements:**

- Follow markdown linting rules (runs in CI)
- Update `last_modified_at` in front matter when editing pages
- Test all changes locally
- Use clear, concise language
- Add proper navigation fields (`parent`, `nav_order`) when creating new pages

## Navigation

Just the Docs uses **front matter-based navigation** instead of a separate navigation file. Each page declares its position in the hierarchy using front matter fields:

- `nav_order`: Position in navigation (1, 2, 3, etc.)
- `parent`: Title of the parent page
- `grand_parent`: Title of the grandparent page (for 3-level nesting)
- `has_children: true`: For parent pages that have children

**Example front matter for a child page:**

```yaml
---
layout: default
title: Client Setup
parent: Getting Started
nav_order: 2
permalink: /docs/client-setup/
---
```

**Example front matter for a parent page:**

```yaml
---
layout: default
title: Getting Started
nav_order: 2
has_children: true
permalink: /docs/getting-started-parent/
---
```

Navigation is automatically generated from these relationships. No separate navigation file is needed!

## Deployment

The site automatically deploys to GitHub Pages when changes are pushed to the `master` branch via GitHub Actions.

### CI/CD Workflow

The deployment workflow ([.github/workflows/jekyll.yml](.github/workflows/jekyll.yml)) runs in three stages:

1. **Lint** - Validates markdown formatting with markdownlint
2. **Build** - Compiles the Jekyll site with production settings
3. **Deploy** - Publishes the built site to GitHub Pages

All stages must pass for deployment to succeed. The workflow can also be triggered manually from the Actions tab.

### Manual Deployment

If needed, you can build the site manually:

```bash
bundle exec jekyll build
```

The generated site will be in the `_site` directory.

## Dependency Management

This repository uses [Dependabot](https://docs.github.com/en/code-security/dependabot) to automatically keep dependencies up to date.

**What Dependabot monitors:**

- **GitHub Actions** - Workflow action versions (checkout, setup-node, setup-ruby, etc.)
- **npm packages** - markdownlint and related development tools
- **Ruby gems** - Jekyll, just-the-docs theme, and plugins

**How it works:**

- Runs weekly checks for all three ecosystems
- Automatically creates pull requests when updates are available
- Includes changelog information, release notes, and compatibility scores
- PRs are labeled by dependency type for easy filtering

Simply review and merge the PRs to keep dependencies current and secure.

## Custom Domain Setup

This site uses the custom domain `docs.goobercraft.com`. To set this up:

1. Add a `CNAME` file with your domain (already included)
2. Configure DNS records:
   - Add a CNAME record pointing to `<username>.github.io`
   - Or add A records pointing to GitHub Pages IPs
3. Enable HTTPS in GitHub Pages settings

### DNS Configuration

Add the following DNS records:

**Option 1: CNAME (recommended for subdomains)**

```
Type: CNAME
Host: docs
Value: goobercraft.github.io
```

**Option 2: A Records (for apex domains)**

```
Type: A
Host: @
Value: 185.199.108.153
Value: 185.199.109.153
Value: 185.199.110.153
Value: 185.199.111.153
```

## Theme Customization

The site uses the Just the Docs theme with:

- **Color Scheme**: Dark mode
- **Search**: Enabled with built-in Lunr.js
- **Navigation**: Front matter-based automatic generation
- **Features**: Heading anchors, back-to-top, GitHub edit links

### Modifying Theme Settings

Edit `_config.yml` to customize:

- Site title and description
- Color scheme (light/dark)
- Search configuration
- Auxiliary links (Discord, GitHub)
- Footer content
- GitHub edit links

### Available Color Schemes

Just the Docs includes several built-in color schemes:

- `light` (default)
- `dark` (currently enabled)
- Custom schemes can be added via CSS

## Adding New Pages

When creating new documentation pages:

1. Create the markdown file in the appropriate `_docs/` subdirectory
2. Add front matter with navigation fields:

   ```yaml
   ---
   layout: default
   title: Your Page Title
   parent: Parent Page Title
   nav_order: 1
   permalink: /docs/category/page/
   ---
   ```

3. Write your content
4. The page will automatically appear in navigation based on the `parent` and `nav_order` fields

## License

This documentation is provided for the GooberCraft community.

## Support

- **Issues**: [GitHub Issues](https://github.com/GooberCraft/docs.goobercraft.com/issues)
- **Discord**: [https://discord.gg/RSZHKQ6cAm](https://discord.gg/RSZHKQ6cAm)
- **In-game**: Contact server staff

## Credits

- Built with [Jekyll](https://jekyllrb.com/)
- Theme by [Just the Docs](https://just-the-docs.com/)
- Hosted on [GitHub Pages](https://pages.github.com/)
- Maintained by the GooberCraft community

---

*GooberCraft isn't just a server, it's a community.*
