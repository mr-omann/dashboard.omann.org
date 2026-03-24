# dashboard.omann.org

Mobile-accessible project status dashboard for Otto Omann.

Hosted at [dashboard.omann.org](https://dashboard.omann.org) via Cloudflare Pages.

## What it shows

- **Work pillar (melabot):** Notion task stats (open, in progress, overdue, blocked) + git/OV health per project
- **Private pillar (ottomator):** Coming Phase 2

## Data sources

The dashboard is fully static — it fetches pre-generated JSON reports from GitHub:

| Pillar | Source |
|--------|--------|
| Work | `https://raw.githubusercontent.com/mr-omann/melabot/main/reports/dashboard.json` |
| Private | TBD |

JSON reports are generated weekly by the hub-sitrep LaunchAgent (`melabot/PROJECTS/hub-sitrep/scripts/collect.sh`).

## Deployment

Connected to Cloudflare Pages. Every push to `main` deploys automatically.

**Custom domain:** `dashboard.omann.org`  
Set DNS CNAME: `dashboard` → `<your-pages-project>.pages.dev`

## Local preview

Open `index.html` directly in a browser. Note: the JSON fetch will fail due to CORS on `file://` — use a local server:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## No build step

Pure HTML/CSS/JS — no npm, no bundler. Cloudflare Pages deploys it directly.
