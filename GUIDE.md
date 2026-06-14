# SkyLuxe Media — Complete Launch Guide
### From zero to a live business website, step by step

This guide takes you through everything in order: setting up the business, buying the domain, publishing the website, connecting your email and contact form, editing the site yourself, adding your real photos and videos, and getting found by clients.

---

## PART 1 — Set up the business (before you launch)

Do these in order. Most are quick and online.

### 1.1 Get an ABN (free, ~15 minutes)
- Go to **abr.gov.au** and register an Australian Business Number as a sole trader (or company if you prefer — talk to an accountant if unsure).
- You'll need your ABN to register a **.com.au** domain, so do this first.

### 1.2 Register the business name (~$45/yr)
- At **asic.gov.au**, register "SkyLuxe Media" as your business name (linked to your ABN).
- Quick search first to make sure the name is available.

### 1.3 Get legal to fly commercially (CASA)
This matters — your website says "CASA-accredited" so it must be true before launch.
- For drones **under 2kg** flown commercially, the simplest path is the **excluded category**: register your drone and complete the free online **RPA operator accreditation** at **casa.gov.au** (valid 3 years).
- For heavier drones or fewer flight restrictions, you'd need a **RePL** (Remote Pilot Licence) — a paid course through a CASA-approved training provider.
- Rules change, so confirm the current requirements on casa.gov.au before your first paid job.

