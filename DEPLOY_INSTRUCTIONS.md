# GitHub Pages handoff — 10-minute deploy for cravitoo-legal

**Why this instead of Hostinger/preview URL:** GitHub Pages has 99.95% SLA, no cold starts, no pod restarts, free. The preview URL has been rejected by Google twice because the backend restarts cause a 10–30 s window where the URL returns 502. GitHub Pages has no such window.

## What you'll get

| Page | Final URL (after deploy) |
| --- | --- |
| Privacy Policy | `https://<your-github-username>.github.io/cravitoo-legal/privacy/` |
| Data Deletion | `https://<your-github-username>.github.io/cravitoo-legal/data-deletion/` |

Plus flat fallbacks: `/privacy.html` and `/data-deletion.html`.

## Download the ready-to-push repo

```
https://food-ordering-app-54.preview.emergentagent.com/api/static/legal/cravitoo-legal-githubpages.zip
```

This ZIP contains a **fully initialised git repo** (`.git` folder included) with the first commit already made. You just need to push it.

## Deploy — three ways. Pick whichever matches your comfort level.

### Way 1 — GitHub web UI (zero-terminal, 5 min)

1. Download the ZIP, unzip it on your laptop → you'll get a folder called `github_pages`.
2. Go to https://github.com/new → repo name **`cravitoo-legal`** → **Public** → do NOT tick "Add README" (we already have one) → **Create repository**.
3. On the empty repo page, click **"uploading an existing file"** (the link in the middle).
4. Drag EVERYTHING from inside the `github_pages` folder (not the folder itself — the contents) into the drop zone. That's `index.html`, `README.md`, `.nojekyll`, `privacy/`, `privacy.html`, `data-deletion/`, `data-deletion.html`.
5. Commit message: `Initial legal pages` → **Commit changes**.
6. Click **Settings** (top-right of the repo page) → **Pages** (left sidebar) → under **Build and deployment → Source** pick **Deploy from a branch** → Branch: **main**, folder: **/ (root)** → **Save**.
7. Wait ~60 seconds. Refresh the Pages tab — it will show a green "Your site is live at https://<username>.github.io/cravitoo-legal/".
8. Verify both URLs in a new browser tab:
   - `https://<username>.github.io/cravitoo-legal/privacy/`
   - `https://<username>.github.io/cravitoo-legal/data-deletion/`

### Way 2 — Git CLI (if you have git on your laptop, 2 min)

```bash
# 1. Download + unzip (keeps .git intact — no re-committing needed)
curl -L -o cravitoo-legal.zip https://food-ordering-app-54.preview.emergentagent.com/api/static/legal/cravitoo-legal-githubpages.zip
unzip cravitoo-legal.zip -d cravitoo-legal
cd cravitoo-legal

# 2. Create empty repo on GitHub (web UI, same as step 2 in Way 1) — do NOT tick "Add README"

# 3. Push
git remote add origin https://github.com/<your-username>/cravitoo-legal.git
git push -u origin main

# 4. Settings → Pages → source = main / (root)
```

### Way 3 — Use GitHub CLI `gh` if installed (90 sec)

```bash
curl -L -o cravitoo-legal.zip https://food-ordering-app-54.preview.emergentagent.com/api/static/legal/cravitoo-legal-githubpages.zip
unzip cravitoo-legal.zip -d cravitoo-legal
cd cravitoo-legal
gh repo create cravitoo-legal --public --source . --push
gh api -X POST /repos/{owner}/cravitoo-legal/pages -f source[branch]=main -f source[path]=/
```

## After deploy — update Play Console

1. **Play Console → Grow users → Store presence → Store settings → Privacy policy**:
   `https://<username>.github.io/cravitoo-legal/privacy/` → Save.
2. **Play Console → App content → Data safety → Account deletion URL**:
   `https://<username>.github.io/cravitoo-legal/data-deletion/` → Save.
3. Repeat for the **Cravitoo Partner** app — same two URLs.
4. Resubmit the appeal with a note: "Legal URLs are now hosted on GitHub Pages (99.95% SLA)."

## Why these URLs will not get rejected

GitHub Pages serves these as pre-cached static files via Fastly's global CDN. There is no origin server to restart, no FastAPI uvicorn process, no supervisor cycle. The URL stays up 24/7.

## Verifying before you resubmit

```bash
curl -I https://<username>.github.io/cravitoo-legal/privacy/
curl -I https://<username>.github.io/cravitoo-legal/data-deletion/
# Both must say: HTTP/2 200, content-type: text/html
```

Also open in an **incognito window** and visually confirm each page shows the orange Cravitoo header + full policy text.

## Updating the pages later

The HTML files are 100% self-contained. To edit:
1. Edit the file in your GitHub repo (web UI "pencil" icon).
2. Commit — GitHub Pages redeploys in ~60 seconds.

## Custom domain later (optional)

Once your Hostinger-managed `cravitoo.com` DNS is handy, you can serve these at `legal.cravitoo.com`:
1. In the GitHub repo, add a file named `CNAME` with contents: `legal.cravitoo.com`
2. In Hostinger DNS, add a `CNAME` record: `legal` → `<username>.github.io`
3. GitHub Pages auto-issues an HTTPS cert via Let's Encrypt in ~10 minutes.
4. Update Play Console URLs to `https://legal.cravitoo.com/privacy/` and `/data-deletion/`.

---

If you get stuck, send me the GitHub username (or screenshot of the repo creation page) and I'll walk you through the specific error.
