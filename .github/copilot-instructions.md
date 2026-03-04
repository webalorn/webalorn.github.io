# Project Guidelines

This is a Jekyll-based academic website using the [Academic Pages](https://academicpages.github.io/) template, hosted on GitHub Pages.

## Build and Test

```bash
# Development server with live reload
bundle exec jekyll serve -l -H localhost

# Build JavaScript assets
npm run build:js

# Install dependencies (if needed)
bundle install
```

## Architecture

| Directory | Purpose |
|-----------|---------|
| `_pages/` | Static pages (about, cv, publications list) |
| `_publications/` | Publication entries (one `.md` per paper) |
| `_data/navigation.yml` | Header navigation config |
| `_includes/` | Reusable HTML components |
| `_layouts/` | Page templates |
| `_sass/` | SCSS stylesheets (`_variables.scss` for customization) |
| `images/` | Site images |

## Content Conventions

### Adding Publications

Create files in `_publications/` with format `YYYY-MM-DD-slug.md`:

```yaml
---
title: "Paper Title"
collection: publications
category: conferences  # conferences | workshop | arxiv
permalink: /publications/YYYY-MM-DD-slug
excerpt: 'Brief description'
date: YYYY-MM-DD
venue: 'Conference/Journal Name'
paperurl: 'https://...'   # Link to paper PDF
codeurl: 'https://...'    # Link to source code
slidesurl: 'https://...'  # Link to slides
---
Paper content in markdown...
```

### Pages Front Matter

```yaml
---
permalink: /url-path/
title: "Page Title"
author_profile: true    # Show sidebar with author info
layout: single          # single | archive | splash
---
```

### Navigation

Edit [_data/navigation.yml](_data/navigation.yml) to add/remove header navigation items.

## Key Files

- [_config.yml](_config.yml) - Site config, author info, social links
- [_pages/about.md](_pages/about.md) - Homepage (sets `permalink: /`)
- [_pages/publications.html](_pages/publications.html) - Publications listing grouped by category
- [_sass/_variables.scss](_sass/_variables.scss) - Colors and typography

## Project Conventions

- Publication categories defined in `_config.yml` under `publication_category`
- Author avatar: `images/profile-picture.jpg`
- Custom publication links: Use `paperurl`, `slidesurl`, `codeurl` in front matter
