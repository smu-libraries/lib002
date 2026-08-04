# AGENTS.md

## Purpose

This repository contains the public Quarto website for **LIB002: Graduate Research Essentials**, developed by SMU Libraries. The website orients visitors and embeds five externally hosted H5P Interactive Books. It must not duplicate the books or become a general-purpose course platform.

These instructions apply to the whole repository.

## Product principles

- Keep the experience modern, calm, scholarly, approachable and distinctly different from a conventional LibGuide or learning-management system.
- Let visitors explore modules in any order and return through stable direct links.
- Prefer clear language, restrained interaction and generous whitespace.
- Treat accessibility, responsive behaviour and keyboard use as acceptance criteria.
- Make the smallest coherent change that solves the requested problem; avoid new frameworks or build dependencies without a demonstrated need.

## Canonical structure

- `_quarto.yml`: global metadata, navigation, footer and HTML configuration.
- Root `.qmd` files: homepage and supporting pages.
- `modules/*.qmd`: one page per H5P book. Filenames are stable public URLs.
- `assets/styles.scss`: Bootstrap/Quarto variables first, custom rules after `/*-- scss:rules --*/`.
- `assets/images/`: approved visual assets with meaningful filenames.
- `includes/`: only genuinely shared HTML fragments.
- `.github/workflows/publish.yml`: GitHub Pages build and deployment.
- `README.md`: beginner-facing setup and maintenance documentation.

## Module-page contract

Every module page must include:

1. A unique page title and `description-meta`. Use `description-meta`, not `description`: the latter also renders as a visible line in the title block, which duplicates the page lead.
2. Its position stated as “Module N of 5”; this is orientation, not a completion requirement.
3. A concise introduction that does not repeat the book.
4. An H5P iframe with a descriptive `title` and an HTTPS embed URL.
5. A visible fallback link to the public H5P page, opening in a new tab.
6. Previous/next navigation or a route back to all modules.
7. A route to Library support through the global navigation/footer.

Do not insert a bare iframe without the fallback link. Do not assume iframe embedding works merely because the public H5P URL loads; verify the provider's embed URL and headers. The public H5P page sends `X-Frame-Options: SAMEORIGIN` and `frame-ancestors 'none'`, so only the `/embed` variant can be framed; the public URL is what the fallback link points at.

Keep the `allow` attribute narrow. The embed code H5P hands out grants autoplay, geolocation, microphone, camera and midi; an interactive book needs none of those, so use `allow="fullscreen"` unless a specific book demonstrably needs more.

### Modules with more than one book

Some modules are made up of several books. Those pages keep one URL and stack the books, and additionally need:

- a short “In this module” contents list naming every book, so the number of them is visible before scrolling;
- one `h2` per book, with a `Book N of M` label above it;
- a separate fallback link under each book.

Load `h5p-resizer.js` **once per page, before the first iframe**. It is an immediately-invoked script that, at the end, walks every h5p iframe already in the document and posts to its `contentWindow`; touching `contentWindow` instantiates the frame and defeats `loading="lazy"`. Placed before the iframes it sees none, and picks each book up instead from the `hello` message the iframe posts when it loads. One copy handles every iframe on the page — the embed code repeats the script tag, and those repeats should be dropped.

Give the first book eager loading and the rest `loading="lazy"`. Note that lazy behaviour cannot be observed in a non-rendering browser context: if the page is not being composited, `visibilityState` is `hidden`, viewport intersection is never evaluated and every frame loads regardless. Check deferral in a real browser window, not a headless or hidden one.

Each book costs roughly 97 requests and a full H5P runtime instance. Bandwidth is partly shared through the HTTP cache since all books come from the same origin, but script parsing and memory are per frame and are not. If a module grows past about five books, or the page becomes sluggish on a mid-range phone, move to loading each book on demand instead of stacking them.

## Accessibility and content checks

- Use one page-level `h1`; preserve a logical heading hierarchy.
- Use real links and buttons for interaction, not clickable generic containers.
- Provide alt text for informative images and empty alt text for decorative images.
- Keep visible focus styles and honour `prefers-reduced-motion`.
- Do not communicate meaning through colour alone.
- Avoid autoplaying media and unnecessary animation.
- Use descriptive link wording; avoid repeated “click here” links.
- Test at narrow mobile width and at 200% browser zoom.

## Working commands

Run from the repository root:

```powershell
quarto preview
quarto render
git status --short
```

Quarto alone is sufficient. Do not add R, Python, Node.js or a package manager unless future functionality actually requires it.

## Verification before handoff

1. Run `quarto render` successfully.
2. Check internal links and confirm every expected page exists under `_site/`.
3. Inspect the homepage and at least one module page at desktop and mobile widths.
4. Confirm placeholder text has not accidentally reached a release-bound change.
5. Review `git diff` and keep generated `_site/` files out of commits.

## Documentation discipline

Update `README.md` when setup, deployment or common editing steps change. Update this file when architecture or agent-wide constraints change. `CLAUDE.md` intentionally points here so that instructions do not drift between agent types.
