# Milos Pro — WhatsApp Landing Page

Static, single-page landing optimized for Meta / Instagram ads that drive traffic to WhatsApp. Bilingual (EN / ES) with automatic language detection based on the device locale, plus manual toggle.

## What's inside

```
milos-lp/
├── index.html          ← The entire landing page (HTML + CSS + JS inline)
├── public/
│   └── images/         ← Optimized WebP images (full + -sm variants)
├── vercel.json         ← Static hosting config + cache headers
├── robots.txt
├── .gitignore
└── README.md
```

No build step, no framework, no node_modules. Drop it on any static host.

## Key features

- **Mobile-first** — designed for IG/Meta ad traffic
- **One CTA** — every button leads to WhatsApp; no nav distractions
- **Auto language detection** — uses `navigator.language` (or `?lang=es` / `?lang=en` URL param to force)
- **UTM preservation** — UTM/fbclid/gclid params from the ad get appended to the WhatsApp message so attribution stays intact
- **Floating WhatsApp button** — appears after scrolling past the hero
- **Optimized images** — WebP, lazy-loaded, ~5 MB total page weight
- **No tracking dependencies out of the box** — placeholders ready for Meta Pixel / GA in `index.html`

## Configuration

Open `index.html` and find the `===== CONFIG =====` section near the bottom:

```js
const WHATSAPP_NUMBER = '17866945349';
```

Replace with the business WhatsApp number in E.164 format (country code + number, **no `+`, no spaces, no dashes**).

To add Meta Pixel or Google Analytics, uncomment and fill in the `fbq` / `gtag` lines inside the click tracker at the bottom of the script.

## Deploy to Vercel

### Option A — via GitHub (recommended)

1. Create a new repo on GitHub (e.g. `milos-pro-landing`).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Milos Pro WhatsApp LP"
   git branch -M main
   git remote add origin https://github.com/<your-user>/milos-pro-landing.git
   git push -u origin main
   ```
3. Go to [vercel.com/new](https://vercel.com/new) → Import the repo.
4. Framework preset: **Other** (it's a plain static site).
5. Leave build/output settings empty. Deploy.
6. Add a custom domain in Vercel → Settings → Domains (e.g. `go.milosprogates.com`).

### Option B — Vercel CLI

```bash
npm i -g vercel
vercel       # follow the prompts
vercel --prod
```

## Ad URL examples (with tracking)

When linking from Meta ads, append UTM parameters. They will be automatically attached to the WhatsApp message:

```
https://yourdomain.com/?utm_source=ig&utm_medium=paid_social&utm_campaign=gates_oct&utm_content=video_a
```

Force language:

```
https://yourdomain.com/?lang=es
https://yourdomain.com/?lang=en
```

## Local preview

Any static server works. E.g.:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Maintenance

- **Update copy** → edit `index.html` directly. EN text is inside `<span data-lang-en>` and ES text inside `<span data-lang-es>`.
- **Swap an image** → drop the new file in `public/images/` keeping the same filename, then commit & push. Vercel redeploys automatically.
- **Add a service area** → duplicate one of the `.area-tag` divs and update the city name.

---

Built for performance, SEO and conversion. Lighthouse should score 95+ across the board on mobile.
