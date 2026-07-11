# CLAUDE.md

Guidance for working in this repository.

## What this is

The Falster Lab website (https://danielfalster.com / falster lab, UNSW), a **Hugo** static site built with a **vendored** custom theme in `themes/hugo-material/`. It follows a blogdown-style workflow: `.Rmd` sources are ignored by Hugo (`ignoreFiles` in `config.toml`). Deployed via Netlify (`netlify.toml`, `content/CNAME`).

## Key paths

- `config.toml` — site config. **Nav menu** = `[[menu.main]]` blocks (ordered by `weight`); footer = `[[menu.footer]]`. `[params]` holds the banner background, custom CSS, contact details.
- `content/` — pages. Top-level: `_index.md` (home), `research.html`, `teaching.html`, `bio.md` (Bio & CV), `members.html`, `opportunities.md` (Join), `cornsters.md`, and `notebook/` (blog).
- `data/*.yml` — `members.yml`, `alumni.yml`, `collaborating.yml` drive the **Members page** via the `{{% members %}}` shortcode → `layouts/shortcodes/members.html` → `layouts/partials/member.html`. Add a person by editing the YAML, not HTML.
- `layouts/` — project overrides of the theme. Page layouts live in `layouts/page/`: `standard.html` (single column, honours a `pagewidth` front-matter param) and `vita.html` (the Bio & CV layout, with contact sidebar + CV download button). Home layout is `layouts/index.html`; home contact card is `layouts/partials/profile.html`.
- `static/img/` — images, served at `/img/...`. Headshots in `static/img/people/`, group photos in `static/img/lab/`.
- `static/files/` — documents.

## Common tasks

- **Add a page**: create a file in `content/` with front matter `type: page` + `layout: standard` (set `pagewidth: 11` for wide) and add a `[[menu.main]]` entry in `config.toml` (adjust `weight`s to position it). See `content/teaching.html` and `content/research.html` for the card-grid pattern; both are hand-written HTML.
- **Videos**: use the built-in `{{< youtube VIDEOID >}}` shortcode. `{{< iframe "url" w h >}}` (in `layouts/shortcodes/`) embeds arbitrary iframes; `{{< figure src="/img/..." >}}` for images.
- **CV PDF**: kept in **two** places that must stay in sync — `content/bio/Falster_CV.pdf` (served next to the Bio page; the download button links to it) and `static/files/Falster_CV.pdf`. Source of truth is the generated CV in the `7-career` folder.

## Preview & build

- Local preview: `hugo server -D` then open the printed URL.
- Production build: `hugo` (outputs to `public/`). A `warning-goldmark-raw-html` warning is expected and is already suppressed via `ignoreLogs` in `config.toml`.

## Conventions

- The PI's public title is **Associate Professor** — keep it unless told a promotion has been granted.
- Metrics (publications, citations, grants) are sourced from the career record in the `7-career` OneDrive folder; use the latest Google Scholar figures.
