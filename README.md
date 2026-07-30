# Oʻahu — A Hosted Week

A single-page, week-long Oʻahu itinerary my friends can browse, customize, and take with them.

## What it does

- **The Week** — seven days laid out as planned / optional / free time, with "open" dinners left deliberately unscheduled. Every place links out to Google Maps.
- **Build** — tick the activities you actually want. Presets (Essentials, Recommended, Everything) set a baseline; the per-person price updates live.
- **Costs** — per-adult breakdown by group size. Shared costs (parking, fuel, lodging, rental car) split cheaper as the group grows.
- **Guides** — food, restaurants, hikes, water activities, seasonal notes, and dinner options by neighborhood.

Two ways to take your plan with you:

- **Download PDF** — generates a one-page summary of your selections via jsPDF (falls back to the browser print dialog if that fails).
- **Copy shareable link** — encodes your whole plan in the query string, so opening the link restores that exact selection.

## Layout

```
public/index.html   the entire site — one self-contained file
wrangler.jsonc      Cloudflare Workers config (static assets)
```

## Running it

Open `public/index.html` directly, or serve it:

```
npx wrangler dev
```

The share-link feature builds absolute URLs only over `http`/`https`, so use a server rather than `file://` if you're testing that.

## Deploying

Cloudflare Workers with static assets. No build step.

```
npx wrangler login    # once
npx wrangler deploy
```

Everything in `public/` is served as-is; `wrangler.jsonc` points at that directory, which keeps `README.md` and `.git` out of the upload.

## Note on external requests

The page loads Google Fonts and jsPDF from CDNs. It degrades gracefully — system fonts if Fonts fails, the print dialog if jsPDF fails — but the two files can be vendored into the repo if you'd rather it make no third-party requests.
