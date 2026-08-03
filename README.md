# LIB002: Graduate Research Essentials

Public Quarto website for **LIB002: Graduate Research Essentials**, a self-paced learning resource developed by SMU Libraries for postgraduate researchers and research staff.

The site is the public front door to five separately hosted H5P Interactive Books. It provides orientation, stable module URLs, accessible embeds, fallback links and routes to further Library support without duplicating the learning content.

## Project status

The website skeleton is in place. H5P URLs, final module summaries, institutional links, branding assets and launch wording still need to be added and reviewed.

## Requirements

Install the current stable [Quarto CLI](https://quarto.org/docs/get-started/) for your operating system. This site does not require R, Python or Node.js.

Confirm the installation:

```powershell
quarto --version
```

If Windows cannot find `quarto` immediately after installation, restart the terminal or Codex desktop app so that it receives the updated `PATH`.

## Preview and build

Run these commands from this directory:

```powershell
# Start a local preview that refreshes when files change
quarto preview

# Produce the complete static site in _site/
quarto render
```

The generated `_site/` directory is intentionally ignored by Git. GitHub Actions produces it again during deployment.

## Where things live

- `_quarto.yml` controls navigation, site metadata and global output options.
- `index.qmd`, `about.qmd`, `support.qmd` and `404.qmd` are top-level pages.
- `modules/` contains one stable page for each H5P Interactive Book.
- `assets/styles.scss` contains theme variables and site-specific styles.
- `assets/images/` is reserved for approved images and branding assets.
- `.github/workflows/publish.yml` renders and deploys the site to GitHub Pages.
- `AGENTS.md` is the authoritative maintenance guide for coding agents.

## Adding an H5P book

Replace the `.h5p-placeholder` block on the relevant module page with this pattern:

```html
<div class="h5p-frame">
  <iframe
    src="H5P_EMBED_URL"
    title="Interactive book: MODULE_TITLE"
    loading="lazy"
    allowfullscreen>
  </iframe>
</div>

<p class="module-note">
  If the interactive book does not load,
  <a href="H5P_PUBLIC_URL" target="_blank" rel="noopener">
    open this module in a new window
  </a>.
</p>
```

Use the provider's **embed URL** in the iframe and its normal **public URL** for the fallback. Confirm that the H5P host permits cross-origin iframe embedding before launch.

## Publishing

The workflow publishes on every push to `main`, or when manually started from the repository's **Actions** tab. In GitHub, set **Settings → Pages → Build and deployment → Source** to **GitHub Actions**.

The configured project-site URL is:

<https://smu-libraries.github.io/lib002/>

Update `website.site-url` in `_quarto.yml` if a custom domain is adopted later.

## Editing principles

- Keep pages concise and orienting; do not reproduce the H5P books.
- Preserve descriptive module filenames because they are public URLs.
- Check keyboard access, focus visibility, heading order and mobile layout.
- Render the entire site before committing structural or styling changes.
- Replace all text marked “to be confirmed” before public launch.
