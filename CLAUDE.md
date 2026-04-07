# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Local development server (live reload)
hugo server

# Production build (matches CI/CD)
hugo --minify --cleanDestinationDir --gc

# Initialize theme submodule (required after fresh clone)
git submodule update --init --recursive
```

## Architecture

This is a **Hugo static site** deployed to GitHub Pages via Actions (`.github/workflows/hugo.yml`). The theme (`terminal-theme`) is a git submodule at `themes/terminal-theme/` — always run `git submodule update --init --recursive` after cloning.

**Content**: 7 flat pages under `content/` (no blog, no taxonomy). Navigation order is controlled by `weight` in the theme's `config.toml` menu config, not in individual page frontmatter.

**Theme customization**: The theme's default dark aesthetic is overridden by `/static/terminal.css`, which redefines CSS variables for a light mode (white background). Avoid editing theme files directly; use `/static/terminal.css` for visual overrides.

**Configuration split**:
- `hugo.toml` — minimal: baseURL, title, theme name only
- `themes/terminal-theme/config.toml` — navigation menu, layout params (`centerTheme=true`), markdown renderer settings (unsafe HTML enabled)

**Data folder**: `/data/` contains reference files (markdown, PDFs) but is not consumed by any Hugo template — it's archival only.

**Deployment**: Pushes to `main` trigger a build and deploy to `gh-pages` branch via `PERSONAL_TOKEN` secret. The `public/` and `resources/` directories are generated artifacts and not committed.
