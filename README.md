# LIB002: Graduate Research Essentials

Public Quarto website for **LIB002: Graduate Research Essentials**, a self-paced learning resource developed by SMU Libraries for postgraduate researchers and research staff.

The site is the public front door to eleven separately hosted H5P Interactive Books across five modules. It provides orientation, stable module URLs, accessible embeds, fallback links and routes to further Library support without duplicating the learning content.

**Live at <https://smu-libraries.github.io/lib002/>**

## Project status

All five modules carry their real H5P books, and the site uses the SMU palette, the SMU digital typefaces and the SMU Libraries lockup. `HANDOVER.md` lists what is still outstanding — chiefly the font licence files, the homepage design, and the institutional details for the About page.

## Requirements

Install the current stable [Quarto CLI](https://quarto.org/docs/get-started/). This site does not require R, Python or Node.js.

```powershell
quarto --version
```

If Windows cannot find `quarto` straight after installing, restart the terminal so it picks up the updated `PATH`.

## Preview and build

Run from this directory:

```powershell
# Local preview that reloads on save. Ctrl+C to stop.
quarto preview
```

```powershell
# Produce the complete static site in _site/
quarto render
```

Use `preview` for everyday editing; it renders as you go. Reach for `render` only when you want to inspect the built output.

Two things to know:

- A running preview holds `_site`, so a concurrent `quarto render` will fail with a file-in-use error. Stop the preview first.
- If a build misbehaves, delete `_site` and `.quarto` and try again. Both are generated and gitignored.

## Where things live

- `_quarto.yml` — navigation, site metadata, footer, and the `resources` list that controls which assets are copied into the build.
- `index.qmd`, `about.qmd`, `support.qmd`, `404.qmd` — top-level pages.
- `modules/` — one stable page per module. Filenames are public URLs; do not rename them.
- `assets/styles.scss` — brand tokens first, then component rules.
- `assets/fonts/web/` — subset WOFF2 for Oswald and Open Sans, self-hosted.
- `assets/logo/` — the two web-sized lockups. The print masters are gitignored.
- `.github/workflows/publish.yml` — renders and deploys to GitHub Pages.
- `AGENTS.md` — the authoritative maintenance guide. Read it before changing module pages.

## Adding or replacing an H5P book

Use the provider's **embed URL** in the iframe and its plain **public URL** for the fallback link. They are not interchangeable: the public page sends `X-Frame-Options: SAMEORIGIN` and `frame-ancestors 'none'`, so only the `/embed` variant can be framed.

```html
<script src="https://smu.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<div class="h5p-frame">
<iframe
  src="H5P_EMBED_URL"
  title="Interactive book: MODULE_TITLE"
  allow="fullscreen"
  allowfullscreen>
</iframe>
</div>
```

```markdown
::: {.module-note}
If this interactive book does not load, [open MODULE_TITLE in a new window](H5P_PUBLIC_URL){target="_blank" rel="noopener"}.
:::
```

The embed code H5P hands out differs from this in ways that matter. Drop its repeated resizer script tags — one per page is enough. Drop its hardcoded `width` and `height`; the stylesheet and the resizer handle sizing. Narrow its `allow` list, which otherwise grants geolocation, microphone, camera and midi that an interactive book does not need.

The resizer script goes **before** the iframes, not after. `AGENTS.md` explains why, and covers the extra structure needed for modules that hold several books.

## Publishing

Every push to `main` renders and deploys the site; the workflow can also be started by hand from the Actions tab. GitHub Pages is already configured to build from GitHub Actions.

Update `website.site-url` in `_quarto.yml` if a custom domain is adopted.

## Editing principles

- Keep pages concise and orienting; do not reproduce the H5P books.
- Preserve module filenames — they are public URLs.
- Use `description-meta` rather than `description` in page front matter, or the text renders twice.
- Colours come from the SMU palette. Where a tone is needed that the palette does not define, tint an existing brand colour rather than introducing a new one.
- Check keyboard access, focus visibility, heading order and mobile layout before committing.
