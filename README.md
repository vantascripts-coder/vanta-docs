# Vanta Docs

Documentation site for Vanta FiveM scripts, built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

## Run locally

```bash
# 1. (once) create a virtual env - optional but recommended
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
# source .venv/bin/activate

# 2. install
pip install -r requirements.txt

# 3. live preview at http://127.0.0.1:8000  (auto-reloads on save)
mkdocs serve
```

## Build static site

```bash
mkdocs build          # outputs to ./site
```

## Deploy

### Option A — GitHub Pages (automatic, recommended)
1. Push this folder to a GitHub repo (e.g. `Vanta-Scripts/vanta-docs`).
2. The included workflow `.github/workflows/deploy.yml` builds and publishes on
   every push to `main`.
3. In the repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
4. Your docs go live at `https://<user>.github.io/<repo>/`.

### Option B — Cloudflare Pages (custom domain like docs.vanta.dev)
1. Connect the repo in the Cloudflare Pages dashboard.
2. Build command: `pip install -r requirements.txt && mkdocs build`
3. Build output directory: `site`
4. Add your custom domain in the Pages project settings.

## Structure

```
vanta-docs/
├── mkdocs.yml            # site config, theme, navigation
├── requirements.txt
├── docs/
│   ├── index.md
│   ├── getting-started/
│   ├── configuration/
│   ├── localization.md
│   ├── features.md
│   ├── security.md
│   └── faq.md
└── .github/workflows/deploy.yml
```

To add a page: create the `.md` file under `docs/` and add it to the `nav:` in
`mkdocs.yml`.
