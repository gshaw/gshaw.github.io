# Agent Notes

Background for AI agents working in this repo.

## What this is

The personal site of Gerry Shaw, live at [gshaw.ca](https://gshaw.ca). A Hugo site
hosted on Cloudflare Pages (project `gshaw-ca`). It exists to introduce Gerry
and his apps to people, search engines, and AI agents.

**The repo and the site are both public.** Anything committed here is published. Keep
private notes, credentials, and personal context out of tracked files.

## Guiding principle

Keep it minimal. Prefer removing over adding. Don't introduce files, themes, Hugo modules,
build steps, or config unless asked — a smaller site is the goal, not a more capable one.

There is no theme and no Hugo module: every template is in `layouts/`. Adding either is a
real change to the project's shape; ask first.

## Commands

```sh
mise run dev       # hugo server on :4001 with live reload
mise run check     # build + spell + markdownlint + internal links
mise run deploy    # guard, check, push, wait for Pages, verify
mise run verify    # curl the live site
mise run deploy-status  # is main live?
```

**Read the counts, not just the exit code.** lychee prints `N OK` and cspell prints
`Files checked: N`. A green run over zero files checked nothing.

Hugo and the check tools (cspell, markdownlint-cli2, lychee) are pinned in `.mise.toml`.
The build runs with `--panicOnWarning`, so a deprecation warning fails it rather than
scrolling past.

## Deploys

Cloudflare Pages builds every push: `main` goes to production, other branches get a
preview URL. The build runs `hugo` on build image v3 with `HUGO_VERSION` set in the
Cloudflare project, for production and preview. A Hugo bump means changing `.mise.toml`
and that variable together.

**Deploy with `mise run deploy`**, never a bare `git push` to `main`.
`scripts/deploy-guard.sh` refuses unless the branch is `main`, the tree is clean and
`origin/main` isn't ahead. Then it runs `check`, pushes, waits for the "Cloudflare Pages"
check run on the commit (`scripts/pages-status.sh --wait`) and runs `verify`. A merged PR
also deploys, since Pages builds every push to `main`. The rule and the list of sites are
in [Workshop's deploy note](https://github.com/gshaw/Workshop/blob/main/Tooling/deploy.md).

GitHub Actions runs `mise run -c check` on pushes and PRs; it doesn't block Cloudflare.

Suppress a check inline, with a reason, in the file that provoked it
(`<!-- cspell:ignore word -->`). Move a word to `cspell.config.yaml` only once a second file
needs it.

## Layout

- `content/_index.md` — homepage. `{{< cards apps >}}` lists `data/apps.yml`;
  `{{< cards links >}}` lists the `links:` in the page's own front matter.
- `content/books.md` → `/books/`. `{{< books >}}` lists `data/books.yml`
  (hand-curated favorites, each with a Goodreads `id` used for both the cover image in
  `static/books/` and the outbound link), newest `date` first.
  `data/goodreads.yml` is a separate generated export of the full reading history.
- `content/recipes/` — one file per recipe. `/recipes/` lists every file there; there is
  no index to update. Photos are in `static/recipes/`. See "Adding a recipe" below.
- `content/resume.md`, `content/articles/` (posts at `/articles/<file name>/`).
- `content/littlefaker/` holds Little Faker's landing, privacy and support pages, with
  their own layout (`layouts/littlefaker/all.html`).
- `static/` is published as it is: CSS, icons, book covers, recipe photos, and the images
  in `aedsim/`, `birdsnearme/`, `qr/` and `onnav/` used elsewhere. `static/_redirects` sends
  `/landnav/` and `/idefibrillate/` to the apps' own sites with a 301.
- `layouts/`: `baseof.html` is the page shell; `_partials/head.html` builds the
  description, canonical and Open Graph tags from `description`/`summary`, `ogimage` or a
  recipe's non-placeholder picture, falling back to `hugo.toml`. `home.atom.xml` is the
  Atom feed at `/feed.xml`; `404.html` the not-found page.
- `public/` is build output and `resources/` Hugo's image cache; both are gitignored.

Hugo doesn't run template code inside Markdown files: a loop over data goes in a
shortcode in `layouts/_shortcodes/`, called from the page.

### Hugo gotchas

Each of these cost time on 2026-10-01, the day the site moved to Hugo.

- **`sort` skips silently on a nil value.** One book without a `date:` left the whole list
  unsorted, with no error. `books.html` sorts the dated books and appends the rest.
- **An empty `define` doesn't override a block.** `{{ define "header" }}{{ end }}`
  is ignored and the default renders. Put a comment in it.
- **Raw HTML ends at a blank line.** A blank line inside a `<div>` in Markdown wraps what
  follows in a `<p>`. Keep raw HTML blocks free of blank lines.
- **A link with spaces needs angle brackets**: `[text](<mailto:x?subject=A B>)`.

## Adding a recipe

Create one file in `content/recipes/`. Nothing else needs editing: `/recipes/` lists every
file in that folder.

```markdown
---
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

- `takes` and `makes` are free text, rendered as-is in the line beneath the title alongside
  the tags. Nothing parses them.
- `picture.filename` is an image in `static/recipes/`; `picture.title` is its alt text and
  caption. The layouts resize it to WebP. `placeholder: true` means there's no real photo
  of the dish yet: the recipe page, its index card and its `og:image` all skip the picture.
- `### Variations` and the trailing `Source:` line are conventions across the existing
  recipes, not requirements.

### Recipe checklists

`layouts/recipes/page.html` runs a script that turns the lists under the `### Ingredients`
and `### Steps` headings into tappable checklists, for cooking from a phone. It matches
the headings' ids, `ingredients` and `steps`, so renaming them silently disables the
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
