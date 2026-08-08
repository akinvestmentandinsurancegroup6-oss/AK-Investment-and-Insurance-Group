# AK Investments and Insurance Group — Website

Single-file static website. Everything (HTML, CSS, JS) lives in `index.html` — no build step required.

## What's inside
- `index.html` — the entire site
- `robots.txt` — search engine crawl rules (+ sitemap reference)
- `sitemap.xml` — single-page sitemap for search engines
- `_redirects` — Netlify SPA/legacy-URL redirect rules (harmless if unused)

## SEO — what was added
- `<link rel="canonical">` — prevents duplicate-content issues
- `meta name="robots" content="index, follow"` — explicit crawl permission
- Open Graph tags (`og:title`, `og:description`, `og:image`, etc.) — controls how the site looks when shared on Facebook, LinkedIn, WhatsApp
- Twitter Card tags — controls the preview on X/Twitter
- `geo.region` / `geo.placename` — local-SEO signals for Chennai, Tamil Nadu
- JSON-LD structured data (`InsuranceAgency` schema) — helps Google understand this is a local insurance/loans business, show rich results, and match "insurance agency near me" style searches. Includes name, phone, address, founder, and social profile links.
- `sitemap.xml` + `Sitemap:` line in `robots.txt`

### ⚠️ Action needed before going live
All the new SEO tags use the placeholder domain **`https://www.akinvestments.in/`** (canonical URL, Open Graph URL/image, sitemap, JSON-LD `url`). Once you know your real domain:
1. Find-and-replace `https://www.akinvestments.in` with your actual domain in `index.html`, `sitemap.xml`, and `robots.txt`.
2. The `og:image` / `twitter:image` tags point to `/og-image.png`, which doesn't exist yet — create a 1200×630px preview image (logo + tagline works well) and add it to this folder, or point the tag at an existing image URL. Without it, social shares will show no preview image.
3. Once live, submit `sitemap.xml` in Google Search Console and Bing Webmaster Tools.

## External dependencies (loaded via CDN, need internet access to work)
- Google Fonts: Fraunces, Manrope, IBM Plex Mono
- Firebase (App + Realtime Database compat SDKs, v10.12.5) — used for form/lead submissions
  - Database URL already configured: `ak-investments-eed7b-default-rtdb.firebaseio.com`
- OpenStreetMap embed — for the location map

No other local images or assets are referenced — the few icons in the page are inline SVGs.

## Deploy options

### Netlify / Vercel (drag & drop)
1. Zip or drag this whole folder into the Netlify/Vercel dashboard ("Deploy manually" / "Add new site" → drag folder).
2. Done — `index.html` is auto-detected as the site root.

### GitHub Pages
1. Push this folder's contents to a repo (e.g. `main` branch or a `docs/` folder).
2. Repo Settings → Pages → set source to that branch/folder.
3. Site will be live at `https://<username>.github.io/<repo>/`.

### Any static host / shared hosting (cPanel, S3, etc.)
Just upload `index.html` (and the other files here) to the web root — no build, no server-side code needed.

### Local preview
```
cd deploy
python3 -m http.server 8000
```
Then open http://localhost:8000

## Notes
- The Firebase database rules should be checked/locked down in the Firebase console (this file only contains the public client config, which is expected to be public for web apps — but make sure your Realtime Database security rules restrict writes appropriately).
- If you want a custom domain, that's configured in your hosting provider's dashboard after deploying — this folder doesn't need any changes for that.
