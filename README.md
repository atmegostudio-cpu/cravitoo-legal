# cravitoo-legal

Static hosting for Cravitoo's public legal pages. Served via GitHub Pages.

| Page | URL |
| --- | --- |
| Privacy Policy | `https://<username>.github.io/cravitoo-legal/privacy/` |
| Account & Data Deletion | `https://<username>.github.io/cravitoo-legal/data-deletion/` |

Both pages are 100% self-contained — inline CSS, no external fetches, no JS. Safe to re-host anywhere.

## Deploy

GitHub Pages: Settings → Pages → Source: `main` branch, `/ (root)` folder → Save. URLs become live in ~1 minute.

## Custom domain (optional)

To serve at `www.cravitoo.com/legal/*` later, add a `CNAME` file in the repo root containing `legal.cravitoo.com`, then create a CNAME DNS record pointing to `<username>.github.io`.
