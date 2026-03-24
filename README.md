# Pine Valley HOA Website

Source code for [pinevalleyroswell.fyi](https://pinevalleyroswell.fyi) — the website for the Pine Valley Homeowners Association in Roswell, GA.

---

## Hosting Architecture

```
GitHub (this repo)
    └── push to main
          └── Cloudflare Pages (auto-build)
                └── Hugo generates static HTML
                      └── Served at pinevalleyroswell.fyi
```

**GitHub** holds all the source files — content, configuration, images, and theme. It is the single source of truth for the site.

**Cloudflare Pages** watches this repository. Any push to the `main` branch automatically triggers a new build. Hugo runs, generates the static site, and Cloudflare deploys it globally within about 60 seconds. There is no server to manage or maintain.

**Hugo** is a static site generator. It reads the markdown content files and Hugo configuration, applies the [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) theme, and outputs plain HTML/CSS. The result is fast, secure, and cheap to host.

---

## Repository Structure

```
content/          # All site content (markdown files)
  _index.md       # Home page
  about/          # About page
  events/         # Events — one .md file per event
  news/           # News posts — one .md file per post
  resources/      # Resources & links page
  contact/        # Contact page
static/
  images/         # Photos and logo
  css/
    custom.css    # Brand colors and site-specific styles
hugo.toml         # Site configuration, navigation, social links
themes/ananke/    # Theme (git submodule — do not edit)
wrangler.toml     # Cloudflare Pages build configuration
```

---

## Making Changes

### Adding a news post

See [AUTHORING.md](./AUTHORING.md) for step-by-step instructions. The short version: create a new `.md` file in `content/news/` and push to `main`.

### Adding an event

Create a new file in `content/events/`, following the same format as `content/events/2026-spring-fling.md`. Include the date, time, location, and a link to the SignUpGenius (or other) signup page.

### Editing page content

All pages are markdown files in `content/`. Open the relevant file, make your changes, and commit. No special tools required — GitHub's built-in editor works fine for simple text changes.

### Updating site configuration

Navigation, social links, and global settings live in `hugo.toml`. Styling overrides are in `static/css/custom.css`.

---

## Local Development

Requires [Hugo](https://gohugo.io/installation/) (extended edition recommended).

```bash
# Clone the repo (includes the Ananke theme submodule)
git clone --recurse-submodules git@github.com:economycomfort/pinevalleyroswell.fyi.git

# Start the local dev server
hugo server

# Visit the site
open http://localhost:1313
```

Changes to content or CSS hot-reload automatically in the browser.

---

## Contributing

Technically inclined neighbors are welcome to open a pull request. For questions or access, contact the board at [pvhoaroswell@gmail.com](mailto:pvhoaroswell@gmail.com).
