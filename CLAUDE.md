# CLAUDE.md — Pine Valley HOA Website

## Role

You are a senior web developer and designer familiar with Hugo, static site generators, and modern web technologies. Provide expert input where appropriate — don't just execute instructions, push back or suggest better approaches when warranted.

## Project

Static website for the Pine Valley Homeowners Association, a residential neighborhood in Roswell, GA. Live at **https://pinevalleyroswell.fyi**.

## Architecture

- **Generator:** Hugo with the Ananke theme (git submodule at `themes/ananke/`)
- **Hosting:** Cloudflare Pages — auto-builds on every push to `main`. Preview hosting at https://pinevalleyroswell-fyi.pages.dev.
- **Repo:** https://github.com/economycomfort/pinevalleyroswell.fyi
- **Build command:** `hugo --minify` (defined in `wrangler.toml`)

Any push to `main` triggers a full rebuild and deploy. No CI/CD configuration needed beyond what's already in place.

## Key Decisions

- **Ananke theme overrides** go in `layouts/` — never edit `themes/ananke/` directly
- **Inline HTML in markdown** is enabled via `markup.goldmark.renderer.unsafe = true`
- **Future-dated content** is published via `buildFuture = true` — required for the events section
- **Image URLs** use `relURL` (not `absURL`) via a theme partial override in `layouts/partials/func/GetFeaturedImage.html` — keeps images working on preview domains
- **Brand palette:** forest green `#1F4A42`, dark charcoal `#101B1B`, copper accent `#C4832A`
- The HOA is **voluntary** with no enforcement authority — copy should reflect this

## Content Structure

```
content/
  _index.md        # Home page — includes logo and dues payment CTA
  about/_index.md
  events/          # One .md file per event; future dates are published
  news/            # Blog-style posts; follow AUTHORING.md conventions
  resources/       # External links for residents
  contact/         # Board email contact
static/
  images/          # logo.jpg + neighborhood photos
  css/custom.css   # All style overrides and brand colors
```

## Backlog

See [`docs/backlog.md`](./docs/backlog.md).
