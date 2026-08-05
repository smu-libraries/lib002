# LIB002 website handover

Last updated: 5 August 2026 (Asia/Singapore)

The site is live at <https://smu-libraries.github.io/lib002/> and is in a finished state. Everything the earlier handover listed as outstanding has been dealt with. What follows is orientation for whoever picks it up next, not a to-do list.

## What the site is

Five module pages fronting eleven H5P Interactive Books, plus a homepage, About, Support and a 404. Quarto builds it; GitHub Actions deploys it on every push to `main`.

| Module | Page | Books |
|---|---|---|
| 1 | `modules/library-services.qmd` | 1 |
| 2 | `modules/literature-review.qmd` | 3 |
| 3 | `modules/working-with-data.qmd` | 5 |
| 4 | `modules/research-data-management.qmd` | 1 |
| 5 | `modules/publishing-impact.qmd` | 1 |

Eleven books, eleven fallback links. Read `AGENTS.md` before changing a module page: it carries the page contract, the multi-book pattern and the rule about where the H5P resizer script goes and why.

## Brand

Colours, typefaces and the lockup follow the SMU identity. SMU Blue `#141C52`, SMU Gold `#8A704C`, Slate Blue `#C5CADF` for lines only, Light Slate `#DDE0ED` for quiet fills, white ground, black body text. Anything else in the stylesheet is a tint of one of those.

Oswald sets headings and Open Sans sets body copy, which is SMU's guidance for digital work. Both are self-hosted as subset WOFF2 in `assets/fonts/web/`, with their SIL Open Font Licence text alongside them, which the licence requires wherever the font files are served. The Bootswatch theme's Google Fonts import is switched off, so the pages make no third-party requests of their own.

`assets/logo/` holds the two web-sized lockups. The print masters they came from are gitignored — they are around 240 megapixels each and belong in the Library's asset store, not in Git.

## Running it

Quarto is on the system PATH. From the repository root:

```powershell
quarto preview
```

Reloads on save; `Ctrl + C` to stop. Use `quarto render` only to inspect the built output — a running preview holds `_site` and a concurrent render fails with a file-in-use error. If a build misbehaves, delete `_site` and `.quarto`; both are generated and gitignored.

## Things worth knowing before changing layout

These were expensive to find and are easy to trip over again.

- **Quarto promotes a leading level-one heading into the title block** when the front matter has no `title`, even when the heading is raw HTML and even wrapped in a div. The homepage therefore sets a `title` and hides the generated title block, keeping its own `h1` inside `.lib-hero` so the tinted band can be sized by its contents.
- **`description` renders visibly as well as into the meta tag.** Use `description-meta`.
- **The article layout caps content at 799px** and reserves margin columns this site does not use. The project runs `page-layout: full` and sets one shared content width in the stylesheet instead, keyed on `.page-lead`, which every page except the homepage and 404 carries.
- **Full-bleed via `calc(50% - 50vw)` overshoots by half a scrollbar**, because `100vw` counts it and the visible area does not. It is clipped on `.quarto-container`; clipping on `html` does not work, as overflow on the root propagates to the viewport.
- **Pandoc treats a bare `<hr>` as an unclosed raw HTML block**, which stops the following `:::` fences being recognised. Write `<hr />`.

## Optional, not outstanding

- **A privacy line.** The site sets no cookies and has no analytics, but the embedded books are served from `smu.h5p.com`, which sets seven — a session cookie and CloudFront signing cookies, functional rather than tracking. Nothing on the public site identifies an individual. A sentence on About saying so was drafted and not adopted; add it if SMU policy wants one.
- **Usage statistics.** None are collected. H5P.com's own dashboard is the cheapest place to look for per-book engagement, since it needs nothing added here. For site-level visitor numbers, the least troublesome route is whatever SMU already uses institutionally. Google Analytics would undo the no-third-party-requests position and would then need a cookie notice.
- **A custom domain.** `_quarto.yml` sets `site-url` to the GitHub Pages address; change it if a domain is adopted. Requires DNS from SMU IT.
- **Workflow action versions** are each one major behind current. They work; bump when convenient.
