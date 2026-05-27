# dhelai.in — Landing page

Static one-page site for **dhelai.in**. Showcases _The Next Super Wave_ (English + Hindi),
links out to the e-book stores and the Android app, and surfaces the author bio. Reading
itself happens in the app, not on the web.

## Local preview

Any static server works. From this folder:

```bash
python3 -m http.server 8080
# or
npx serve .
```

Then open <http://localhost:8080>.

## File layout

```
website/
├── index.html      # single-page landing (HTML + inline CSS, no JS framework)
├── CNAME           # custom-domain hint for GitHub Pages → dhelai.in
├── README.md       # this file
└── assets/         # book covers copied from the app's asset folder
    ├── nsw-3d-en.png
    ├── nsw-3d-hi.png
    ├── nsw-fullcover-en.jpg
    └── nsw-fullcover-hi.png
```

If the source covers change in the app, refresh the copies:

```bash
cp ../appcode/ShoonayAISchool/assets/Book_Covers/3dCover/the-next-super-wave-3d.png assets/nsw-3d-en.png
cp ../appcode/ShoonayAISchool/assets/Book_Covers/3dCover/the_next_super_wave_Hindi_3D.png assets/nsw-3d-hi.png
cp ../appcode/ShoonayAISchool/assets/Book_Covers/the-next-super-wave/the-next-super-wave-fullcover-preview.jpg assets/nsw-fullcover-en.jpg
cp ../appcode/ShoonayAISchool/assets/Book_Covers/the-next-super-wave-hindi/the-next-super-wave-hindi-fullcover.png assets/nsw-fullcover-hi.png
```

## Deploy to GitHub Pages

The simplest path: a **separate repo** named e.g. `dhelai-site`, with this folder's contents
at the repo root.

1. Create a new repo on GitHub (public) — call it whatever (`dhelai-site` works).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial landing page"
   git branch -M main
   git remote add origin git@github.com:<you>/dhelai-site.git
   git push -u origin main
   ```
3. On GitHub → Settings → Pages:
   - Source: **Deploy from a branch**
   - Branch: `main` / `(root)`
4. Wait ~1 minute. Pages will serve at `https://<you>.github.io/dhelai-site`.
5. To use the `dhelai.in` custom domain:
   - `CNAME` file is already in this repo (set to `dhelai.in`).
   - Add a DNS `CNAME` record at your domain registrar: `@` (or `www`) → `<you>.github.io`.
   - Back on Pages, enter `dhelai.in` in the Custom domain field and enforce HTTPS.

## Updating content

Edit `index.html` directly — content lives inline (no build step, no framework). Stats
(pages, price), store links, and author bio are hard-coded; when the book data changes in
the app's `book_metadata.json`, mirror the same updates here.

## What's NOT on the site

- The reader itself. Reading happens only in the Dhelai app — keeps Google Play's payment
  policy clean and means we don't have to ship the book JSON over public web.
- User accounts, likes, comments — analytics live in the app.
