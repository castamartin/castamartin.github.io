# Martin Časta — personal website

A self-hosted, static version of the personal academic site, rebuilt to run on
GitHub Pages instead of Google Sites. It's a single page (`index.html`) with no
build step, no framework, and no dependencies — just open it in a browser and it
works. Fonts load from Google Fonts; all paper/course links point to the same
Google Drive / journal / CNB pages as the original.

```
index.html    ← the whole site (edit this to update content)
photo_me.jpg  ← sidebar portrait
.nojekyll     ← tells GitHub Pages to serve the files as-is
README.md     ← this file
```

---

## Publish it on GitHub Pages

### Option A — no command line (easiest)

1. Sign in to GitHub and create a **new public repository**.
   - For a site at `https://<username>.github.io/`, name the repo exactly
     `<username>.github.io`.
   - For a site at `https://<username>.github.io/website/`, name it anything
     (e.g. `website`).
2. On the new repo page, click **Add file → Upload files**, then drag in
   `index.html`, `photo_me.jpg`, `.nojekyll`, and `README.md`. Commit.
3. Go to **Settings → Pages**. Under *Build and deployment*, set
   **Source = Deploy from a branch**, **Branch = main**, **Folder = / (root)**,
   and Save.
4. Wait a minute, then reload the Pages settings — the live URL appears at the
   top. Done.

### Option B — command line

```bash
git init
git add index.html photo_me.jpg .nojekyll README.md
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

Then enable Pages as in step 3 above.

---

## Use your own domain (optional)

1. In **Settings → Pages → Custom domain**, enter e.g. `martincasta.cz` and save.
   GitHub creates a `CNAME` file in the repo.
2. At your domain registrar, add DNS records pointing to GitHub Pages:
   - Four `A` records for the apex domain → `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - or a `CNAME` record for `www` → `<username>.github.io`
3. Back in Settings → Pages, tick **Enforce HTTPS** once the certificate is ready.

---

## Editing the site later

Everything lives in `index.html`.

- **Add a paper:** copy one `<article class="entry"> … </article>` block inside
  the relevant section, change the title, link, venue, and year. Entries are
  sorted newest-first by hand.
- **Change the bio:** edit the paragraphs inside `<section id="about">`.
- **Colours / fonts:** the palette and typefaces are CSS variables at the top of
  the `<style>` block (`--paper`, `--ink`, `--accent`, `--serif`, …). Change once,
  applies everywhere.
- The navigation, the "active section" highlighting, and the footer year update
  themselves — no need to touch them when adding content.

## Hosting the PDFs yourself (optional)

Links currently point to Google Drive, so the site stays light. If you'd rather
be fully independent of Google, drop the PDFs into a `papers/` folder in the repo
and change each `href` from the Drive URL to e.g. `papers/mortgage-rates.pdf`.
