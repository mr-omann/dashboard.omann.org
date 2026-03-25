# dashboard.omann.org

Mobile-accessible project status dashboards for Otto Omann.

Two separate dashboards, deployed from this repo via Cloudflare Pages:

| URL | File | Pillar |
|-----|------|--------|
| [work.omann.org](https://work.omann.org) | `work.html` | Work (melabot) |
| [life.omann.org](https://life.omann.org) | `life.html` | Private (ottomator) |

## What each shows

- **Notion task stats:** open, active, overdue, blocked/human-owned
- **Git / OV health:** per-project status flags (Critical, Git Stale, OV Silent, Idle, OK)
- **Needs Attention:** projects with flags worse than OK/Idle

## Data sources

Fully static — fetches pre-generated JSON reports from GitHub raw URLs on every load:

| Pillar | Source |
|--------|--------|
| Work | `https://raw.githubusercontent.com/mr-omann/melabot/main/reports/dashboard.json` |
| Private | `https://raw.githubusercontent.com/mr-omann/ottomator/main/reports/dashboard.json` |

JSON reports are generated weekly by each pillar's sitrep LaunchAgent (Mondays at 09:00 / 09:15).

## Deployment

Connected to Cloudflare Pages. Every push to `main` deploys automatically.

**Two custom domains on one Pages project:**
1. Add `work.omann.org` domain → set path rewrite or root redirect to `work.html`
2. Add `life.omann.org` domain → set path rewrite or root redirect to `life.html`

DNS in Cloudflare: CNAME `work` → `<pages-project>.pages.dev`, CNAME `life` → `<pages-project>.pages.dev`

## Local preview

```bash
python3 -m http.server 8080
# work: http://localhost:8080/work.html
# life: http://localhost:8080/life.html
```

Note: JSON fetch will fail from `file://` due to CORS — use the local server.

## No build step

Pure HTML/CSS/JS — no npm, no bundler. Cloudflare Pages deploys directly from repo root.
