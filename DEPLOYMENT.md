# WY Architect Website — Deployment & Handover Guide

## Overview

| Item | Detail |
|---|---|
| Framework | Astro v6 (static output) |
| Styling | Tailwind CSS v4 |
| Fonts | Cormorant Garamond (headings) + DM Sans (body) via Google Fonts |
| Build command | `pnpm build` |
| Output directory | `dist/` |
| Node.js requirement | ≥ 22.12.0 |

---

## 1. Deploying to Cloudflare Pages (Recommended)

### Step 1 — Push to GitHub

1. Create a new GitHub repository (e.g. `wyarchitect-site`)
2. In the project folder, run:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/wyarchitect-site.git
   git push -u origin main
   ```

### Step 2 — Connect to Cloudflare Pages

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Go to **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
3. Select the `wyarchitect-site` repository
4. Configure the build settings:
   - **Framework preset:** Astro
   - **Build command:** `pnpm build`
   - **Build output directory:** `dist`
   - **Node.js version:** 22 (set in Environment Variables: `NODE_VERSION = 22`)
5. Click **Save and Deploy**

### Step 3 — Connect Custom Domain

1. In Cloudflare Pages project → **Custom domains** → **Set up a custom domain**
2. Enter `wyarchitect.com.au` and `www.wyarchitect.com.au`
3. Follow the DNS instructions (add CNAME records pointing to your Pages deployment)

---

## 2. Setting Up the Contact Form (Formspree)

The contact form uses [Formspree](https://formspree.io) — free for up to 50 submissions/month.

1. Sign up at [formspree.io](https://formspree.io)
2. Create a new form and copy the **Form ID** (e.g. `xpwzabcd`)
3. Open `src/pages/contact.astro` and replace `REPLACE_WITH_FORM_ID`:
   ```html
   action="https://formspree.io/f/REPLACE_WITH_FORM_ID"
   ```
   → becomes:
   ```html
   action="https://formspree.io/f/xpwzabcd"
   ```
4. Rebuild and redeploy

---

## 3. Local Development

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

---

## 4. Updating Content

### Adding a New Project Photo
1. Optimise the image (max 1920px wide, JPEG, <500KB recommended)
2. Place it in `public/images/`
3. Reference it in `src/pages/projects.astro`

### Updating Contact Details
Edit `src/layouts/Layout.astro` (footer section) and `src/pages/contact.astro`.

### Updating the Schema
Edit `public/schema.json` to update business details for Google rich results.

---

## 5. File Structure

```
wyarchitect-site/
├── public/
│   ├── images/          ← All project photos + logo
│   ├── schema.json      ← JSON-LD structured data
│   ├── sitemap.xml      ← SEO sitemap
│   ├── robots.txt       ← Search engine directives
│   └── _redirects       ← Cloudflare Pages redirects
├── src/
│   ├── layouts/
│   │   └── Layout.astro ← Global layout (nav + footer)
│   ├── pages/
│   │   ├── index.astro  ← Homepage
│   │   ├── about.astro  ← About page
│   │   ├── services.astro ← Services page
│   │   ├── projects.astro ← Projects gallery
│   │   └── contact.astro  ← Contact page + form
│   └── styles/
│       └── global.css   ← Tailwind + custom CSS
├── astro.config.mjs     ← Astro configuration
└── package.json
```

---

## 6. Post-Launch Checklist

- [ ] Replace `REPLACE_WITH_FORM_ID` in `contact.astro` with real Formspree ID
- [ ] Verify DNS records for `wyarchitect.com.au` and `www.wyarchitect.com.au`
- [ ] Submit sitemap to Google Search Console: `https://www.wyarchitect.com.au/sitemap.xml`
- [ ] Test contact form submission end-to-end
- [ ] Test on mobile devices (iPhone Safari, Android Chrome)
- [ ] Verify all project images load correctly
- [ ] Check that the logo displays in the header and footer

---

*Built by Manus — June 2026*
