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
