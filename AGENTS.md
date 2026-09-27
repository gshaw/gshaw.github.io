# Agent Notes

Background for AI agents working in this repo.

## What this is

The personal site of Gerry Shaw, live at [gshaw.ca](https://gshaw.ca). A Jekyll site
hosted on Cloudflare Pages (project `gshaw-ca`). It exists to introduce Gerry
and his apps to people, search engines, and AI agents.

**The repo and the site are both public.** Anything committed here is published. Keep
private notes, credentials, and personal context out of tracked files.

## Guiding principle

Keep it minimal. Prefer removing over adding. Don't introduce files, gems, plugins, build
steps, or config unless asked — a smaller site is the goal, not a more capable one.

There are currently no Jekyll plugins: `_config.yml` has no `plugins:` key and the
`Gemfile` carries only `jekyll`, `webrick`, and a few stdlib gems. Adding a plugin is a
real change to the project's shape; ask first.

## Commands

```sh
mise run install   # bundle install
mise run dev       # serve locally on :4001 with livereload
mise run check     # build + spell + markdownlint + internal links
mise run verify    # curl the live site after a deploy
mise run deploy    # check, then git push
```

**Read the counts, not just the exit code.** html-proofer prints `Ran on N files` and cspell
prints `Files checked: N`. A green run over zero files checked nothing.

The check tools (cspell, markdownlint-cli2, html-proofer) are pinned in `.mise.toml`, not
the `Gemfile`, so the site's own dependencies stay at `jekyll` and `webrick`.

## Deploys

Cloudflare Pages builds every push: `main` goes to production, other branches get a
preview URL. The build runs `bundle exec jekyll build` on build image v3 with
`RUBY_VERSION` set in the Cloudflare project, so a Ruby bump means changing `Gemfile`,
`.mise.toml` and that variable together. GitHub Actions runs `mise run -c check` on pushes
and PRs; it doesn't block Cloudflare.

Suppress a check inline, with a reason, in the file that provoked it
(`<!-- cspell:ignore word -->`). Move a word to `cspell.config.yaml` only once a second file
needs it.

## Layout

- `index.md` — homepage. Apps come from `_data/apps.yml`; the "Other Stuff" cards come
  from the `links:` list in the page's own front matter.
- `books.md` → `/books/`, driven by `_data/books.yml` (hand-curated favorites, each with
  a Goodreads `id` used for both the cover image and the outbound link).
  `_data/goodreads.yml` is a separate generated export of the full reading history.
- `recipes.md` → `/recipes/`, which auto-lists every page with `layout: recipe`. New
  recipes appear automatically; there is no index to update.
- `recipes/*.md` — one file per recipe, plus their images. See "Adding a recipe" below.
- `resume.md`, `articles.md`, `404.md`, `feed.xml` (hand-written Atom feed).
- `littlefaker/` holds Little Faker's landing, privacy and support pages (its own layout).
  `landnav/` and `idefibrillate/` are redirects to the apps' own sites. `aedsim/`,
  `birdsnearme/`, `qr/` and `onnav/` hold only images used elsewhere.
- `_layouts/` and `_includes/` (`head`, `footer`, `analytics`). `head.html` builds the
  description, canonical and Open Graph tags from `description`/`summary`, `ogimage` or a
  recipe's non-placeholder picture, falling back to `_config.yml`.
- `_site/` is build output and is gitignored.

Markdown is kramdown with GFM input. Permalinks are `pretty`.

## Adding a recipe

Create one file in `recipes/`. Nothing else needs editing — `recipes.md` builds the index
by scanning for every page with `layout: recipe`, so a new file appears on `/recipes/`
automatically.

```markdown
---
layout: recipe
title: Quick-Glazed Carrots
summary: Tender carrots simmered until glossy, then finished with lemon and herbs.
tags:
  - side
  - vegetarian
takes: 25 minutes
makes: 4 servings
picture:
  title: Pottery by Jesse Weise
  filename: pottery.jpg
  placeholder: true
---

### Ingredients

- 1 lb carrots, cut into coins or sticks
- 1 tablespoon extra-virgin olive oil

### Steps

1. Put the carrots and oil in a small saucepan with the liquid and bring to a boil.

2. Cover, lower the heat, and simmer until tender.

### Variations

- Orange and Ginger: add grated fresh ginger at the start and use orange juice as the liquid.

Source: [How to Cook Everything, Mark Bittman](https://www.goodreads.com/book/show/202814)
```

Field notes:

- `layout: recipe` is what puts the recipe on the index. Without it the page is invisible there.
- `takes` and `makes` are free text, rendered as-is in the row beneath the title alongside
  the tags. Nothing parses them.
- `picture.filename` is an image in `recipes/`; `picture.title` is its alt text and photo
  credit. `placeholder: true` hides the large image on the recipe page but the image is
  *still* used for the index card — that's how a generic stock photo works without looking
  like a real photo of the finished dish.
- `### Variations` and the trailing `Source:` line are conventions across the existing
  recipes, not requirements.

### Recipe checklists

`_layouts/recipe.html` runs a script that converts the lists under the `### Ingredients`
and `### Steps` headings into tappable checklists, for cooking from a phone. It matches
those two heading texts exactly. Renaming or re-leveling them silently disables the
feature, with no build error.

## Deliberate decisions — don't "fix" these

Each of these looks like an oversight and isn't. Leave them alone unless asked directly.

- **No `robots.txt`.** A missing robots.txt already means unrestricted crawling, so an
  allow-all file would add nothing. The site is intentionally open to search and AI crawlers.
- **No `sitemap.xml`.** At roughly 30 well-linked pages, a sitemap adds no discoverability
  and would be one more thing to keep in sync.
- **`/articles/` is not linked from the homepage, and its two posts are placeholders.**
  The section is a work in progress and is deliberately left unlinked until there's real
  writing to show. Don't link it from the homepage, delete the placeholder posts, or
  otherwise tidy the section.
