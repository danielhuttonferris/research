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
  og.png        ← the image shown when someone shares your link
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

**Why this step exists:** GitHub is a file-storage site first and a web host
second. Uploading the files doesn't publish them — they just sit there. This
step flips the switch that says "serve these files as a website."

**Click by click:**

1. You should be looking at your repository page, with your files listed
   (`index.html`, `assets`, and so on).

2. Along the top of that page is a row of tabs: *Code · Issues · Pull requests ·
   Actions · Projects · Wiki · Security · Insights · **Settings***.
   Click **Settings** — the last one, on the right.

   ⚠️ This is the trap: there is *also* a Settings for your account, under your
   profile picture in the top-right corner. That's the wrong one. You want the
   Settings **tab on the repository page**.

3. A long list appears down the left. Scroll to the group headed
   *Code and automation* and click **Pages**.

4. Under the heading **Build and deployment** there's a box labelled **Source**
   with a dropdown. Set it to **Deploy from a branch**.

   > *Plain English: "publish the files I uploaded", as opposed to "run a build
   > process first". You don't need a build — your site is already finished HTML.*

5. A second row appears with two dropdowns. Set them to:

   - first dropdown: **`main`**
   - second dropdown: **`/ (root)`**

   > *Plain English: "main" is the name of your one and only version of the
   > folder — you'll have nothing else to choose. "/ (root)" means "the web
   > files are at the top level", which is true: `index.html` is not tucked
   > inside a subfolder.*

6. Click **Save**.

**Then wait.** For a minute or two the page may say *"Your site is ready to be
published"* — that's normal, not an error. Refresh after a couple of minutes and
it changes to:

> ✅ **Your site is live at `https://<your-username>.github.io/`**

Click that link. You should see your website. The first publish is the slowest;
every later edit goes live in under a minute.

**If nothing happens after 10 minutes,** the usual cause is that `index.html`
ended up inside a subfolder instead of at the top level. On the repository's
**Code** tab you should see `index.html` in the very first list of files. If
instead you see a single folder that you have to click into, that's the problem
— open it, and re-upload the files from inside it.

### ⚠️ Filenames are case-sensitive

GitHub Pages treats `photo.JPG` and `photo.jpg` as two completely different
files. Windows does not, so a file can arrive with its capitalisation changed
and silently 404 on the live site while looking fine on your PC.

Every filename in this folder is **lowercase**. If something doesn't appear on
the site, check its name on the repository's **Code** tab before anything else.

## 4. Point danielhuttonferris.com at it

Go to wherever the domain is registered (Wix → *Domains* → **Manage DNS**).

> ### ⚠️ Do not clear out the record list
>
> Change **only** the records named below. Everything else on that page —
> **MX** records, **TXT** records, and any mail-related **CNAME**s such as
> `imap.` or `mail.` — is what makes email on this domain work. Delete those
> and your email stops arriving. Leave them exactly as they are.

**Change these four A records** (the ones whose host is the bare domain):

| Type | Host / Name          | Value             |
|------|----------------------|-------------------|
| A    | `danielhuttonferris.com` (or `@`) | `185.199.108.153` |
| A    | `danielhuttonferris.com` (or `@`) | `185.199.109.153` |
| A    | `danielhuttonferris.com` (or `@`) | `185.199.110.153` |
| A    | `danielhuttonferris.com` (or `@`) | `185.199.111.153` |

**Then find the `www` CNAME** in the *CNAME (Aliases)* section and change its
value to `<your-username>.github.io` — nothing else in that section.

### About AAAA records — skip them

GitHub also publishes four **AAAA** records for IPv6. **Wix's DNS editor cannot
create AAAA records at all** — it only handles A, CNAME, MX, TXT, SPF, SRV and
NS. This is not something you're doing wrong, and it doesn't matter: the A
records alone are all GitHub Pages needs. AAAA records only add a second route
for visitors on IPv6-only connections, and those visitors reach the site over
IPv4 regardless.

If you later move the domain to Cloudflare, you can add them there in a minute.

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

### Abstracts

Each publication can carry an abstract that opens when the reader clicks
"Abstract". It sits directly after the links row:

```html
<div class="entry-links">
  ...
</div>
<div class="abs" id="abs-my-paper">
  <p>Your abstract text. Use &lt;em&gt;words&lt;/em&gt; for italics.</p>
</div>
```

The "Abstract" button is added automatically by the small script at the bottom
of the file — you never write it yourself. Give each panel a unique `id`.
Leave the `<div class="abs">` out entirely and that paper simply has no button.

Abstracts are written into the page fully visible and collapsed by JavaScript,
so they still work for search engines and for anyone with JavaScript off.

### Research-interest tags

The tags under your bio are buttons. Hovering one emphasises the papers it
covers; tapping one pins it (for touch screens). Two places control this:

1. The tag itself, in `<div class="tags" id="themes">`:
   `<button type="button" class="tag" data-theme="elections" ...>elections</button>`
2. Each publication's opening tag:
   `<div class="entry" data-themes="democracy representation elections">`

A paper lights up for a tag when its `data-themes` contains that tag's
`data-theme`. Spelling must match exactly — lowercase, hyphens instead of
spaces. An entry with no `data-themes` never lights up, which is currently the
case for the book review and the two Conversation pieces.

Tags are listed most-covered first, and each shows how many papers it covers.

The tag row is **sticky** — it pins to the top of the window as you scroll, so
you can always see which papers are lighting up. That's `.themebar` in the CSS;
it has to sit as a direct child of `<main class="main">` (not inside a
`<section>`) or it stops sticking partway down the page.

Clicking a tag **filters** the list to just those papers and reveals a
"Show all papers" button. Group headings with nothing left under them hide
themselves.

### The "Latest" panel

The tinted box above the publications list is `<section id="latest">`. When you
publish something new, change the title, link and journal in that block — it's
plain HTML, no cleverness. Deleting the whole section is fine too.

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

### On phones

Everything below `@media (max-width: 900px)` at the very end of the stylesheet
controls the phone layout. Two things to know if you edit it:

- The sidebar uses `display: contents` on small screens, which dissolves it so
  its parts can be reordered around the main column with `order`. Your photo and
  name sit at the top; contact details and profile links move to the bottom, so
  the papers come first.
- That media query must stay **last** in the stylesheet. Move it earlier and the
  base rules override it, because they have equal specificity.

---

## Cost

| Item | Cost |
|---|---|
| Hosting (GitHub Pages) | £0 |
| SSL certificate | £0 |
| Bandwidth (100GB/month soft limit) | £0 |
| Domain renewal | ~£8–15/year |

**Total: the price of the domain, and nothing else.**
