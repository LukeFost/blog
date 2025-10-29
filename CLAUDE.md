# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll blog deployed on Netlify, focused on sharing ideas about Claude Code, development strategies, and research. The blog uses a Gruvbox Dark theme and is hosted at `blog.lukefoster.net`.

## Architecture

### Jekyll Structure
- **`_posts/`**: Blog post markdown files with YAML frontmatter
- **`_layouts/`**: HTML templates (default.html for all pages)
- **`assets/images/`**: SVG diagrams and GIF animations referenced in posts
- **`_config.yml`**: Jekyll configuration (title, URL, plugins, exclusions)
- **`Gemfile`**: Ruby dependencies (Jekyll ~4.3, jekyll-feed)

### Post Format
All posts in `_posts/` follow this structure:
```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD
tags: [tag1, tag2, tag3]
---
```

Use `tags:` (not `categories:`) for consistency. Dates follow `/posts/:year/:month/:day/:title/` permalink structure.

### Styling
The blog uses an embedded Gruvbox Dark theme in `_layouts/default.html`:
- Background: `#282828`
- Text: `#ebdbb2` (body), `#fabd2f` (headings), `#83a598` (links)
- Code blocks: `#3c3836` background
- When adding SVGs, ensure colors work on dark backgrounds (transparent backgrounds, light text)

## Common Development Tasks

### Build and Test Locally
```bash
bundle install
bundle exec jekyll serve
```
Runs on `http://localhost:4000`

### Creating Posts
1. Create file: `_posts/YYYY-MM-DD-title.md`
2. Add frontmatter with title, date, and tags
3. Write content in markdown
4. Images: reference as `![alt]({{ '/assets/images/filename' | relative_url }})`
4. For cache-busting: add `?v=N` parameter to URLs: `{{ '/assets/images/filename.svg?v=3' | relative_url }}`

### Adding Images/SVGs
- Place in `assets/images/`
- **SVGs**: Must have `fill="transparent"` background and light text colors for dark theme
- **GIFs**: Reference with cache-busting parameter `?v=N` (increment on updates)
- **Markdown reference**: Use Jekyll's `relative_url` filter for consistent paths

### Deployment
- Push to `main` branch on GitHub
- Netlify automatically builds via `netlify.toml` command: `bundle install && bundle exec jekyll build`
- Build output: `_site/` directory
- No SPA redirects (removed inappropriate catch-all redirect for static site)

## Key Configuration Notes

### `_config.yml`
- `url: "https://blog.lukefoster.net"` (must match actual domain for correct URLs)
- `permalink: /posts/:year/:month/:day/:title/` (standard format)
- `jekyll-feed` plugin: generates RSS feed automatically
- Excludes: `.gitignore`, `README.md` (not published)

### `netlify.toml`
- Build command: `bundle install && bundle exec jekyll build`
- Publish directory: `_site/`
- Environment: `JEKYLL_ENV=production`
- No redirects configured (site is static, not SPA)

## Writing Standards

Apply William Strunk Jr.'s *Elements of Style* principles:
- **Rule 10**: Use active voice
- **Rule 11**: Put statements in positive form
- **Rule 12**: Use definite, specific, concrete language
- **Rule 13**: Omit needless words
- Use the `/publish` skill (referenced in README) for guided post publication

## Common Issues and Solutions

### SVGs Not Showing
- **Problem**: SVGs with light backgrounds/dark text don't display on dark theme
- **Solution**: Set background to `transparent`, use Gruvbox light colors (`#fabd2f`, `#d5c4a1`)
- **Verification**: Open SVG in browser, ensure visibility against dark backgrounds

### Images Not Updating
- **Problem**: Browser/CDN caching serves old images
- **Solution**: Add cache-busting parameter: `?v=N` (increment N on updates)
- **Test**: Hard refresh (Cmd+Shift+R or Ctrl+Shift+F5) to verify new version loads

### Build Failures on Netlify
- Check `netlify.toml` for correct build command
- Ensure `Gemfile` dependencies match local environment
- Verify Jekyll version compatibility (~4.3)

## Jekyll Front Matter Best Practices

```yaml
---
layout: post
title: "Clear, Specific Title"
date: YYYY-MM-DD
tags: [tag1, tag2, tag3]
---
```

Tags should be lowercase, hyphen-separated if multi-word. Use tags consistently across posts for discoverability.
