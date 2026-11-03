# The Age Check That Isn’t

A diagnostic report on the legal weaknesses and vulnerabilities in the UK Online Safety Act 2023 age-verification regime for pornography.

## Published site

The GitHub Pages site lives in **`docs/`**.

Set GitHub Pages to:

- **Source:** Deploy from a branch
- **Branch:** `main`
- **Folder:** **`/docs`**

The public site root is still **`/`** — the `/docs` folder is the publishing source in the repo, not a URL subpath.

Custom domain: **`porn.m30w.com`**. The `CNAME` file is in `docs/CNAME`, which is the publishing root.

Expected URL: <https://porn.m30w.com/>

## Local preview

```sh
python3 -m http.server 8000 --directory docs
```

Then open <http://localhost:8000/>.

## Structure

```
.
├── docs/                     # published site
│   ├── index.html            # the full report
│   ├── CNAME                 # custom domain
│   ├── .nojekyll             # serve as plain static files
│   └── assets/
│       └── css/
│           └── report.css    # shared stylesheet
├── research/                 # evidence dossiers (not published)
│   ├── 01-scope-gaps.md
│   ├── 02-enforcement.md
│   ├── 03-circumvention.md
│   ├── 04-privacy.md
│   ├── 05-other-loopholes-reform.md
│   ├── 06-4chan-ruling.md
│   ├── style-example.html    # earlier style specimen
│   └── sources/              # primary 4chan PDFs
└── README.md
```

## Notes

- No build step. The report is a single HTML file with one relative CSS file.
- No external assets: fonts are system fonts; charts and icons are inline SVG.
- `research/` is deliberately outside `docs/`, so it is not part of the published site.
- The report is print-friendly: browser print produces a clean multi-page PDF.
- The report is diagnostic only; it does not propose a fix.

## Deploy

```sh
git add -A
git commit -m "Restructure for GitHub Pages"
git push origin main
```

Then set **Settings → Pages → Source: Deploy from a branch → `main` / `/docs`** if it is not already set.

If you later prefer the site at the repo root instead, move the contents of `docs/` to the root and set the Pages folder to `/`. The current layout is the cleaner option because it keeps the research notes out of the published site.
