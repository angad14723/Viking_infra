# Vikings Infra Solutions Pvt. Ltd. — Website

A static website (plain HTML/CSS/JS, no build step) for a **geosynthetics /
ground-engineering** company — soil reinforcement, retaining structures, slope
protection, ground improvement and rockfall mitigation. Layout modelled on the
structure of techfabindia.com.

> All product/solution copy is original. The Terrain PDFs supplied during the
> build were used only as reference for which product categories to cover — no
> Terrain wording, product names, photos or client lists are used.

## Pages

| File             | Purpose                                                        |
|------------------|---------------------------------------------------------------|
| `index.html`     | Home — hero, what-we-do, solutions, products, sectors, why-us, standards, CTA |
| `about.html`     | Who we are, mission/vision/values, how we work, capabilities  |
| `solutions.html` | Six engineering applications (retaining, slope, ground, geohazard, pavement, drainage) |
| `products.html`  | Nine product families with anchors (`#geogrid`, `#geocell`, `#gfrp`, …) |
| `sectors.html`   | Eight infrastructure sectors served                          |
| `contact.html`   | Enquiry form + contact details + Google Map                  |

Shared assets:

- `assets/css/style.css` — all styling. **Brand colours live in the `:root` block at the top** (primary is the logo teal `#2E8C9E`).
- `assets/js/main.js` — mobile menu, sticky-header shadow, scroll reveal, footer year, contact-form mailto fallback.
- `assets/img/` — `logo.png` (used in every header/footer), JPG photos for products (`prod-*`), sectors (`sector-*`), solutions and page posters (`*-poster.jpg`). The `ill-*` / `pr-*` SVG illustrations and `logo.svg` are earlier artwork no page currently references. Swap any photo by dropping a JPG in and updating that `<img src>`.
- `assets/video/hero.mp4` — background video in the home hero (720p, ~8 s loop, ~6.5 MB, H.264, no audio). Source: aerial highway-interchange stock clip (`245030_medium.mp4`, transcoded from 2560×1440/54 MB).
- `assets/video/about.mp4` — background of the About page header (`.page-head__media`, ~7 MB, 8 s loop). Source: cable-stayed bridge at sunset (`231167_medium.mp4`). Poster: `about-poster.jpg`.
- `assets/video/solutions.mp4` — background of the Solutions page header (~6.4 MB, 7 s loop, 720p). Source: aerial causeway / dike highway (`370708_medium.mp4`, trimmed from 53 s / 56 MB). Poster: `solutions-poster.jpg`.
- `assets/video/products.mp4` — background of the Products page header (~7 MB, 5 s loop, 720p). Source: aerial concrete arch overpass (`276651_medium.mp4`, trimmed from 15 s / 28 MB). Poster: `products-poster.jpg`.
- `assets/video/sectors.mp4` — background of the Sectors page header (~6.6 MB, 8 s loop, 720p). Source: night city flyover / elevated highway (`19627-304735769_medium.mp4`, trimmed from 16 s / 16 MB). Poster: `sectors-poster.jpg`.
- `assets/video/contact.mp4` — background of the Contact page header (~6.9 MB, 5 s loop, 720p). Source: aerial township / residential development beside a highway (`334921_medium.mp4`, trimmed from 26 s / 70 MB). Poster: `contact-poster.jpg`.
- Every page now has a header/hero video. They use the shared `.page-head__media` block (home uses `.hero__media`) — remove that block from a page to go back to the plain navy gradient.
- All videos are hidden on screens < 700 px and for visitors who prefer reduced motion — the matching `*-poster.jpg` shows instead. Only a neutral (grey) gradient sits over each for text legibility; no colour wash.
- **Confirm every clip's licence permit commercial use** (Pexels/Pixabay/Coverr-style licences do; keep the download pages on file). To replace one, drop in a new `.mp4` and update its poster JPG to a matching frame.

## View it locally

Open `index.html` in a browser, or serve it:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## What still needs your input

Placeholders are in `[SQUARE BRACKETS]` or an orange dashed note box. Find `[` to locate them.

1. **Logo** — `assets/img/logo.png` is wired into every header/footer. Replace it with the final artwork when you have it (keep the filename `logo.png`).
2. **Company identifiers** — `CIN` and `GSTIN` were removed from `contact.html` and every footer (old Balabharti registration numbers). Add Vikings Infra Solutions' real numbers when available.
3. **Photos** — the product/sector/solution images are stock-style JPGs. When you have real project photos, replace them (drop a JPG in `assets/img/`, update the `<img src>`), and we can add a Projects / Case Studies page.
4. **Hero stats** — `9+`, `6`, etc. on the homepage are indicative; adjust to real figures.
5. **Standards strip** — homepage lists ISO 9001 / IRC / MoRTH / IS / ASTM / BIS as *design/spec* references. Add real certificates (and any vendor approvals like NHAI) only if the company actually holds them.
6. **Social links** — LinkedIn / YouTube `href="#"` in every footer.
7. **Product data sheets** — `products.html` says "data sheets available on request"; link real PDFs when ready.

## Contact form → real email

The form currently opens the visitor's email client (zero setup). Once hosted:

- **Netlify Forms** — add `netlify` to the `<form>` tag.
- **Formspree** — set `action="https://formspree.io/f/XXXX"` and `method="POST"`, then remove the `data-contact-form` attribute so `main.js` stops intercepting.

## Deploying — Cloudflare Pages → vikingsinfra.in

The live site is hosted on **Cloudflare Pages** (free, unlimited bandwidth). Every push to `main` redeploys automatically. The domain stays registered at Hostinger; only its nameservers point to Cloudflare.

Deploy config files in the repo root:

- `_headers` — cache rules (assets 30 days, HTML 5 minutes) and basic security headers.
- `_redirects` — keeps `README.md` / `assets/img/README.txt` from being served.
- `robots.txt`, `sitemap.xml` — for search engines.

One-time setup:

1. **Cloudflare** — dash.cloudflare.com → *Add a domain* → `vikingsinfra.in` → Free plan. Delete any imported parking `A` records.
2. **Hostinger** — hPanel → *Domains* → vikingsinfra.in → *DNS / Nameservers* → *Change nameservers* → enter the two Cloudflare nameservers.
3. **Pages project** — Cloudflare → *Workers & Pages* → *Create* → *Pages* → *Connect to Git* → authorise the Cloudflare GitHub app for `Raunak379/Viking_infra`. Production branch `main`, framework preset **None**, build command empty, build output directory `/`.
4. **Custom domains** — project → *Custom domains* → add `vikingsinfra.in` and `www.vikingsinfra.in`.
5. **Redirects / HTTPS** — *Rules* → *Redirect Rules* → template "Redirect from WWW to root"; *SSL/TLS* → *Edge Certificates* → **Always Use HTTPS** on.

Cloudflare Pages serves `about.html` at `/about` (the `.html` URLs redirect there, so existing links keep working). If you add email on the domain later, add its MX/TXT records in Cloudflare DNS, not Hostinger.

## Notes

- Header and footer markup is duplicated in each HTML file (the no-build-step trade-off). Change a nav or footer link → change it in all 6 files.
- `style.css` pulls fonts (Sora + Inter) from Google Fonts via `@import`; offline it falls back to system fonts.
- Responsive to ~360px; works without JavaScript except the mobile menu, scroll reveal and the form helper.
