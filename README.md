# GM91 — Growth Machine 91

Productized growth for local businesses, by **91pixels**. GM91 gets local businesses found on Google, booked online, reviewed by happy customers, and scaled with ads — run as one system.

**Live:** https://bala91px.github.io/gm91/

## What's here
- `index.html` — the deployed GM91 pitch (generic, for any local business). This is what GitHub Pages serves at the root URL.
- `gm91-pitch.html` — the same pitch as a named copy. **Keep it in sync with `index.html`.**

Single-file, self-contained HTML — Fira Sans (display) + Inter (body), strict 4-point spacing grid. No build step, no dependencies.

## Packages
Free Google audit → **Spark ₹500/mo** → **Momentum ₹1,000–1,200/mo** → **Lead Machine ₹3,000–5,000/mo + setup**. India introductory pricing; US & Dubai priced per market.

## Deploy
GitHub Pages **auto-deploys on every push to `main`** — no manual deploy step (unlike Cloudflare Pages). Edit, commit, push:

```bash
git add -A && git commit -m "update pitch" && git push
```

Allow ~1 minute for the Pages build after pushing.

## Local preview
```bash
python3 -m http.server 8080   # → http://localhost:8080
```
