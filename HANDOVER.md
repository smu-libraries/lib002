# LIB002 website handover

Last updated: 4 August 2026 (Asia/Singapore)

## Current state

Working branch: `codex/quarto-skeleton`. Check `git status` and the remote before making changes.

The site renders cleanly (9/9 pages, no Quarto warnings) and all five modules now carry their real H5P books.

### Books embedded

| Module | Page | Books |
|---|---|---|
| 1 | `modules/library-services.qmd` | 1 |
| 2 | `modules/literature-review.qmd` | 3 |
| 3 | `modules/working-with-data.qmd` | 5 |
| 4 | `modules/research-data-management.qmd` | 1 |
| 5 | `modules/publishing-impact.qmd` | 1 |

Eleven books, eleven fallback links. Every embed URL was checked for framing headers before use. See `AGENTS.md` for the multi-book page contract and the rule about where the H5P resizer script must go.

### Brand

Colours, typography and the logo follow the SMU identity. SMU Blue `#141C52`, SMU Gold `#8A704C`, Slate Blue `#C5CADF`, Light Slate `#DDE0ED`, white background, black body text. Secondary text uses a tint of SMU Blue rather than a new hue.

Typefaces follow SMU's guidance for digital applications: Oswald for headings, Open Sans for body. Both are self-hosted as subset WOFF2 in `assets/fonts/web/`. The Bootswatch theme's Google Fonts import is disabled, so the site makes no third-party requests other than the H5P embeds themselves.

Logo derivatives live in `assets/logo/`. The print masters they came from are gitignored; keep them in the Library's own asset store.

## Not yet done

### Needs a decision or an answer from the project owner

- **Institutional details.** The About page no longer carries a placeholder box asking for them, but the ownership statement, a named accessibility contact and a review date are still not on the site.
- **Custom domain.** `_quarto.yml` sets `site-url` to `https://smu-libraries.github.io/lib002/`. Change it if a custom domain is adopted.
- **Analytics.** None configured. Nothing is currently tracked.
- **Homepage design.** The hero uses two side-by-side calls to action, a floating shadowed card and a gold accent rule. These read as a product landing page rather than a Library resource and are the main outstanding design question.
- **Book title spelling.** Module 2 book 3 is "Organizing Your References" (American -z) against British spelling elsewhere on the site. Module 3 book 3 is "Data Pre-processing & Cleaning" in H5P but "and" on the site. Align whichever way is preferred.

### Needs doing

- **Font licences.** Oswald and Open Sans are SIL Open Font License. The licence text must accompany redistribution, and serving the WOFF2 files publicly counts. The SMU font packs did not include `OFL.txt`. Add the licence files to `assets/fonts/web/`.
- **Module 3 load check.** Five H5P runtimes on one page is the heaviest thing on the site, roughly 97 requests per book. Try it on a mid-range phone. If it drags, switch that page from stacked books to loading each on demand; `AGENTS.md` records the threshold.
- **Lazy-loading check.** Books after the first are marked `loading="lazy"`. This could not be verified in the preview browser, which reports `visibilityState: hidden` and never evaluates viewport intersection, so every frame loads regardless. Confirm in a real window with the network panel open.

## Running the site

Quarto is installed and on the system PATH. From the repository root:

```powershell
quarto preview
```

Starts a local server that reloads on save. `Ctrl + C` to stop. Use `quarto render` only to produce `_site/` for inspection; a running preview holds `_site` and will make a concurrent render fail. If a build behaves strangely, delete `_site` and `.quarto` and try again — both are generated and gitignored.

## Publishing

`.github/workflows/publish.yml` renders and deploys on every push to `main`, and can be run manually from the Actions tab. GitHub Pages must be set to build from GitHub Actions under **Settings → Pages → Build and deployment → Source**.

The public URL is determined by the organisation and repository name, so it is `https://smu-libraries.github.io/lib002/` unless the repository is renamed or a custom domain is configured.
