# danielhuttonferris.com

A single-file static website. No build step, no framework, no dependencies.
Hosted free on GitHub Pages.

```
index.html      ← the entire site (content + design in one file)
CNAME           ← tells GitHub the site lives at danielhuttonferris.com
robots.txt      ← lets search engines index the site
sitemap.xml     ← helps Google find the page
.nojekyll       ← stops GitHub running an unnecessary build step
assets/
  photo.jpg     ← your headshot (already included)
  cv.pdf        ← your CV       (already included)
  papers/       ← ungated drafts of the paywalled articles
```

---

## 1. Nothing to add — it's complete

`assets/photo.jpg` (your headshot, cropped to 4:5) and `assets/cv.pdf` are
already in place. Upload the folder as-is.

To swap either one later, just replace the file keeping the same name.

**Note on the CV:** `assets/cv.pdf` is the *public* version — the referees page
has been removed (their names, phone numbers and email addresses are gone from
the file itself, not just hidden), and replaced with "References: available on
request." Keep your full version for job applications; don't overwrite this one
with it.

## 2. Put it on GitHub

1. Make a free account at [github.com](https://github.com).
2. Click **+** (top right) → **New repository**.
3. Name it **`<your-username>.github.io`** — e.g. `dhuttonferris.github.io`.
   Set it to **Public**. Click **Create repository**.
4. Click **uploading an existing file**, drag in everything from this folder
   (including the `assets` folder), then click **Commit changes**.

## 3. Turn on hosting

**Settings** → **Pages** (left sidebar) → under *Build and deployment*
set **Source: Deploy from a branch**, **Branch: `main`**, **Folder: `/ (root)`** → **Save**.

Wait 1–2 minutes. Your site is now live at `https://<your-username>.github.io`.

## 4. Point danielhuttonferris.com at it

Go to wherever the domain is registered (probably Wix → *Domains*) and open its
**DNS records**. Replace the existing records with:

| Type  | Host / Name | Value |
|-------|-------------|-------|
| A     | `@`         | `185.199.108.153` |
| A     | `@`         | `185.199.109.153` |
| A     | `@`         | `185.199.110.153` |
| A     | `@`         | `185.199.111.153` |
| AAAA  | `@`         | `2606:50c0:8000::153` |
| AAAA  | `@`         | `2606:50c0:8001::153` |
| AAAA  | `@`         | `2606:50c0:8002::153` |
| AAAA  | `@`         | `2606:50c0:8003::153` |
| CNAME | `www`       | `<your-username>.github.io` |

Then in GitHub: **Settings** → **Pages** → **Custom domain** →
type `danielhuttonferris.com` → **Save**.

DNS takes anywhere from 10 minutes to a few hours. Once GitHub shows a green
tick, tick **Enforce HTTPS** as well. You now have a free SSL certificate.

## 5. Only then, cancel Wix

Check the site works at `https://danielhuttonferris.com` first. Then cancel the
Wix Premium plan.

⚠️ **Keep the domain registration.** If the domain is registered *through* Wix,
cancelling the site plan is separate from cancelling the domain — but it's worth
transferring the domain out to a cheaper registrar (Cloudflare charges at cost,
roughly £8/year). Wix requires a domain to be at least 60 days old before it can
be transferred away.

---

## Editing the site later

Everything lives in `index.html`. On github.com, open the file and click the
pencil icon ✏️. Edit, then click **Commit changes**. The site updates itself in
about a minute.

### Adding a publication

Find the section that starts `<h3>Peer-reviewed articles</h3>` and copy one of
the blocks, changing the text:

```html
<div class="entry">
  <div class="entry-year">2026</div>
  <div class="entry-body">
    <p class="entry-title">Your Article Title Here</p>
    <p class="entry-meta">With Co-Author. <cite>Journal Name</cite> 12(3), 45&ndash;67.</p>
  </div>
</div>
```

- `<cite>` renders the journal name in italics.
- To link the title, wrap it: `<p class="entry-title"><a href="https://doi.org/...">Title</a></p>`
- To flag something unpublished, add `<span class="entry-note">Online first</span>`
  after the `entry-meta` line.

Newest goes at the top.

### The links under each publication

Each entry ends with a row of links:

```html
<div class="entry-links">
  <span class="entry-note">Online first</span>
  <a href="https://doi.org/...">Journal</a>
  <a href="assets/papers/my-paper-draft.pdf" target="_blank" rel="noopener" data-pdf>Ungated draft (PDF)</a>
</div>
```

- Say **"Journal (open access)"** when the published version is already free —
  then no draft is needed.
- Say **"Journal"** plus an ungated draft when it's paywalled.
- `data-pdf` is what adds the small ↓ arrow. Only put it on PDF links.
- Drop the `<span class="entry-note">` line if it isn't forthcoming.

**To add a new draft:** put the PDF in `assets/papers/` using lowercase-and-hyphens
for the filename (no spaces — spaces break URLs), then link to it exactly as above.

### Changing the colours

The whole palette is the first block of CSS, near the top of `index.html`:

```css
--accent: #2E5C4E;   /* the deep green used for links and headings */
```

Change that one value and the entire site re-colours itself. The dark-mode
palette is a few lines below, under `prefers-color-scheme: dark`.

### Changing text

All the words are plain text in the bottom half of the file, between the HTML
tags. Edit anything that isn't inside `<` `>` brackets.

---

## Cost

| Item | Cost |
|---|---|
| Hosting (GitHub Pages) | £0 |
| SSL certificate | £0 |
| Bandwidth (100GB/month soft limit) | £0 |
| Domain renewal | ~£8–15/year |

**Total: the price of the domain, and nothing else.**
