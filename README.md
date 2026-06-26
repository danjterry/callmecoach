# Call Me Coach — Speaker Website

Premium speaker-booking site for Greg Taylor under the **Call Me Coach** brand.
Single-page static site (Home, About, Speaking Topics, Inquiry) with a built-in
inquiry modal + full inquiry page, the hero sizzle-reel lightbox, testimonials,
client logos, and a planner FAQ.

**Deploy `index.html` + `support.js` together** (same folder). `index.html` is the
page; `support.js` is a small runtime it loads, and it pulls React + fonts from a
CDN at runtime — so the file stays tiny and the page paints instantly (no splash,
no build step).

---

## 1. Push to GitHub

```bash
# from this folder
git init
git add index.html support.js netlify.toml README.md
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

## 3. Connect the inquiry form (so Greg gets the emails)

The form is pre-wired for **Formspree** (free tier is plenty to start).

1. Create a free account at **formspree.io** and add a new form.
2. Point its notifications to Greg's email; Formspree also sends the inquirer a
   confirmation if you enable **autoresponse**.
3. Copy the form ID from the endpoint it gives you —
   `https://formspree.io/f/XXXXXXXX` → the ID is `XXXXXXXX`.
4. Open **`Call Me Coach.dc.html`**, find this line near the top of the logic:

   ```js
   FORMSPREE_ID = "";
   ```

   Paste your ID between the quotes, e.g. `FORMSPREE_ID = "xayzabcd";`
5. Re-export `index.html` (ask Claude to "refresh index.html") and push again.

> Until an ID is set, the form still validates and shows the success screen, but
> no email is sent. Basin or Getform work the same way — just swap the endpoint
> URL in the `submit` function.

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
