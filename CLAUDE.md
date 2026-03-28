# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based academic portfolio website (al-folio theme) hosted on GitHub Pages at https://liuziruiliu738-cloud.github.io/. It uses Liquid templating, SCSS, and a large set of Jekyll plugins.

## Development Commands

### Local Development (Docker — recommended)
```bash
docker compose pull
docker compose up
# Site available at http://localhost:8080 with live reload
```

### Lightweight Docker alternative
```bash
docker compose -f docker-compose-slim.yml up
```

### Manual (Ruby)
```bash
bundle install
bundle exec jekyll serve
```

### Production Build & Deploy
```bash
# Deploy to gh-pages branch
./bin/deploy

# Manual production build with CSS purging
export JEKYLL_ENV=production
bundle exec jekyll build
purgecss -c purgecss.config.js
```

### Code Formatting
```bash
npx prettier --write .
```

## Architecture

### Content Authoring
- **Pages**: `_pages/` — main site sections (about, blog, cv, publications, projects, teaching)
- **Blog posts**: `_posts/` — Markdown files with YAML front matter
- **Projects**: `_projects/` — portfolio items
- **News**: `_news/` — announcements shown on the home page
- **Books**: `_books/` — book collection

### Data & Configuration
- **`_config.yml`**: Master config — site identity, plugins, collections, theme color, analytics, Jekyll Scholar settings
- **`_data/cv.yml`**: CV content (education, experience, skills, etc.)
- **`_data/citations.yml`**: Auto-generated publication metadata (do not edit manually)
- **`_data/coauthors.yml`**: Co-author profile links
- **`_data/socials.yml`**: Social media links shown in the header/footer
- **`_data/repositories.yml`**: GitHub repos to display on the repositories page

### Publications System
Publications use Jekyll Scholar: add BibTeX entries to `_bibliography/papers.bib`. The `_layouts/bib.liquid` template (16KB) renders each publication with optional Altmetric/Dimensions badges, PDF links, and abstract toggles. The `bin/update_scholar_citations.py` script auto-fetches citation counts.

### Templates
- **`_layouts/`**: Page-level Liquid templates (about, post, cv, bib, distill, archive, etc.)
- **`_includes/`**: Reusable partials (header, footer, head, CV components, repository stats, pagination)
- **`_scripts/`**: JavaScript as Liquid templates (search, analytics, Giscus comments)

### Styling
- **`_sass/_variables.scss`**: Size/spacing variables
- **`_sass/_themes.scss`**: Light/dark mode color definitions
- **`_sass/_base.scss`**: Core styles (27KB)
- Theme color is set in `_config.yml` under `theme_color`

### CI/CD (`.github/workflows/`)
- **deploy.yml**: Auto-builds and deploys on push to `main`
- **prettier.yml**: Formatting validation
- **broken-links.yml**: Link validation (lychee)
- **update-citations.yml**: Refreshes citation metadata

## Key Customization Points

| What to change | Where |
|---|---|
| Profile info, bio, social links | `_pages/about.md` and `_data/socials.yml` |
| CV content | `_data/cv.yml` |
| Publications | `_bibliography/papers.bib` |
| Site name, URL, theme color | `_config.yml` |
| Navigation items | `_config.yml` → `navbar_pages` |
| Profile photo | `assets/img/` (filename set in `_pages/about.md`) |
