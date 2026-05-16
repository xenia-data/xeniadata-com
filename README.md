# xeniadata.com

Static landing site for **Xenia** (xeniadata.com) — a hotel data aggregator.

This repository hosts the public marketing/legal pages served at https://xeniadata.com:

- `/` — Landing page
- `/dmca/` — DMCA designated agent and takedown procedure
- `/privacy/` — Privacy policy
- `/terms/` — Terms of service
- `/methodology/` — How Xenia gathers, validates, and displays data
- `/crawler/` — Crawler information for webmasters

## Hosting

The site is served by **GitHub Pages** from the `main` branch root. The custom domain `xeniadata.com` is configured via the `CNAME` file plus DNS records at the registrar.

## Editing

Edit any HTML file directly. Commit and push to `main` — GitHub Pages auto-deploys within ~1 minute.

The source of truth for the longer legal pages is in `Staymatch/Xenia/Implementation/pages/*.md` (private Dropbox). HTML versions are regenerated via `build_pages.py` when those markdown sources change.

## Status

- 2026-05-16 — Initial commit. Landing page + 5 legal pages live.
- Service provider: **Xenia Data** — entity formation in progress (S-Corp, TX or NV). Pages contain `<!-- TBD-ENTITY -->` markers where the final legal name/state needs to be inserted.

