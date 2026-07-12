# TODO — items that need your input

This site is a strong first production version built from verified CV information.
The items below are things only you can supply or confirm. Nothing here is invented;
where a fact was missing it was left as a clear placeholder.

---

## A. Required before going live

### 1. GitHub repository — username is `kahalisayan` ✅
- `baseURL` is set to `https://kahalisayan.github.io/` in `config/_default/hugo.toml`. ✅
- **Still to do:** create a repository named **exactly** `kahalisayan.github.io` on
  GitHub, push this repo to it, then set **Settings → Pages → Source → GitHub Actions**.
- See `MAINTENANCE.md` → “GitHub Pages deployment” for the exact commands.

### 2. Public CV (privacy-critical)
- Your existing CV contains **private data** (phone number, date of birth, marital
  status, IEEE membership number). It is **not** published and is **not** committed.
- Create a private-free version and save it as:
  `static/files/Sayan_Kahali_Public_CV.pdf`
- The “Download CV” button is **hidden automatically** until that file exists — no
  further change needed once you add it.
- Do **not** add the original `SAYAN KAHALI_CV.pdf`; `.gitignore` already blocks the
  filename `static/files/Sayan_Kahali_CV.pdf` as a safeguard.

### 3. Profile photograph
- Add a professional headshot at: `static/images/profile.jpg`
- Until then, a clean “SK” initials placeholder is shown in the hero.
- Recommended: square-ish, at least 400×400 px, well-lit, neutral background.

### 4. Academic & social profile URLs
- Added ✅: **Google Scholar, ORCID, LinkedIn** (icons now show; they also feed the
  `sameAs` field in the Person schema, which helps SEO).
- **Still to add** (in `config/_default/languages.en.toml` → `[params.author].links`):
  **GitHub, ResearchGate**. Icons stay hidden until provided.
- Semantic Scholar and DBLP have no built-in icon; add them as links on the Contact
  page text if you want them (optional).

### 5. Publication DOIs / links
- Every entry in `data/publications.yaml` has empty `doi:` / `url:` fields.
- Add the DOI (just the `10.xxxx/...` part, no `https://doi.org/` prefix) for each
  paper. **Do not guess DOIs** — leave blank if unsure.
- Optionally add `pdf:` and `code:` links per entry.

---

## B. Optional — improve over time

- **Project images / thumbnails** — none are used yet; add if you want richer cards.
- **Self-hosted fonts** — the site uses high-quality system serif/sans stacks (no
  external fonts, fast, no layout shift). To brand it further, drop e.g. Newsreader +
  Inter `.woff2` files in `static/fonts/`, add `@font-face` in `assets/css/custom.css`,
  and point `--font-serif` / `--font-sans` at them.
- **Talks & Awards pages** — add when you have verified content (a `Springer Best
  Paper Award` is already noted on the relevant conference paper).
- **Blog draft outlines** — the three starter posts from the brief were not created as
  site content because the blog lives on Ghost. If you'd like, I can draft outlines for
  “What Makes an AI System Clinically Reliable?”, “From Medical Image Segmentation to
  Clinical Decision Support”, and “Why Efficient and Neuromorphic AI Matter for Edge
  Intelligence” for you to post on Ghost.
- **Custom domain** — see `MAINTENANCE.md` → “Custom domain”.
- **Analytics** — off by default. See `MAINTENANCE.md` → “Analytics” for a privacy-friendly
  option (Plausible / GoatCounter).
- **Citation counts** — intentionally omitted (they go stale and can look inflated).
  Link Google Scholar instead once its URL is added.

---

## D. SEO — getting the site found

On-page SEO is already built in: meta titles/descriptions, canonical URLs, Open Graph
+ Twitter cards, sitemap.xml, robots.txt (allows all), RSS, and Schema.org structured
data (Person + WebSite on the homepage, ScholarlyArticle for every journal/conference
paper). The rest is **off-page** — telling search engines the site exists:

1. **Google Search Console** (most important) — <https://search.google.com/search-console>
   - Add property `https://kahalisayan.github.io/`.
   - Verify via the **HTML tag** method: copy the `content="..."` code Google gives you
     into `googleSiteVerification` in `config/_default/params.toml`, then push.
   - Once verified, submit the sitemap: `sitemap.xml`.
2. **Bing Webmaster Tools** — <https://www.bing.com/webmasters> (same idea; paste the
   code into `bingSiteVerification`). You can also import directly from Search Console.
3. **Backlinks / entity signals** — add `https://kahalisayan.github.io/` to your
   Google Scholar profile, ORCID, LinkedIn, ResearchGate, GitHub bio, Ghost blog, and
   email signature. These help Google associate the site with you (and the `sameAs`
   links in the Person schema reinforce it — so filling section A.4 also helps SEO).
4. **Give it time** — indexing typically takes days to a couple of weeks after
   submission. Searching `site:kahalisayan.github.io` in Google shows what's indexed.

---

## C. Privacy decisions already made (for your awareness)

- Phone number, date of birth, marital status, and IEEE membership number are **never**
  rendered anywhere on the site.
- Impact factors were **removed** from all publication entries.
- No paper is claimed to be “open access”; no DOIs were fabricated.
- Ongoing hospital projects (GI ultrasound, colonoscopy) are described at a
  direction-only level, with no patient data, datasets, or internal results.
