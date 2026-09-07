# Helldivers Dashboard

A live Helldivers 2 status page: current Major Order / Strategic Opportunity progress
(including best-effort blocked/prereq-planet detection) and planets currently under
attack. Single static `index.html` - your browser calls the live, unofficial
[api.helldivers2.dev](https://api.helldivers2.dev) API directly (CORS-enabled), no
backend, no build step, nothing runs on a schedule anywhere.

This replaces an earlier version of this page that ran as a persistent script on a
home PC (LAN-only, required manual port-forwarding/firewall setup to reach from a
phone). This version has no such requirement - deploy it as a static site and it's
reachable from anywhere.

## What's here vs. the Discord bot

The companion Discord bot (a separate, private project) posts richer scheduled
reports - a 5-tier seasonally-adjusted prognosis/ETA, trend charts, and a
reconstructed historical activity log - all built from a local SQLite history this
static page has no equivalent of. This page is deliberately lighter: live status
only, refreshed by your browser every 60 seconds. No trend, no history, no activity
log.

## Deploying

Static site, no build step. On Cloudflare Pages:

1. Connect this repo.
2. Framework preset: **None**.
3. Build command: *(leave blank)*.
4. Build output directory: `/`.

Any other static host (GitHub Pages, Netlify, S3, etc.) works the same way - just
serve `index.html` as-is.

## Notes

- No secrets, no API keys, no config file - the API is public/unauthenticated. The
  `X-Super-Client`/`X-Super-Contact` headers in `index.html` are just a courtesy
  self-identification to the API operator, not credentials.
- Task-to-planet mapping and blocked/prereq detection are best-effort heuristics
  reverse-engineered from the API's behavior, not documented fields - see the
  comments in `index.html` for specifics.
