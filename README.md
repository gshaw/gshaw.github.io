# Gerry's Personal Home Page

Jekyll site for Gerry's personal home page.

[Live Site](https://gshaw.ca)

## Build Instructions

```sh
brew install mise
mise install
mise run install
mise run dev
mise run deploy
```

Deploy with `mise run deploy`. It refuses unless you're on a clean `main` with nothing newer on GitHub, then checks, pushes, waits for Cloudflare Pages and runs `mise run verify`. `mise run deploy-status` says whether `main` is live. The rule is in [Workshop's deploy note](https://github.com/gshaw/Workshop/blob/main/Tooling/deploy.md).

`mise run check` runs the build, spell check, Markdown lint and internal link check.

## Powered By

- Domain Register: [Namecheap](https://www.namecheap.com)
- DNS: [Cloudflare DNS](https://www.cloudflare.com/dns/)
- Hosting: [Cloudflare Pages](https://pages.cloudflare.com)
- Build System: [Jekyll](https://jekyllrb.com)
- CSS: [Pico.css](https://picocss.com)
