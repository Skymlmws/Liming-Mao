# AI Coding Agent Instructions

## Project Overview

This is a **Jekyll-based academic personal homepage** using the Minimal Light theme. It's a static site generator project with:
- Content: Markdown files (`index.md`, `_includes/`) compiled to HTML
- Styling: SCSS files (`_sass/`) for light/dark mode support
- Data: YAML files (`_data/publications.yml`) providing structured content
- Layout: Liquid templates (`_layouts/homepage.html`) rendering pages

## Build & Deployment

**Build locally:**
```bash
bundle install
bundle add webrick
bundle exec jekyll server
```
Site runs at `http://localhost:4000` with HTML output in `_site/` folder.

**Deployment:** GitHub Pages (auto-compiled from source, or manual HTML uploads to `html_source_file/`).

## Key Files & Patterns

### Content Structure
- **`_config.yml`** - Site configuration (title, author, links, theme settings)
- **`index.md`** - Homepage content in Markdown with YAML front matter (`layout: homepage`)
- **`_data/publications.yml`** - Structured publication list (title, authors, conference, links, images)
- **`_includes/publications.md`** - Liquid template that iterates `site.data.publications.main` to render publications
- **`_includes/services.md`** - Services/activities section (similar pattern)

### Styling
- **`_sass/minimal-light.scss`** - Main styles with dark mode support
- **`_sass/minimal-light-no-dark-mode.scss`** - Dark mode disabled variant
- **`assets/css/publications.css`** - Publication styling (compiled from SCSS)
- **`assets/css/style.scss`** - Core styles

**Font selection:** Controlled via `_config.yml` `font` field (Serif/Sans Serif switches CSS files).

### Template Pattern
All pages use Liquid template syntax:
```liquid
{% for link in site.data.publications.main %}
  {{ link.title }}
  {{ link.authors }}
{% endfor %}
```

## Essential Workflows

1. **Add/Update Content:**
   - Edit `index.md` for main content
   - Add publications to `_data/publications.yml` (fields: title, authors, conference_short, conference, pdf, code, bibtex, image, notes)
   - Run local Jekyll server to preview

2. **Modify Styling:**
   - Edit `_sass/minimal-light.scss` and commit
   - Jekyll auto-compiles to CSS on build
   - Test both light/dark modes (`auto_dark_mode: true/false` in `_config.yml`)

3. **Update Site Config:**
   - Edit `_config.yml` for metadata, links, theme toggles
   - Changes apply to all pages automatically (Liquid variables: `{{ site.title }}`, `{{ site.google_scholar }}`, etc.)

## Important Conventions

- **Front matter required:** All Markdown pages need `layout: homepage` or appropriate layout
- **Asset paths:** Use relative paths (`./assets/img/`, `./assets/files/`) for GitHub Pages compatibility
- **Dark mode:** Site supports automatic dark mode; test with both variants when styling
- **Localization:** README exists in multiple languages (README.md, README_zh_Hans.md, README_de.md, README_zh_Hant.md) but content site is English-focused

## External Dependencies

- **Ruby/Bundler:** Required for local Jekyll builds
- **Jekyll ~3.8.5:** Static site generator
- **CDN assets:** Font Awesome (6.4.2), Academic Icons (1.8.6), webrick (1.8)
- **Theme base:** `yaoyao-liu/minimal-light` (remote theme, customizable)

## Common Tasks & Patterns

| Task | File | Pattern |
|------|------|---------|
| Add news item | `index.md` | Add to `## News` section with date format `[Date]` |
| Add publication | `_data/publications.yml` | Add entry under `main:` with all fields; include image path |
| Change site title | `_config.yml` | Update `title:` field |
| Add social link | `_config.yml` | Add new field like `github_link:` or `twitter_link:` (uses template vars) |
| Enable/disable dark mode | `_config.yml` | Toggle `auto_dark_mode: true/false` |

## Git Workflow

- Source code: Main branch (Markdown, SCSS, YAML)
- Compiled output: `html_source_file/` (optional backup, usually not committed if GitHub Pages handles build)
- `.gitignore`: Excludes Gemfile.lock, `_site/`, and build artifacts

