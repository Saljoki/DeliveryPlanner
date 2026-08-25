# DeliveryPlanner

A single-file delivery planning board — lanes, tasks, deadlines, holidays, share
links, and PDF/ICS/JSON export. Everything lives in
[`index.html`](index.html): inline CSS and JS, no build step, no backend.

Because it is one static file at the repo root, any static host serves it as-is.

## Deployment

Two routes are wired up; either works, and they can coexist.

**GitHub Actions** — [`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml)
assembles `_site/` and publishes on every push to `main`, plus manual runs from
the Actions tab. Requires **Settings → Pages → Source: GitHub Actions**.

**Deploy from a branch** — set **Settings → Pages → Source** to **Deploy from a
branch**, `main`, `/ (root)`. GitHub's own Pages builder serves `index.html`
directly, using no Actions minutes. The root `.nojekyll` keeps Jekyll from
processing the file. Useful when Actions is unavailable.

Either way the site lands at https://saljoki.github.io/DeliveryPlanner/

## Where plans are stored

Plans are held in the browser's `localStorage`, keyed per origin — nothing is
sent to a server. That means plans do not follow you between browsers or
devices, and clearing site data clears them. Use **Export** for anything worth
keeping, or **Share link**, which packs the whole plan into the URL hash so
recipients get a read-only copy without any storage at all.

Because the key is per origin, the same plan does not carry across two different
deployments of this app — each host has its own storage.

## Running locally

Open `index.html` directly, or serve it if you want share links to produce real
URLs:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000/
```

PDF export pulls `html2canvas` and `jsPDF` from cdnjs on first use, so that one
feature needs network access; everything else works offline.
