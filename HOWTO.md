# HOWTO — run, test and deploy the site

## Prerequisites (one-time setup)

- Ruby (3.1+) and Bundler
- Install dependencies:

```sh
cd ~/working/NCRunners
bundle install
```

Gems are installed locally into `vendor/bundle` (see `.bundle/config`), so no
root access is needed.

## Test locally

Start the dev server:

```sh
bundle exec jekyll serve
```

Add `--livereload` if you want the browser to auto-refresh as you edit files.
Stop the server with `Ctrl-C`.

Then open <http://localhost:4000> and click through the pages:

- <http://localhost:4000/> — home
- <http://localhost:4000/ncrhdc/> — 100-Day Challenge
- <http://localhost:4000/ncrhdc_2025/> and <http://localhost:4000/ncrhdc_2026/> — finisher lists
- <http://localhost:4000/noSugar/> — No Sugar Challenge
- <http://localhost:4000/NC_LSOM_2025/> and <http://localhost:4000/NC_LSOM_2026/> — LSoM event pages
- <http://localhost:4000/History/> — how the community started

Things worth checking:

- Nav links scroll to the right sections on the home page.
- Tables look right in a phone-sized window (resize the browser narrow —
  wide tables should scroll horizontally, not break the layout).
- Toggle your OS dark mode to see both light and dark themes.

## Build only (no server)

```sh
bundle exec jekyll build
```

The generated site lands in `_site/`. This is what CI runs, so if it builds
cleanly here it will build cleanly on GitHub.

## Deploy to GitHub Pages

Deployment is automatic: every push to `main` triggers the workflow in
`.github/workflows/pages.yml`, which builds the site with Jekyll and publishes
it to GitHub Pages at <https://www.ncrunners.in>.

One-time repository setting (needed once, or deployment will not work):

> **Settings → Pages → Source → "GitHub Actions"** (instead of "Deploy from a
> branch"). The custom domain `www.ncrunners.in` setting stays as it is.

If a deployment fails, check the **Actions** tab on GitHub for the build log.

## Editing content

- `index.md` — home page (sessions, achievements, trainings, contact)
- `ncrhdc.md`, `ncrhdc_2025.md`, `ncrhdc_2026.md` — 100-Day Challenge and finishers
- `NC_LSOM_2025.md`, `NC_LSOM_2026.md` — LSoM event pages
- `noSugar.md`, `History.md` — other pages
- `_layouts/default.html` — shared layout (header, nav, footer)
- `assets/css/style.css` — all styling

Each page's URL is set by the `permalink:` line in its front matter. To add a
new page, copy an existing one, change the title and permalink, and link to it
from `index.md`.
