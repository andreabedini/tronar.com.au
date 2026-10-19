# Tronar Red Angus

## Preview your changes

From this project folder, with Zola 0.23.4 installed:

```sh
zola serve
```

Open the local address printed by Zola. Changes to content and templates rebuild automatically.
If you use mise, the included `mise.toml` selects the tested version; use `mise exec -- zola serve`.

## Edit a page or add a journal post

Edit the Markdown files in `content/`. The home page is `content/_index.md`.
Contact details are in the `[extra]` section of `config.toml` (Zola's site settings must be TOML). Everything else is YAML: each page starts with YAML front matter between `---` lines.

For a new journal post, create `content/blog/your-story.md`:

```yaml
---
title: Your story
date: 2026-10-19
path: your-story
extra:
  award: false
  image: /images/photographs/new-photo.jpg
---

Write your story here in Markdown.
```

Copy the photo into `static/images/photographs/`. The post appears automatically in the farm journal. Set `award: true` for show results; the post then carries a purple “Show award” tag. Keep each `path` unique. Keep existing `path` values to preserve the old website URLs.

Add `draft: true` to keep a post off the website while it is being checked. Preview drafts with `zola serve --drafts`; delete the `draft` line to publish.

On the home page, `featured` chooses the three featured stories and `story_links` lists the pages linked beside the farm's story. Gallery entries are in `data/photographs.yaml`:

```yaml
- title: Cattle on the farm
  src: /images/photographs/new-photo.jpg
```

Farm photos are in `static/images/photographs/`, logos and the favicon are in `static/images/branding/`, the self-hosted fonts (Archivo and Literata) are in `static/fonts/`, and the stylesheet is `static/css/site.css`. Zola resizes photos at build time, so copy them in at full size. The gallery shows only the photos listed in `data/photographs.yaml`, grouped as the herd, bulls, and shows and sales; other images in the folder are not shown there. Image filenames are lowercase with hyphens; the old WordPress image paths are no longer served.

## Build and upload the website

Check local links and build:

```sh
zola check --skip-external-links
zola build
```

The complete website is generated in `dist/`.

## Publish the website

The website is hosted on GitHub Pages. Every push to `main` runs `.github/workflows/pages.yml`, which checks and builds the site with the Zola version from `mise.toml` and publishes `dist/` to https://tronar.com.au. To republish without a change, run the workflow by hand from the repository's Actions tab.

The custom domain is set in the repository's Pages settings, not in a `CNAME` file. The DNS for `tronar.com.au` is at Porkbun; email is at Fastmail, so leave the `MX` and `TXT` records alone when changing the web records.

For a different domain, change `base_url` in `config.toml`, or use `zola build --base-url https://your-domain.example`. Deploy at the domain root; navigation and image URLs start with `/`. Resized images use absolute URLs from `base_url`, so to preview a build locally use `zola serve`, or `zola build --base-url http://localhost:PORT`.

## Content to review before launch

- Confirm the phone numbers, address and email are still correct.
- The old `/join-mailing-list/` address redirects to the home page; there is no mailing list.
- Historical external links and the YouTube video are preserved; their current availability is not guaranteed by the local link check.

Reference: [Zola documentation](https://www.getzola.org/documentation/).
