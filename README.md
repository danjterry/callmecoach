# Call Me Coach — Speaker Website

Premium speaker-booking site for Greg Taylor under the **Call Me Coach** brand.
Single-page static site (Home, About, Speaking Topics, Inquiry) with a built-in
inquiry modal + full inquiry page, the hero sizzle-reel lightbox, testimonials,
client logos, and a planner FAQ.

**Deploy `index.html` + `support.js` + the `uploads/` folder together** (same
structure). `index.html` is the page; `support.js` is a small runtime it loads,
and it pulls React + fonts from a CDN at runtime — so the file stays tiny and the
page paints instantly (no splash, no build step). `uploads/` holds the photos of
Greg the page references.

---

## 1. Push to GitHub

```bash
# from this folder
git init
git add index.html support.js netlify.toml README.md uploads/
git commit -m "Call Me Coach speaker site"
git branch -M main
git remote add origin https://github.com/<your-username>/callmecoach.git
git push -u origin main
```

(If you don't use the command line, you can also drag these files into a new repo
on github.com → "Add file" → "Upload files".)

---

## 2. Deploy to Netlify

1. Log in at **app.netlify.com** → **Add new site → Import an existing project**.
2. Choose **GitHub** and pick the `callmecoach` repo.
3. Build settings (Netlify usually auto-detects these from `netlify.toml`):
   - **Build command:** *(leave empty)*
   - **Publish directory:** `.`
4. Click **Deploy**. Your site goes live at a `*.netlify.app` URL in ~30 seconds.

Any future `git push` to `main` auto-deploys.

---

## 3. The inquiry form (already built in — Netlify Forms)

The inquiry form is wired to **Netlify Forms**, so it works the moment you deploy
to Netlify — no third-party account, no API key. A hidden detection form lives in
`index.html` and Netlify captures every submission automatically.

**To get the emails:**

1. After the first deploy, open **Netlify → your site → Forms**. You'll see a
   form named **`inquiry`** and any test submissions.
2. Go to **Site configuration → Forms → Form notifications → Add notification →
   Email notification** and enter Greg's email. Done — every inquiry now emails
   him and is also stored in the dashboard.

> On the live site (`*.netlify.app` or your `callmecoach` domain) the form submits
> for real. In local preview it just validates and shows the success screen.
> Netlify's free tier includes 100 submissions/month.

---

## 4. Point callmecoach.co at Netlify

1. In Netlify: **Site configuration → Domain management → Add a domain** →
   enter `callmecoach.co`.
2. Netlify shows you the DNS records. Easiest path: change your registrar's
   **nameservers** to Netlify's (it walks you through this), or add the `A` /
   `CNAME` records it lists at your current DNS host.
3. Netlify provisions a free SSL certificate automatically once DNS resolves
   (usually within an hour).

When moving off Squarespace, update the domain's DNS at whoever manages it now,
then remove the old Squarespace site once the new one resolves.

---

## Editing the site

The real source is **`Call Me Coach.dc.html`** — edit that (text, colors,
testimonials, topics), then refresh `index.html` from it. Keep `support.js`
alongside `index.html` whenever you deploy.

## Notes / TODO before launch

- **Sizzle reel** currently streams from Greg's existing Squarespace CDN. Move it
  to your own host (or YouTube/Vimeo) so it can't break later, then update the
  video `src`.
- Swap placeholder **photos of Greg**, **video testimonials**, and **client
  logos** for real assets.
- Confirm the **testimonial quotes** and **stats** are approved/accurate.
