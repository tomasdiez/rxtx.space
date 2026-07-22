# rxtx.space

RXTX — the experimental studio of Tomas Diez. Receive / transmit: essays in progress, sound, and experiments, made in Bali.

## Stack

- Jekyll, built natively by GitHub Pages. No custom Ruby, no remote theme.
- Whitelisted plugins only: `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-feed`.
- Hand-written layouts and one CSS file (`assets/css/main.css`). One tiny inline script (the footer clock). No frameworks, no analytics.

## Run locally

Requires Ruby and Bundler.

```sh
bundle install
bundle exec jekyll serve
# → http://localhost:4000
```

## Add a Transmission

Three ways, from least to most friction:

### 1. PagesCMS (browser / phone)

The repo has a `.pages.yml` schema. Open [app.pagescms.org](https://app.pagescms.org),
pick this repo, and use the **Transmissions** collection — filename
(`tx-NNN-slug.md`) is generated from the TX number and title. Check the log
for the latest TX number first; numbering is sequential.

### 2. `publish.py` from an Obsidian draft (Hermes / Claude Code / terminal)

Drafts live in `Obsidian/Hermes/Transmissions/drafts/`. One command validates
frontmatter, auto-assigns the next TX number (`tx: NEXT`), writes the file,
commits, and pushes:

```sh
python3 ~/websites/tools/publish.py transmission path/to/draft.md
# --dry-run to preview, --no-push to commit without pushing
```

### 3. By hand

One essay = one Markdown file in `_transmissions/`. Name it after the next number in the log, e.g. `tx-002-your-slug.md`:

```markdown
---
title: "Your title"
dek: "One line under the title, and in the log index."
description: "One sentence for search engines and link previews."
tx: "002"
date: 2026-08-01
---
Body in Markdown. Internal links: [text]({{ "/sound/" | relative_url }}).
```

Rules of the log:

- `tx` is a three-digit string (`"002"`, `"003"`, …), next in sequence. It also goes in the filename by convention.
- `date` in `YYYY-MM-DD`. The index sorts by it, newest first.
- Layout is applied automatically (`_config.yml` defaults). Nothing else to touch.
- The feed at `/transmissions.xml` picks it up on the next build. That is the URL to share for RSS.

## Add an Experiment

Append a block to `_data/experiments.yml` (newest first — the field reference is commented at the top of that file):

```yaml
- id: "EXP-003"
  title: "Name"
  status: "ongoing"   # live | ongoing | dormant | dead
  year: "2026"        # optional
  description: "What it is, in one to three sentences."
  link:               # optional
    url: "/sound/"    # internal starts with /, external with https://
    label: "Link text"
```

The grid on `/experiments/` renders it automatically, and the two "awaiting signal" placeholders renumber themselves.

## Structure

```
├── CNAME                  ← custom domain binding. Do not delete.
├── _config.yml            ← site config, collection + feed setup
├── _data/experiments.yml  ← experiments grid content
├── _includes/             ← header, footer
├── _layouts/              ← default, transmission
├── _transmissions/        ← one .md file per essay
├── assets/css/main.css    ← the whole design system
├── index.html             ← manifesto + doorways
├── transmissions.html     ← the log index
├── sound.html             ← narrative + Bandcamp/SoundCloud embeds
├── experiments.html       ← the bench
├── 404.html               ← no carrier
├── favicon.svg            ← transmit glyph
└── robots.txt
```

## Deploy

Push to the default branch; GitHub Pages builds and publishes (Settings → Pages → deploy from branch, root). The `CNAME` file binds `rxtx.space` — deleting it unbinds the live domain. Keep "Enforce HTTPS" on.
