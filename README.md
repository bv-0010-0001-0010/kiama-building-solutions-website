# kiamabuildsol.com.au

Static website for **Kiama Building Solutions Pty Ltd** (ABN 92 689 628 180),
Croydon South VIC. Plain HTML, CSS and JavaScript — no build step, no framework,
no dependencies to keep updated.

---

## What's in here

```
├── index.html            Home
├── services.html         Renovations, kitchens/bathrooms, new builds, outdoor living
├── projects.html         Project types + permits & compliance
├── workforce.html        Hire a crew (builders) / Join our crew (tradespeople)
├── about.html            Company, director, values, safety & quality
├── contact.html          Enquiry form (quote, crew hire, job seeker, general)
├── privacy.html          Privacy policy
├── terms.html            Terms of use
├── 404.html              Not found
├── css/style.css         All styling. Brand colours are CSS variables at the top.
├── js/main.js            Nav, scroll reveal, form submit  ← paste your form URL here
├── assets/                Favicons, social share image (logo is inline SVG in every page)
├── apps-script/           Contact-form backend + setup guide
├── sitemap.xml            Submit this to Google Search Console
├── robots.txt
└── vercel.json            Clean URLs, redirects, cache and security headers
```

The logo is the client-supplied Kiama artwork, used exactly as provided — stored as
`assets/kiama-logo.svg` (a tightly-cropped vector copy; `kiama-logo-original.svg` is
the untouched source file) and referenced from every page as a single `<img
class="brand-logo">`, so it's crisp at any size, loads fast, and stays pixel-identical
everywhere it appears. `assets/favicon.svg` is a separate crop of just the icon mark
(no wordmark) for the browser tab, pinned tiles and app icon. `assets/kiama-logo.png`
is a high-resolution raster render of the same artwork, used for the og-image and the
letterhead.

To swap in a different logo revision later, replace `kiama-logo.svg` — the website
itself just needs that one file, since every page loads it via
`<img src="/assets/kiama-logo.svg">` rather than embedding it. You'll also want to
re-rasterise it to PNG (e.g. with the `sharp` npm package, at a few thousand pixels
wide) to refresh `assets/favicon.svg`, the favicons, `og-image.png`, and the letterhead
in the separate `Kiama Building Solutions - Letterhead` folder (see its own README).

---

## Deploying to Vercel

1. Create a new GitHub repository, e.g. `kiama-building-solutions-website`.
2. Push this folder to it:
   ```bash
   git init
   git add .
   git commit -m "Kiama Building Solutions website"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/kiama-building-solutions-website.git
   git push -u origin main
   ```
3. In Vercel: **Add New → Project → Import** the repo.
4. Framework preset: **Other**. Leave build command and output directory empty —
   it's a static site.
5. **Deploy.**

Every push to `main` redeploys automatically.

## Pointing the Hostinger domain at Vercel

In Vercel: **Project → Settings → Domains → Add** `kiamabuildsol.com.au`, then add
`www.kiamabuildsol.com.au` as well. Vercel will show you the records to create.

In Hostinger: **Domains → kiamabuildsol.com.au → DNS / Nameservers → DNS records**:

| Type | Name | Value |
|---|---|---|
| A | `@` | `76.76.21.21` |
| CNAME | `www` | `cname.vercel-dns.com` |

Use whatever values Vercel displays — they occasionally change. Delete any
conflicting existing A or CNAME records for `@` and `www`. DNS usually takes
15–60 minutes; the SSL certificate is issued automatically and free.

Set `www.kiamabuildsol.com.au` as the primary domain in Vercel so it matches the
canonical URLs already in the HTML.

## Connecting the contact form

See **`apps-script/SETUP.md`**. Short version: create a Google Sheet, paste
`apps-script/Code.gs` into script.google.com, deploy as a web app with access set
to *Anyone*, then paste the resulting URL into line 10 of `js/main.js`.

Until you do that, the form shows a message saying it isn't connected yet. You can
set this up today with your personal Gmail and switch the notification address to
`admin@kiamabuildsol.com.au` once Google Workspace is active on the domain — just
change `NOTIFY_TO` in `apps-script/Code.gs` and redeploy the Apps Script version.

---

## SEO — everything here is free

Already built in:

- Unique title and meta description on every page
- Canonical URLs, Open Graph and Twitter card tags
- JSON-LD structured data (`GeneralContractor` + `HomeAndConstructionBusiness`, with
  your ABN, address, opening hours and service areas), plus breadcrumbs on inner pages
- Semantic headings, one `<h1>` per page, descriptive link text
- `sitemap.xml` and `robots.txt`
- Fast: no framework, no tracking scripts, cached assets

### What to do after launch

1. **Google Search Console** (free) — <https://search.google.com/search-console>.
   Verify the domain, then submit `https://www.kiamabuildsol.com.au/sitemap.xml`.
2. **Bing Webmaster Tools** (free) — <https://www.bing.com/webmasters>. You can
   import straight from Search Console.
3. **Google Business Profile** (free) — <https://business.google.com>. For a local
   building business this moves the needle more than anything on the website. Use
   the exact same business name, address and phone number as the footer here.
4. **Free local directories** — True Local, Yellow Pages free listing, Hotfrog,
   Oneflare, hipages (worth a paid profile too, once you're busy).
5. **PageSpeed Insights** (free) — <https://pagespeed.web.dev>. This site should
   score well out of the box; check again once you add real project photos.

### Keywords the pages already target

`home renovations eastern Melbourne`, `builder Croydon South`, `house extensions
Ringwood`, `kitchen renovations Maroondah`, `new home builds Yarra Ranges`,
`construction labour hire Melbourne east`.

---

## Adding photos

The design works without photography, which is why it currently ships without any.
When you have real project photos:

1. Drop them in `assets/` as `.webp` or `.jpg`, around 1600px wide, under 300KB.
2. Add them to a section, e.g. inside `index.html`:
   ```html
   <img src="/assets/kitchen-croydon.jpg" alt="Completed kitchen renovation, Croydon South"
        width="1600" height="900" loading="lazy" class="chamfer">
   ```

Use your own photos of real completed work. Stock images of staged interiors read
as fake to anyone shopping around, and licensed stock has its own costs and
restrictions.

---

## Changing brand colours

Everything derives from CSS variables at the top of `css/style.css`, sampled directly
from the logo artwork:

```css
--clay:  #FF730B;   /* orange — sampled from "KIAMA" in the logo */
--slate: #123333;   /* dark teal-ink — derived from the logo's teal */
--paper: #F6F9F8;   /* cool background */
```

Change those three and the whole site follows — buttons, links, the logo mark, the
hero pattern and the footer all read from them.

---

## Before you go live — checklist

- [ ] Apps Script URL pasted into `js/main.js`
- [ ] Test enquiry submitted, row appears in the Sheet, emails arrive
- [ ] Google Workspace set up for `kiamabuildsol.com.au`, then switch `admin@` over
      in `apps-script/Code.gs`
- [ ] Domain connected in Vercel, `www` set as primary, HTTPS working
- [ ] Sitemap submitted to Google Search Console
- [ ] Google Business Profile created and verified
- [ ] Privacy policy and terms reviewed by a lawyer (they're templates, not advice)
- [ ] Footer disclaimer reviewed by a lawyer
- [ ] Business details double-checked: ABN 92 689 628 180, 0424 059 638,
      156 Eastfield Road, Croydon South VIC 3136
