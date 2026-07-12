# Dr. Sayan Kahali — academic website

Personal research website built with [Hugo](https://gohugo.io/) and the
[Blowfish](https://blowfish.page/) theme, deployed free on GitHub Pages via GitHub
Actions. Content is driven by Markdown and YAML data files so it is easy to maintain.

> First-time setup checklist lives in [`TODO.md`](TODO.md) (GitHub username, photo,
> public CV, profile links, DOIs).

---

## Prerequisites (Ubuntu / Linux)

- **Git** — `sudo apt install git`
- **Hugo Extended `0.163.3`** — must be the *extended* build and within the theme's
  supported range (`0.158.0`–`0.163.3`). Install it without touching apt's older
  version:

  ```bash
  cd /tmp
  wget https://github.com/gohugoio/hugo/releases/download/v0.163.3/hugo_extended_0.163.3_linux-amd64.tar.gz
  tar xzf hugo_extended_0.163.3_linux-amd64.tar.gz hugo
  mkdir -p ~/.local/bin && mv hugo ~/.local/bin/hugo
  # make sure ~/.local/bin is on your PATH:
  echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
  hugo version   # should print v0.163.3 ... +extended
  ```

No Go, Node, or database is required. Search is Blowfish's built-in static search.

---

## Get the theme (git submodule)

The Blowfish theme is a git submodule under `themes/blowfish`. After cloning the
repository:

```bash
git submodule update --init --recursive
```

---

## Local preview

```bash
hugo server -D=false     # http://localhost:1313/  (drafts hidden, like production)
```

Add `-D` if you want to preview drafts. Stop with `Ctrl+C`.

Production build (writes to `public/`, which is git-ignored):

```bash
hugo --gc --minify
```

---

## Editing content

### Add a publication
Edit [`data/publications.yaml`](data/publications.yaml). Add an entry under
`journal:`, `conference:`, or `abstract:`:

```yaml
  - key: kahali2025example        # unique BibTeX key
    selected: true                # show in the "Selected" list & homepage
    title: "Paper title"
    authors: "Sayan Kahali, Co Author"   # your name is auto-bolded
    venue: "Journal or Conference Name (Publisher)"
    journal: "Journal Name"       # (journals) used in BibTeX
    publisher: "Wiley"
    volume: "12"
    issue: "3"
    pages: "100-110"
    year: 2025
    doi: "10.xxxx/xxxxx"          # leave "" if unknown — never guess
    url: ""
    tags: ["topic"]
```

BibTeX is generated automatically from these fields (copy button on each entry).

### Add a project
```bash
hugo new content projects/my-project.md   # uses archetypes/projects.md
```
Fill in the front matter (`status`, `summary`, `weight`, optional `publications:`
list of BibTeX keys) and the body sections. Lower `weight` sorts first.

### Add a news / update item
Edit [`data/news.yaml`](data/news.yaml) and add to the top of `items:`:
```yaml
  - date: "2026"
    text: "Short, factual update."
```

### Add experience, service, patents, research themes
Edit the matching file in `data/`: `experience.yaml`, `service.yaml`,
`patents.yaml`, `research.yaml`. The pages render straight from these.

### Add a blog post
The blog lives on your external Ghost site
(<https://the-conscious-compiler.ghost.io/>). Post there — the homepage pulls the
three latest posts automatically via its RSS feed at build time. Nothing to edit here.

### Profile photograph
Save as `static/images/profile.jpg`. The hero and About page use it automatically;
otherwise an “SK” initials placeholder is shown.

### Replace the CV
Save a **private-free** PDF as `static/files/Sayan_Kahali_Public_CV.pdf`. The
“Download CV” button appears automatically once the file exists. Do not commit the
original CV (it contains private data and is blocked in `.gitignore`).

### Update social / profile links
Edit `config/_default/languages.en.toml` → `[params.author].links`. Uncomment the
platforms you have and add real URLs. Missing icons stay hidden.

---

## GitHub Pages deployment

This is configured as a **user site** served at the domain root.

1. Create a GitHub repository named **exactly** `USERNAME.github.io`.
2. Set the base URL in `config/_default/hugo.toml`:
   `baseURL = "https://USERNAME.github.io/"`.
3. Push the repository (the theme submodule pushes as a reference):

   ```bash
   git remote add origin git@github.com:USERNAME/USERNAME.github.io.git
   git push -u origin main
   ```

4. In the repo on GitHub: **Settings → Pages → Build and deployment → Source →
   GitHub Actions**.
5. Every push to `main` triggers `.github/workflows/deploy.yml`, which installs Hugo
   Extended, builds the site, and deploys it. You can also run it manually from the
   **Actions** tab (“Run workflow”).

The workflow injects the correct base URL automatically, so deployment works even if
the config placeholder is not yet updated.

### Manual (local) deploy alternative
Not needed with the Actions workflow. If you ever want to deploy by hand, run
`hugo --gc --minify` and publish the `public/` directory yourself.

---

## Custom domain (optional, later)

1. Add a file `static/CNAME` containing just your domain, e.g. `www.example.com`.
2. Configure the DNS records with your registrar (CNAME to `USERNAME.github.io`, or
   A/AAAA records to GitHub Pages IPs).
3. Set the domain under **Settings → Pages → Custom domain** and enable HTTPS.
4. Update `baseURL` in `config/_default/hugo.toml` to the new domain.

---

## Analytics (optional, off by default)

No analytics or cookies are enabled. Privacy-friendly options:

- **GoatCounter** or **Plausible** — add the provider's small script via
  `layouts/partials/extend-head-uncached.html`.
- **Google Analytics** — set `googleAnalytics = "G-XXXX"` in `hugo.toml` (Blowfish
  supports it natively). Least privacy-friendly; not recommended.

---

## Updating the Blowfish theme safely

```bash
cd themes/blowfish
git fetch --tags
git checkout v<new-version>     # check the theme changelog first
cd ../..
hugo --gc --minify              # rebuild and confirm no errors
git add themes/blowfish && git commit -m "chore: update Blowfish theme"
```

Because customisations live in the project's own `layouts/`, `assets/`, `config/`,
and `data/` — never inside `themes/blowfish/` — theme updates will not overwrite your
work. If a new version changes its minimum Hugo requirement, update `HUGO_VERSION` in
`.github/workflows/deploy.yml` and your local Hugo to match.

---

## Troubleshooting

- **`Module "blowfish" is not compatible with this Hugo version`** — install a Hugo
  Extended version within `0.158.0`–`0.163.3` (see Prerequisites).
- **`can't evaluate field Locale` / template errors on build** — usually a Hugo
  version that is too old for the theme. Upgrade Hugo Extended.
- **Blank theme / missing styles** — the submodule wasn't fetched. Run
  `git submodule update --init --recursive`.
- **Homepage “From the blog” section missing** — the Ghost RSS feed was unreachable
  during the build (the section hides itself rather than failing the build). Re-run
  the build when the blog is reachable.
- **“Download CV” button not showing** — expected until you add
  `static/files/Sayan_Kahali_Public_CV.pdf`.

---

## Repository layout

```
config/_default/   Hugo + Blowfish configuration (TOML)
content/           Page content (Markdown)
data/              Publications, projects, experience, news, service, patents (YAML)
layouts/           Custom templates (homepage, publications, projects, etc.)
assets/css/        Custom color scheme (schemes/sayan.css) and custom.css
static/            Static files: images/ (profile photo), files/ (public CV)
archetypes/        Templates for `hugo new`
themes/blowfish/   Theme (git submodule — do not edit directly)
.github/workflows/ GitHub Actions deployment
```