### 1.4 Get insured
- **Public liability insurance** for drone operators is essential (many real estate agencies won't hire you without it; $10–20M cover is typical). Search "drone public liability insurance Australia" — providers offer annual or even per-flight policies.
- Consider hull insurance for the drone itself once you're busy.

### 1.5 Money basics
- Open a separate business bank account.
- Set up simple invoicing (Wave is free; Xero/QuickBooks if you want more).
- Note: if you earn over $75k/year you must register for GST.

---

## PART 2 — Domain and email

### 2.1 Buy the domain (~$10–25/yr)
- Recommended: **skyluxemedia.com.au** (you need your ABN for .com.au — that's why Part 1 came first). Also grab **skyluxemedia.com** if available, to protect the name.
- Buy from a registrar like **VentraIP** (Australian), **Namecheap**, or **Cloudflare Registrar**. Avoid heavy upsells — you only need the domain itself.

### 2.2 Set up professional email
Your site lists **hello@skyluxemedia.com.au**, so make it real:
- **Zoho Mail** — free plan, perfectly good to start.
- **Google Workspace** — ~$9/user/month, best long-term (Gmail + Drive under your domain).
- Either one walks you through adding a few DNS records (MX records) at your registrar. Takes ~15 minutes.

---

## PART 3 — Publish the website on Vercel

Your site is in the project folder (`skyluxe-final`). It's a static site — no servers, no monthly hosting cost. Vercel's free plan is more than enough.

### 3.1 First deployment (5 minutes)
1. Go to **vercel.com** → sign up (use GitHub if you have it, or email).
2. Click **Add New → Project**.
3. Drag the entire **skyluxe-final folder** onto the import area.
4. Click **Deploy**. In ~30 seconds you'll have a live URL like `skyluxe-final.vercel.app`. Test it on your phone.

### 3.2 Connect your domain
1. In your Vercel project: **Settings → Domains → Add** → type `skyluxemedia.com.au`.
2. Vercel shows you DNS records. At your registrar's DNS settings, add:
   - **A record**: `@` → `76.76.21.21`
   - **CNAME**: `www` → `cname.vercel-dns.com`
3. Wait 10 minutes–24 hours for DNS to spread. Vercel adds free HTTPS automatically.

### 3.3 Make the contact form actually send (10 minutes)
Right now the form shows a thank-you message but doesn't email you.
1. Sign up free at **formspree.io** → **New Form** → name it "SkyLuxe enquiries" → copy the endpoint URL (looks like `https://formspree.io/f/abcd1234`).
2. Open `index.html` in a text editor and find this line:
   ```html
   <form class="panel" id="cform" novalidate>
   ```
   Change it to:
   ```html
   <form class="panel" id="cform" action="https://formspree.io/f/YOUR_ID" method="POST">
   ```
3. Each input needs a `name` attribute so Formspree labels it. Update them like:
   ```html
   <input id="cn" name="name" type="text" ...>
   <input id="ce" name="email" type="email" ...>
   <input id="cp" name="phone" type="tel" ...>
   <select id="cs" name="service">
   <input id="ca" name="address" type="text" ...>
   <textarea id="cm" name="message" ...>
   ```
4. In the `<script>` near the bottom, find the block starting with `var form=document.getElementById('cform');` and delete that whole `safe(function(){ ... });` block — so the browser submits the form normally to Formspree.
5. Redeploy (see 5.1) and send yourself a test enquiry.

---

## PART 4 — Editing the website yourself

Open `index.html` in **VS Code** (free, code.visualstudio.com) — or any text editor. Everything is in this one file.

### 4.1 Changing text
All wording lives in plain HTML. Search (Ctrl/Cmd+F) for the text you see on screen and edit it. Examples:
- Headline: search `Your world,`
- Prices: search `$250`, `$350`, `$550`
- Phone/email/Instagram: search `hello@skyluxemedia`

### 4.2 Changing colours
At the top of the file inside `<style>`, the `:root{...}` block holds your brand colours:
```css
--amber:#E8862C;      /* main accent (buttons, highlights) */
--terra:#F0633F;      /* secondary warm accent */
--euca:#3F9B6B;       /* green ticks */
```
The sky/landscape colours through the day are in the `<script>` section in the `var KEY=[...]` block — four rows for dawn, midday, golden hour and dusk. Each colour is a normal hex code; change any of them and refresh.

### 4.3 Changing chapter speed
In the script, `SCROLL_PER_SCENE=1.6` controls how much scrolling each chapter takes. Higher = slower, more cinematic; lower = snappier.

### 4.4 Previewing changes locally
Just double-click `index.html` to open it in your browser. Edit → save → refresh.

---

## PART 5 — Updating the live site & a better workflow

### 5.1 The simple way
Repeat the drag-and-drop: Vercel dashboard → your project → **Deployments** → drag the updated folder. New version is live in seconds.

### 5.2 The better way (GitHub auto-deploy)
Worth doing once you're editing regularly:
1. Create a free **github.com** account → **New repository** → name it `skyluxe-site`.
2. Upload your project files (GitHub's web uploader is fine — drag the files in).
3. In Vercel: **Add New → Project → Import** that repository → Deploy.
4. From now on, editing a file on GitHub (or pushing from your computer) automatically republishes the site. You also get full version history.

---

## PART 6 — Adding your real photos (portfolio)

### 6.1 Prepare the images
1. Pick your 6 best aerial shots (or start with 2–3 real ones and keep placeholders for the rest).
2. Resize to about **1600px wide** and compress at **squoosh.app** (free, in-browser) — aim for under **300KB each**. This keeps the site fast.
3. Name them simply: `home.jpg`, `land.jpg`, `construction.jpg`, `airbnb.jpg`, `business.jpg`, `suburb.jpg`.
4. Put them in the project's **assets/portfolio/** folder.

### 6.2 Swap them into the tiles
In `index.html`, find the portfolio section (search `port-grid`). Each tile looks like:
```html
<div class="tile"><div class="art a1"></div><div class="ov"></div>
  <div class="meta"><small>Residential</small><h3>Luxury home at golden hour</h3></div></div>
```
Replace the `<div class="art a1"></div>` line with an image:
```html
<img class="art" src="assets/portfolio/home.jpg" alt="Aerial photo of a luxury Brisbane home at golden hour" style="object-fit:cover;width:100%;height:100%">
```
Repeat for each tile (a1–a6), update the caption text, and write a real `alt` description for each (good for Google too). The hover zoom and overlay keep working automatically.

Do the same for the polaroid in the About section if you like — search `polaroid` and replace its `<div class="ph"></div>` with an `<img class="ph" src="..." style="object-fit:cover">`.

### 6.3 Adding more than 6 tiles
Copy-paste a whole `<div class="tile">...</div>` block and change the image and text. The grid arranges itself.

---

## PART 7 — Adding video

Video files are heavy, so choose the right method:

### Option A — Tiles that play a short clip on the page (best for 5–15s loops)
1. Compress the clip with **HandBrake** (free): 1080p, no audio, target under **6MB**.
2. Save as `assets/portfolio/home.mp4`.
3. Replace a tile's image line with:
```html
<video class="art" src="assets/portfolio/home.mp4" autoplay muted loop playsinline style="object-fit:cover;width:100%;height:100%"></video>
```
`muted` + `playsinline` are required for autoplay on phones. Use at most 1–2 video tiles, or the page gets heavy.

### Option B — Link out to full films (best for 60s+ cinematic work)
1. Upload to **YouTube** (unlisted is fine) or **Vimeo**.
2. Make a tile clickable:
```html
<a class="tile" href="https://youtu.be/YOUR_VIDEO" target="_blank" rel="noopener" style="display:block">
  ...same inner content as other tiles...
</a>
```
Viewers tap the tile and watch the full film. Add a small "▶ Watch the film" in the tile's `<h3>` so it's obvious.

### Option C — Instagram does the work
Since your reels live on Instagram anyway, update the Instagram link in the contact section (search `@skyluxemedia`, change `href="#"` to your real profile URL) and let the portfolio tiles tease the stills.

---

## PART 8 — Get found (SEO & Google)

1. **Google Business Profile** (business.google.com) — free, and the single biggest source of local "drone photographer Brisbane" leads. Add your services, area, photos, and ask early clients for reviews.
2. **Google Search Console** (search.google.com/search-console) — add your domain, verify via DNS, and submit the site so Google indexes it.
3. The site already has good titles and descriptions; once you have real photos, the `alt` text from Part 6 helps too.
4. Put the website link in your Instagram bio, Facebook page, and email signature.

---

## PART 9 — First clients (practical playbook)

1. **Shoot your own portfolio first.** Fly 3–4 free/cheap shoots — a friend's house, a local park, a landmark — so the portfolio is real before you pitch anyone.
2. **Real estate agents:** pick 10 local agencies, find the listing agents on realestate.com.au, and send a short email with 2 of your best shots and your Starter price. Offer the first shoot at a discount in exchange for being added to their supplier list.
3. **Builders:** drive past active construction sites, note the builder names on signage, offer a monthly progress package.
4. **Airbnb hosts:** search stays in scenic spots near you; hosts with mediocre photos are your easiest wins.
5. Reply fast (your site promises it), deliver in 24–48h (it promises that too), and ask every happy client for a Google review.

---

## Quick reference

| Task | Where |
|---|---|
| Edit any text | `index.html` — search for the words you see |
| Brand colours | `:root{}` block at top of the CSS |
| Sky/day colours | `var KEY=[...]` in the script |
| Portfolio images | `assets/portfolio/` + Part 6 |
| Contact form | Formspree — Part 3.3 |
| Update live site | Re-drag folder to Vercel, or GitHub auto-deploy |
| Domain DNS | A `76.76.21.21`, CNAME `cname.vercel-dns.com` |

You're launching with a site most established operators don't have. Good luck up there. 🌅
