# TV Fix Pro — website

Static one-page site for TV Fix Pro, a TV repair business in Banashankari 3rd Stage, Bengaluru.
Hosted free on GitHub Pages. **No build step, no backend** — everything is plain HTML, CSS and JS,
which is what keeps GitHub Pages hosting free.

**Live:** https://tvfixpro.github.io/

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | The entire site. CSS and JS are inline by design — one request, no build tooling. |
| `thank-you.html` | Where the contact form redirects after a successful submit. `noindex`. |
| `404.html` | GitHub Pages serves this automatically for unknown URLs. |
| `robots.txt` | Allows crawling, points to the sitemap. |
| `sitemap.xml` | Submitted to Google Search Console / Bing Webmaster Tools. |
| `site.webmanifest` | Icons + theme colour for "Add to Home Screen". |
| `.nojekyll` | Skips GitHub's Jekyll build. Serves files verbatim and deploys faster. |
| `assets/` | Logos, icons and the social share image. |

## Editing

Open `index.html` in any editor and save. There is nothing to compile or install.
Push to `main` and GitHub Pages redeploys in roughly a minute.

To preview locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Use a local server rather than opening the file directly — the root-relative paths
(`/assets/…`, `/favicon.ico`) only resolve correctly when served.

## Things that must stay in sync

The site URL is hard-coded in several places, because a static page cannot compute
its own address and search crawlers do not run JavaScript. If the domain ever changes,
update **all** of these:

- `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image` in `index.html`
- every `https://tvfixpro.github.io/...` inside the JSON-LD `@graph` block
- the form's hidden `redirect` field
- `robots.txt` (the `Sitemap:` line) and `<loc>` in `sitemap.xml`
- `canonical` in `thank-you.html`

## Contact form

Posts to [Web3Forms](https://web3forms.com). The `access_key` is a public, submit-only
key — it is visible in the page source to every visitor regardless of whether this repo
is public, so making the repo public exposes nothing extra.

Anti-spam already in place:

- a hidden `botcheck` honeypot field that bots fill and humans never see
- a `pattern` constraint on the mobile number
- `subject` / `from_name` so the emails arrive labelled

**Still to do in the Web3Forms dashboard:** restrict the key to `tvfixpro.github.io`
so nobody can reuse it from another site. That is the single most valuable mitigation
and it cannot be done from this repo.

## Never commit

`.gitignore` covers the usual suspects, but note that **git history is permanent** —
deleting a file in a later commit does not remove it from the repo. Never commit API
keys, `.env` files, or customer data.
