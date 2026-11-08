# AGENTS

Guidance for AI coding agents working in this repository.

## What this is

A small [Hugo](https://gohugo.io/) static site: the landing page served at
[summittdweller.com](https://summittdweller.com/). It is purely navigational —
a set of panels linking to the owner's other sites and services.

## Deployment — read before pushing

**Every push to `main` triggers an automatic deployment.** DigitalOcean App
Platform is connected to this GitHub repo; it clones (with submodules), builds
the site with its Hugo buildpack, and publishes to summittdweller.com. Do not
push unverified changes.

- `baseURL` is intentionally commented out in `config.toml` (App Platform
  serves from its own assigned URL). Do not re-enable it.
- The legacy Docker/Traefik/Watchtower deployment is retired; its artifacts
  live in `.out-of-the-way/` for reference only.

## Layout

- `config.toml` — site config, params, search engines. The author name lives
  under `[params.author]`.
- `data/links/*` — the link panels rendered on the home page. Add/edit entries
  here to change the navigation cards.
- `layouts/index.html` — home page template (project override). Contains the
  "Site Analytics" placeholder panel with wiring instructions for the
  SummittDweller-Google-Analytics report.
- `layouts/partials/` — project-level overrides of theme partials:
  - `head.html` — includes the Matomo tracking snippet.
  - `js.html` and `seo_schema.html` — modern-Hugo compatibility overrides
    (the theme targets an old Hugo; see below).
- `themes/bootstrap-bp-hugo-startpage` — the theme, a **git submodule**. Do
  not edit files inside it; override in the project `layouts/` tree instead.
- `.grip.yml` — marks this as a "reported repo" for the
  [GRIP](https://github.com/Digital-Grinnell/GRIP) inventory tool and carries
  its report metadata. Keep it valid YAML at the repo root.
- `public/` — committed build output; ignored by git going forward via
  `.gitignore`. App Platform builds fresh, so never hand-edit it.

## Building and verifying

```bash
hugo                      # production build into public/
hugo server               # local dev server
```

- Clone/update with submodules: `git submodule update --init`.
- The theme predates modern Hugo; removed features (`.Site.Author`,
  `.Site.RSSLink`, `_internal/google_analytics_async.html`) are patched via
  the project-level partial overrides noted above. If a new Hugo release
  breaks the build, prefer adding another override over editing the submodule.
- Verify a build locally before pushing (remember: push = deploy). For a
  styled local preview, pass a base URL, e.g.
  `hugo server` or `hugo -b http://localhost:1313/`.

## Conventions

- Keep changes minimal; this is a simple single-page site.
- Google Analytics: the modern internal template emits nothing until a GA4
  `G-XXXXXXXXXX` ID replaces the dead `UA-` value in `config.toml`. Matomo in
  `layouts/partials/head.html` is the active tracker for now.
- `HUMANS.md` documents the people behind the site; update it if authorship
  or credits change.
