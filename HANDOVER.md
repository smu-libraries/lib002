# LIB002 website handover

Last updated: 3 August 2026 (Asia/Singapore)

## Current state

The initial Quarto website skeleton has been created on the working branch `codex/quarto-skeleton`. Check the latest Git status and remote branch state before making further changes.

The repository now contains:

- global Quarto configuration and navigation in `_quarto.yml`;
- a designed homepage in `index.qmd`;
- five directly linkable module pages under `modules/`;
- supporting About, Library Support and custom 404 pages;
- a responsive SCSS visual system in `assets/styles.scss`;
- a GitHub Pages deployment workflow in `.github/workflows/publish.yml`;
- beginner-facing setup notes in `README.md`;
- repository-wide coding-agent guidance in `AGENTS.md`;
- a short `CLAUDE.md` pointer to avoid duplicated agent instructions;
- placeholder directories for approved images and shared includes.

The first module uses the descriptive path:

`modules/library-services.qmd`

Its displayed title is **Introduction to Library Services**.

## Decisions already made

- The site is a Quarto static website, with no R, Python, Node.js or application framework dependency.
- H5P books remain externally hosted. Each module page will contain an iframe plus a visible fallback link.
- Visitors may enter the modules in any order. Previous/next links are conveniences, not prescribed progression.
- GitHub Actions will render `_site/` and publish it using GitHub Pages artifacts. A local `gh-pages` branch bootstrap is not required.
- `AGENTS.md` is the authoritative guide for future coding agents.
- Presentation files live under `assets/`; learning and orientation content remains in `.qmd` files.

## Checks completed

- All Markdown links to local `.qmd` pages resolve to real files.
- `git diff --check` passed.
- The SCSS file has balanced opening and closing braces.
- The GitHub Pages workflow follows the current Quarto/GitHub static-site deployment pattern.
- The repository has intentional, clearly labelled placeholders for H5P embeds and final institutional links.

## Not yet completed

### 1. Install and verify Quarto locally

Quarto was not installed or available on the command path of the company computer. Install the current stable Quarto CLI on the home computer; no optional R, Python or Node.js setup is needed for this project.

After installation, restart the terminal/Codex app if necessary and run:

```powershell
quarto --version
```

### 2. Render the site

From the repository root (`lib002/`), run:

```powershell
quarto render
```

Fix any Quarto, YAML, Markdown or SCSS errors before continuing. This is the first task for the next session because render-level validation has not yet been possible.

Then preview locally:

```powershell
quarto preview
```

Inspect at least:

- the homepage at desktop and narrow mobile widths;
- one representative module page;
- the Explore modules dropdown;
- the About, Support and 404 pages;
- keyboard focus states and 200% browser zoom.

### 3. Review draft wording and visual direction

The current summaries are sensible drafts based on the project brief, not approved final copy. Review the homepage hierarchy, module card descriptions, page introductions, colours, typography and spacing before adding the H5P books.

### 4. Add final information

Still needed from the project owner:

- five H5P embed URLs and five public fallback URLs;
- confirmed module summaries if the current drafts need changing;
- official SMU Libraries contact, consultation and website links;
- any required logo, brand colours, footer wording, privacy notice or accessibility statement;
- confirmation of the final public domain;
- analytics requirements, if any.

Search for `placeholder` and `to be confirmed` before launch.

### 5. Configure and publish GitHub Pages

After local review and an intentional commit/push, set the GitHub repository to:

**Settings → Pages → Build and deployment → Source → GitHub Actions**

The current project URL configured in `_quarto.yml` is:

`https://smu-libraries.github.io/lib002/`

Change `website.site-url` if an SMU custom domain will be used.

## Suggested prompt for the next Codex session

> Read `HANDOVER.md`, `AGENTS.md`, `README.md` and `_quarto.yml` completely. Continue the LIB002 Quarto website from the documented handover. First check whether Quarto is installed, run `quarto render`, fix any build errors, then preview and visually inspect the homepage and one module page. Do not add H5P URLs or invent institutional contact details unless I provide them.

## Continuing on another computer

The intended remote branch is `origin/codex/quarto-skeleton`. After the push has been confirmed, fetch and switch to it on the home computer:

```powershell
git fetch origin
git switch --track origin/codex/quarto-skeleton
```

If a local branch with that name already exists, use `git switch codex/quarto-skeleton` instead. Confirm the successful push in the originating Codex session before relying on the remote branch.
