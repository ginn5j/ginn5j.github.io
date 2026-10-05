# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal Jekyll site for ginn5j.com, built on the remote theme `mmistakes/minimal-mistakes@4.28.0` (air skin). There is no local `_layouts`/`_includes`/`_sass`; all theme files come from the remote theme, so overriding one means copying it into the repo at the same path.

## Commands

```sh
bundle install
bundle exec jekyll serve      # local preview at http://localhost:4000
bundle exec jekyll build      # output to _site/ (gitignored)
```

`_config.yml` is not reloaded by `jekyll serve`; restart after editing it. There are no tests or linters.

Any file not starting with `_` or `.` is published as-is. Add new repo-only files (docs, tooling config) to `exclude:` in `_config.yml`.

Deployment: pushing to `main` triggers `.github/workflows/jekyll.yml`, which builds with Ruby 3.3 and `JEKYLL_ENV=production` and deploys to GitHub Pages.

## Content model

- **Posts** — `_posts/YYYY/MM/YYYY-MM-DD-slug.md`. Recent posts set an explicit `permalink: /blog/YYYY/MM/DD/slug/` and `type: post`; the global permalink (`/:categories/:title/`) only applies to older posts without one. Use `<!--more-->` with `excerpt_separator: <!--more-->` for excerpts. Images live under `assets/YYYY/MM/<post-slug>/`.
- **Books** — a `books` collection in `_books/YYYY/MM/YYYY-MM-DD-slug.md`, where the date is `date_finished`. Front matter: `title`, `author`, `series`, `series_number`, `rating` (1–5), `date_finished`, `genres` (list); body is a short review. `_pages/books.md` renders all books as a Liquid-driven table (rating labels/stars, genre filter) sorted by `date_finished`, so keep those field names stable.
- **Pages** — `_pages/` (included via `include:` in `_config.yml`). Top nav is `_data/navigation.yml`.
- **Templates** — `_templates/book.md` and `_templates/post.md` are Obsidian templates (the repo root is an Obsidian vault; `.obsidian/` config is committed, new notes default to `_posts`, attachments to `assets/2026`). They use Obsidian `{{date:...}}` syntax, not Liquid.

## Content arriving from outside this repo

Much of the commit history is automated; expect upstream changes on `main` and pull before pushing.

- `_pages/add-book.html` and `_pages/add-post.html` (`/add-book/`, `/add-post/`, `layout: none`, noindex) are standalone mobile forms that commit new files directly to `main` through the GitHub GraphQL API using a user-supplied PAT. They hardcode the repo and the `_books/YYYY/MM/...` / `_posts/...` path conventions — update them if those conventions change.
- `publish books` commits come from `github-actions[bot]` (an external workflow) adding files to `_books/`.
- `shows-96b39a3e.ics` (show-premiere calendar feed) is generated and committed by `github-actions[bot]`; don't hand-edit it.
- `album-club/` is a prebuilt Vite app deployed by `github-actions[bot]` from elsewhere; its hashed assets are build output, not source.

## Sass note

`quiet_deps: true` in `_config.yml` hides the theme's Dart Sass deprecation warnings. The two remaining `@import` warnings come from the theme's `assets/css/main.scss` and are left visible deliberately; switching to `@use` breaks the skin's colors (see the comment in `_config.yml`).
