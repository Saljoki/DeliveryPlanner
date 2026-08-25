# DeliveryPlanner

A single-file delivery planning board — lanes, tasks, deadlines, holidays, share
links, and PDF/ICS/JSON export. Everything lives in
[`delivery-planner.html`](delivery-planner.html): inline CSS and JS, no build
step, no backend.

Once deployed it is served at https://saljoki.github.io/DeliveryPlanner/ — that
URL is dead until the two setup steps below are done.

## Deployment

Pushes to `main` publish the site via
[`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml). The
workflow copies `delivery-planner.html` to `_site/index.html` and hands it to
the GitHub Pages actions, so the HTML file stays the single source of truth —
there is no duplicated copy to keep in sync.

One-time setup, in the repo's **Settings → Pages**: set **Source** to **GitHub
Actions**. After that every push to `main` redeploys; `workflow_dispatch` lets
you deploy manually from the Actions tab.

## Where plans are stored

Plans are held in the browser's `localStorage`, keyed per origin — nothing is
sent to a server. That means plans do not follow you between browsers or
devices, and clearing site data clears them. Use **Export** for anything worth
keeping, or **Share link**, which packs the whole plan into the URL hash so
recipients get a read-only copy without any storage at all.

## Running locally

Open the file directly, or serve it if you want share links to produce real
URLs:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000/delivery-planner.html
```

PDF export pulls `html2canvas` and `jsPDF` from cdnjs on first use, so that one
feature needs network access; everything else works offline.
