# Setup Guide for Goobercraft Documentation Site

This guide will help you complete the setup of your Jekyll documentation site and deploy it to GitHub Pages with your custom domain.

## Current Status

Your Jekyll site is now fully configured with:

- ✅ Jekyll configuration with Minimal Mistakes dark theme
- ✅ Sample documentation pages
- ✅ Navigation structure
- ✅ GitHub Actions workflow for automatic deployment
- ✅ Custom domain configuration (CNAME file)

## Next Steps

### 1. Review and Customize Configuration

Edit `_config.yml` to update placeholder information:

```yaml
# Update these fields:
title: Goobercraft Documentation
email: your-email@example.com
repository: "your-github-username/docs.goobercraft.com"
url: "https://docs.goobercraft.com"

# Update author information:
author:
  name: "Goobercraft"
  # Add avatar image if you have one
  # Add links to your social media, Discord, etc.
```

### 2. Initialize Git Repository and Push to GitHub

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial Jekyll site setup with Minimal Mistakes theme"

# Create GitHub repository first, then:
git remote add origin https://github.com/YOUR-USERNAME/docs.goobercraft.com.git

# Push to GitHub
git push -u origin master
```

### 3. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under "Build and deployment":
   - Source: **GitHub Actions** (the workflow is already configured)
4. The site will automatically build and deploy when you push changes

### 4. Configure Custom Domain (docs.goobercraft.com)

#### DNS Configuration

Add these DNS records with your domain registrar:

**For subdomain (docs.goobercraft.com):**

```
Type: CNAME
Host: docs
Value: YOUR-USERNAME.github.io
TTL: 3600 (or default)
```

**OR if using apex domain (goobercraft.com):**

```
Type: A
Host: @
Value: 185.199.108.153

Type: A
Host: @
Value: 185.199.109.153

Type: A
Host: @
Value: 185.199.110.153

Type: A
Host: @
Value: 185.199.111.153
```

#### Enable Custom Domain in GitHub

1. Go to repository **Settings** → **Pages**
2. Under "Custom domain", enter: `docs.goobercraft.com`
3. Click **Save**
4. Wait for DNS check to complete (may take a few minutes to 48 hours)
5. Once verified, enable **Enforce HTTPS**

### 5. Update Placeholder Content

Search for and update these placeholders throughout the documentation:

- **Server address**: `play.goobercraft.com` (update in multiple files)
- **Minecraft version**: Update with your actual server version
- **Discord links**: Add your Discord invite links
- **Email addresses**: Update contact information
- **GitHub repository**: Update with your actual GitHub username/organization
- **Server specifications**: Add actual server specs in `/docs/server-info/`

Files to check:

- `_config.yml`
- `_docs/getting-started.md`
- `_docs/getting-started-quick-start.md`
- `_docs/server-info/overview.md`
- `_docs/server-info/connect.md`
- `_docs/server-info/faq.md`
- `_pages/about.md`
- `index.md`

### 6. Add Images (Optional but Recommended)

The home page references several images. You can either:

**Option A**: Add actual images to `/assets/images/`:

- `header-bg.jpg` - Header background
- `rules-icon.jpg`, `guidelines-icon.jpg`, `server-icon.jpg`, `quickstart-icon.jpg`

**Option B**: Modify `index.md` to remove image references until you have images ready:

```yaml
# Remove or comment out image_path lines in the feature_row sections
```

### 7. Test Locally

Before pushing to production:

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000 in your browser
# Check all links and pages work correctly
```

### 8. Create Additional Documentation

Based on your community's needs, add:

- More detailed server rules
- Building guidelines
- Communication guidelines
- Resource guidelines
- Server specifications
- Gameplay features documentation
- Any other community-specific information

### 9. Set Up Repository Settings

On GitHub:

1. **Protect master branch**:
   - Settings → Branches → Add rule
   - Require pull request reviews (optional)
   - Require status checks to pass

2. **Enable issue templates** (optional):
   - Create issue templates for bug reports and suggestions

3. **Add collaborators**:
   - Settings → Collaborators
   - Add team members who can edit documentation

### 10. Promote Your Documentation

Once live:

- Add link to Discord
- Include in server MOTD
- Share with community members
- Encourage contributions

## Troubleshooting

### Site not building?

- Check GitHub Actions tab for build errors
- Ensure Gemfile and _config.yml are valid
- Check for syntax errors in markdown files

### Custom domain not working?

- Verify DNS records are correct
- Wait up to 48 hours for DNS propagation
- Check GitHub Pages settings
- Ensure CNAME file contains only the domain name

### Images not showing?

- Verify image paths are correct
- Ensure images exist in `/assets/images/`
- Check file names match exactly (case-sensitive)

### Search not working?

- Ensure `search: true` is in `_config.yml`
- Clear browser cache
- Rebuild site

## Maintenance

### Regular Updates

- Update `last_modified_at` when editing pages
- Review and update content regularly
- Check for broken links
- Update Minecraft version when server updates

### Backup

Your documentation is version-controlled with Git, so all history is preserved. Consider:

- Regular commits for changes
- Meaningful commit messages
- Pull requests for major changes

## Getting Help

- **Jekyll Docs**: <https://jekyllrb.com/docs/>
- **Minimal Mistakes Docs**: <https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/>
- **GitHub Pages Docs**: <https://docs.github.com/en/pages>
- **Community**: Ask in Goobercraft Discord or GitHub Issues

## Security Notes

- Never commit sensitive information (API keys, passwords, etc.)
- Review pull requests before merging
- Keep dependencies updated
- Enable branch protection on production branch

---

Good luck with your documentation site! 🚀
