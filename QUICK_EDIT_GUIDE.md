# Quick Edit Guide for Non-Technical Users

This guide is for community members who want to help improve documentation but aren't familiar with Git, command line tools, or development workflows.

## The Easy Way: Edit on GitHub

You can edit documentation files directly in your web browser without installing anything!

### Step-by-Step: Making a Simple Edit

1. **Find the file you want to edit**
   - Browse to the file on GitHub: `https://github.com/YOUR-ORG/docs.goobercraft.com`
   - Navigate through folders to find the page (e.g., `_docs/community-rules/overview.md`)

2. **Click the pencil icon** (Edit this file)
   - In the top-right corner of the file view
   - This opens the web editor

3. **Make your changes**
   - Edit the text directly in the browser
   - Preview tab shows how it will look

4. **Propose the change**
   - Scroll to the bottom
   - Write a brief description: "Fixed typo in community rules"
   - Click **"Propose changes"**
   - Then click **"Create pull request"**
   - Click **"Create pull request"** again

5. **Done!**
   - A maintainer will review and merge your change
   - You'll be notified when it's live!

## The Easier Way: Use VS Code (If You Prefer a Desktop App)

VS Code is a free, user-friendly editor that makes writing markdown easier.

### One-Time Setup

1. **Install VS Code**
   - Download from: <https://code.visualstudio.com/>
   - It's free and works on Windows, Mac, and Linux

2. **Clone the repository**
   - In VS Code: View → Command Palette (Ctrl+Shift+P)
   - Type: "Git: Clone"
   - Enter: `https://github.com/YOUR-ORG/docs.goobercraft.com.git`
   - Choose a folder on your computer

3. **Install recommended extensions**
   - VS Code will prompt you to install recommended extensions
   - Click **"Install All"** (these help with markdown formatting)

4. **Automatic formatting setup**
   - VS Code will automatically use our `.editorconfig` file
   - This handles indentation, line endings, and character encoding
   - You don't need to configure anything - it just works!

### Making Changes in VS Code

1. **Open the file** you want to edit (in the left sidebar)

2. **Edit the content**
   - VS Code will show:
     - ✅ Green squiggles: Things it can auto-fix
     - ⚠️ Yellow warnings: Things to check
     - ❌ Red errors: Things that need fixing

3. **Auto-fix formatting issues**
   - Right-click in the file
   - Select **"Format Document"**
   - Or save the file (Ctrl+S) - it auto-fixes on save!

4. **Save and commit**
   - Click the Source Control icon (left sidebar)
   - Type a message: "Updated server connection guide"
   - Click the checkmark to commit
   - Click **"Sync Changes"** to upload

## Markdown Basics (What You Need to Know)

### Headings

```markdown
# Big Heading (Page Title)
## Medium Heading (Section)
### Small Heading (Subsection)
```

### Text Formatting

```markdown
**Bold text** - Use double asterisks
*Italic text* - Use single asterisks
```

### Links

```markdown
[Link text](/docs/page-name/)
[External link](https://example.com)
```

### Lists

```markdown
Unordered list:
- First item
- Second item
  - Nested item (2 spaces indent)
- Third item

Numbered list:
1. First step
2. Second step
3. Third step
```

### Code Blocks

````markdown
```bash
command to run
```

```yaml
key: value
```
````

### Important Notes

```markdown
**Note:** This is important information.

**Warning:** Be careful about this.
```

## Common Formatting Rules (Auto-Enforced)

Don't worry too much about these - the linter will help you fix them!

### Things to Remember

1. **Headings**: Use `#` symbols, not underlines

   ```markdown
   ✅ # Good Heading
   ❌ Bad Heading
      ===========
   ```

2. **Lists**: Use dashes `-`, not asterisks or plus signs

   ```markdown
   ✅ - List item
   ❌ * List item
   ```

3. **Line Length**: Try to keep lines under 120 characters
   - The editor will show a subtle line at 120 characters
   - It's okay to go over for links or code

4. **Spacing**:
   - Blank line before and after headings
   - Blank line before and after lists
   - Blank line before and after code blocks

### Example of Good Formatting

```markdown
## Section Title

This is a paragraph with some information.

### Subsection

Here are some important points:

- First point
- Second point
- Third point

Check out the [Community Rules](/docs/community-rules/overview/) for more info.

```

## Getting Help

### If You're Stuck

1. **Don't worry!** Making mistakes is okay
2. **Ask for help** in Discord or open an issue
3. **Look at existing pages** for examples
4. **The linter will catch issues** - maintainers can help fix them

### If the Linter Shows Errors

When you create a pull request, an automatic check runs. If it fails:

1. **Check the error message** - it usually tells you what's wrong
2. **Common fixes**:
   - Add blank lines around headings
   - Use dashes for lists
   - Remove trailing spaces at end of lines
3. **Ask a maintainer** - They can fix it or guide you

### Getting Familiar with GitHub

If GitHub is new to you:

- **Fork** = Make your own copy of the repository
- **Branch** = A separate version where you make changes
- **Commit** = Save your changes with a description
- **Pull Request (PR)** = Ask maintainers to include your changes
- **Merge** = Your changes are added to the main documentation

## Tips for Success

### Before You Start

1. ✅ Check if someone else is already fixing the same thing
2. ✅ Make small, focused changes (easier to review)
3. ✅ Update the `last_modified_at` date in the page header

### While Editing

1. ✅ Preview your changes if possible
2. ✅ Read what you wrote - does it make sense?
3. ✅ Check links work
4. ✅ Use simple, clear language

### After Submitting

1. ✅ Check for comments on your pull request
2. ✅ Be responsive to feedback
3. ✅ Don't be discouraged by change requests - they're normal!

## Templates

To make it even easier, we've created templates for common page types. Check the `_templates/` folder for:

- Documentation page template
- FAQ entry template
- Guide template

Copy the template, fill in your content, and you're done!

## Still Have Questions?

- **Discord**: Ask in the documentation channel (add link)
- **GitHub Issues**: Open an issue with your question
- **Existing docs**: Look at similar pages for examples
- **Maintainers**: Tag a maintainer in your PR

---

**Remember:** Documentation doesn't have to be perfect. Even small improvements help! We appreciate all contributions, regardless of technical skill level. 🎉
