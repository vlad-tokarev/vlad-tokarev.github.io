# vtok.xyz - Personal Blog

Personal website and blog built with Hugo, hosted on GitHub Pages.

## Project Structure

```
vtok.xyz/
├── content/           # Blog content (posts, pages)
│   ├── posts/         # Blog posts (page bundles)
│   ├── archives.md    # Archives page (EN)
│   ├── archives.ru.md # Archives page (RU)
│   ├── search.md      # Search page (EN)
│   └── search.ru.md   # Search page (RU)
├── themes/PaperMod/   # Theme (git submodule)
├── static/            # Static assets
├── assets/            # Hugo assets (CSS, JS)
├── layouts/           # Custom layout overrides
├── hugo.yaml          # Main configuration
└── public/            # Generated site (gitignored)
```

## Quick Commands

```bash
# Run local development server
hugo server -D

# Build the site
hugo

# Create a new post
hugo new posts/my-post/index.md
```

## Multilingual Setup

The site supports two languages:
- **English (en)** - default, at root `/`
- **Russian (ru)** - at `/ru/`

### Creating Posts

Posts use page bundles (folder with `index.md`):

```
content/posts/my-post/
├── index.md      # English version
├── index.ru.md   # Russian version
└── image.png     # Shared images
```

### Front Matter Template

```yaml
---
title: "Post Title"
date: 2025-11-30
draft: false
tags: ["Tag1", "Tag2"]
categories: ["Category"]
summary: "Brief description for post list"
---
```

## Theme (PaperMod)

Uses [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme as a git submodule.

### Currently Enabled Features

- Reading time display (`ShowReadingTime: true`)
- Code copy buttons (`ShowCodeCopyButtons: true`)
- Breadcrumbs (`ShowBreadCrumbs: true`)
- Post navigation links (`ShowPostNavLinks: true`)
- Auto theme - light/dark (`defaultTheme: auto`)
- Fuse.js search with JSON output
- RSS feeds for both languages

### Homepage Modes

**Home-Info Mode** (currently used):
```yaml
params:
  homeInfoParams:
    Title: "Welcome"
    Content: "Description text"
  socialIcons:
    - name: github
      url: "https://github.com/username"
```

**Profile Mode** (alternative):
```yaml
params:
  profileMode:
    enabled: true
    title: "Your Title"
    subtitle: "Subtitle text"
    imageUrl: "image_link"
    imageWidth: 120
    imageHeight: 120
    buttons:
      - name: "Archive"
        url: "/archive"
```

### Post Cover Images

```yaml
cover:
  image: "path/url"
  alt: "alternate text"
  caption: "caption text"
  relative: true  # for page bundle images
```

Global cover settings:
```yaml
params:
  cover:
    hidden: true           # hide on post page
    hiddenInList: true     # hide in list view
    hiddenInSingle: true   # hide in single view
    responsiveImages: false
    linkFullImages: true
```

### Table of Contents

Per-post or global:
```yaml
ShowToc: true
TocOpen: true  # expanded by default
```

### Edit Link (for GitHub)

```yaml
params:
  editPost:
    URL: "https://github.com/user/repo/tree/master/content"
    Text: "Suggest Changes"
    appendFilePath: true
```

### Search Configuration

Requires JSON output (already enabled):
```yaml
outputs:
  home:
    - HTML
    - RSS
    - JSON
```

Fuse.js options:
```yaml
params:
  fuseOpts:
    isCaseSensitive: false
    shouldSort: true
    threshold: 0.4
    minMatchCharLength: 0
    keys: ["title", "permalink", "summary", "content"]
```

### Comments Integration

Create `layouts/partials/comments.html` with your provider code, then:
```yaml
params:
  comments: true
```

### Keyboard Shortcuts

- `c` - Toggle table of contents
- `g` - Go to top
- `h` - Home
- `t` - Toggle theme
- `/` - Search page

### Other Available Options

```yaml
params:
  ShowShareButtons: true      # social share buttons
  ShowWordCount: true         # word count display
  disableThemeToggle: true    # hide theme switcher
  disableScrollToTop: true    # hide scroll-to-top button
  hidemeta: true              # hide post metadata
  hideSummary: true           # hide post summary in list
```

## Deployment

Automatic deployment via GitHub Actions on push to `master`:
1. GitHub Actions builds site with Hugo 0.147.0
2. Deploys to GitHub Pages

Workflow: `.github/workflows/deploy.yml`

## Configuration Notes

- Base URL: `https://vtok.xyz/`
- RSS feeds: enabled for both languages
- JSON output: enabled for search functionality
- Comments: disabled
- Share buttons: disabled

## Content Guidelines

- Posts go in `content/posts/` as page bundles
- Images should be placed inside the post bundle
- Use British English for English content
- Tags and categories help with organisation
