# MCN 2.0 Study Site

Interactive revision site for Mains Concise Notes 1–48 (Polity).

## Structure
- `index.html` — the entire app (open directly in any browser)
- `support.js` — runtime the page needs
- `notes/mcn01.json … mcn48.json` — note content (edit these to update notes)
- `_ds/…` — stylesheet + component bundle

## Run locally
Because the app fetches `notes/*.json`, open it via a local server, not by double-clicking:

```bash
npx serve site        # or: python3 -m http.server
```

## Deploy (GitHub + Vercel)
1. Create a GitHub repo and push this folder (see chat instructions).
2. In Vercel: **Add New → Project → Import** the repo.
3. Framework preset: **Other**. Build command: *none*. Output directory: `./`
4. Deploy — done. Every `git push` redeploys automatically.
