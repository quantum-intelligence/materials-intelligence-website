# Materials Intelligence — Rhone Research Group website

A Jekyll site for the Rhone Research Group (RPI), built for GitHub Pages.

## Structure

- `_config.yml` — site title, nav, contact info (edit here for global changes)
- `_data/*.yml` — **content lives here**: `members.yml`, `publications.yml`, `news.yml`, `courses.yml`, `resources.yml`
- `_layouts/default.html`, `_includes/header.html` / `footer.html` — shared page chrome
- `assets/css/main.scss` — all styling
- `index.html`, `research/`, `members/`, `publications/`, `courses/`, `resources/`, `news/`, `contact/` — pages

## Updating content

Most updates don't require touching HTML:

- **New publication** → add an entry to `_data/publications.yml`
- **New news item** → add an entry to `_data/news.yml`
- **New member** → add an entry under the right group in `_data/members.yml`
- **Member photo** → drop an image in `assets/img/members/`, then add `photo: /assets/img/members/name.jpg` to that person's entry in `members.yml`

## Running locally

```bash
gem install jekyll jekyll-sitemap jekyll-seo-tag
jekyll serve
```

Then open http://localhost:4000.

Note: there's no `Gemfile` in this repo on purpose. GitHub Pages' build
container already ships a matching `github-pages` gem environment; adding a
`Gemfile` makes it run `bundle install` against that frozen environment,
which is a common source of version-conflict build failures.

## Deploying on GitHub Pages

1. Push this repo to GitHub.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. GitHub will build the Jekyll site automatically — no Actions workflow needed.

## Custom domain (Cloudflare)

1. Add a `CNAME` file at the repo root containing just your domain, e.g. `materials-intelligence.com`.
2. In **Settings → Pages**, enter the same custom domain and enable **Enforce HTTPS** once it's available.
3. In Cloudflare DNS for the domain, add:
   - Four `A` records for `@` pointing to GitHub Pages' IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - A `CNAME` record for `www` pointing to `<your-github-username>.github.io`
4. Set the Cloudflare proxy status to **DNS only** (grey cloud) on those records until the GitHub Pages HTTPS certificate has provisioned, then you can switch to proxied (orange cloud) if desired.

## Contact form

The contact page posts to [Formspree](https://formspree.io) since GitHub Pages can't run a backend. Create a free Formspree form and replace `YOUR_FORM_ID` in `contact/index.html` with your real endpoint ID.
