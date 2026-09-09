# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal academic homepage of Yue Wang (王越), built with Jekyll using the [academicpages](https://github.com/academicpages/academicpages.github.io) theme (a fork of minimal-mistakes), deployed via GitHub Pages at https://keithyue.github.io. Deploy happens automatically on push to `master`; there is no build step to run manually for deployment.

## Commands

```bash
bundle install                                        # install Ruby deps (delete Gemfile.lock first if it errors)
bundle exec jekyll serve                              # build + serve at localhost:4000
bundle exec jekyll liveserve                          # serve with auto browser refresh (via hawkins gem)
bundle exec jekyll serve --config _config.yml,_config.dev.yml   # dev overrides (disables analytics, expands sass)
```

No tests or linters exist in this repo.

GitHub Pages builds with the `github-pages` gem, so only whitelisted plugins in `_config.yml` may be used.

## Architecture

### Where the real content lives (important)

The site owner's actual content is maintained in `_pages/`, primarily:

- `_pages/about.md` — bio page (the homepage)
- `_pages/publications.md` — **the real publication list, written inline as a numbered HTML/markdown list**, not via the `_publications/` collection
- `_pages/cv.md`, `_pages/talks.html`, `_pages/teaching.html` — other pages

The Jekyll collections (`_publications/`, `_talks/`, `_teaching/`, `_posts/`, `_portfolio/`, `_drafts/`) still contain **placeholder files from the original academicpages template** ("Paper Title Number 3", etc.). When adding a new paper, edit `_pages/publications.md` — do not add a file to `_publications/` unless deliberately migrating to the collection model.

### Publication list conventions (`_pages/publications.md`)

Grouped by section (e.g. "Conference Publications"), numbered list, one paper per entry:

- Own name in bold: `**Yue Wang**`
- Corresponding author marked with `**Yue Wang<sup>*</sup>**`
- Venue tag in backticks: `` `[VLDB'21]` ``
- Paper title in blue: `<font color="blue">Title</font>`
- Venue full name in italics on the following line

### Theme machinery (rarely needs changes)

- `_config.yml` — all site settings (author info, social links, collections, defaults, plugins)
- `_data/navigation.yml` — top navigation links
- `_layouts/`, `_includes/`, `_sass/` — minimal-mistakes templates
- `files/` — uploaded PDFs etc., served at `/files/<name>`
- `markdown_generator/` — Python scripts/notebooks to generate collection markdown from `publications.tsv` / BibTeX (unused so far)
- `talkmap.py` — regenerates the talks map page

Markdown is kramdown with GFM input; `future: true` (future-dated posts render); site timezone is America/Los_Angeles.
