# Deploying the Xenia landing page

This folder contains the static landing page for xeniadata.com. Pick one of the two paths below. Both are free.

## Option A — Netlify Drop (simplest, ~5 minutes)

1. Open https://app.netlify.com/drop in your browser.
2. Drag this entire `website/` folder onto the drop zone.
3. Netlify gives you a temporary URL like `random-name-123.netlify.app`. The site is live.
4. To use xeniadata.com instead:
   - In Netlify: Site settings → Domain management → Add custom domain → `xeniadata.com`
   - In Porkbun (xeniadata.com → DNS):
     - Delete any existing A or CNAME records for the root and `www`.
     - Add an A record: host = blank, answer = `75.2.60.5` (Netlify's load balancer)
     - Add a CNAME: host = `www`, answer = `<your-site>.netlify.app`
   - DNS takes 5–30 minutes to propagate.
   - Back in Netlify, enable HTTPS (Let's Encrypt, free, automatic).

## Option B — Cloudflare Pages (best long-term — same provider as Cloudflare Workers/R2/D1)

Since the Xenia infra plan uses Cloudflare for Workers, R2, D1, and Email Routing,
Cloudflare Pages is the natural fit. Requires a Cloudflare account (which D1.B
sets up anyway).

1. In Cloudflare dashboard → Pages → Create a project → Direct upload.
2. Name the project `xeniadata`.
3. Drag the contents of this `website/` folder (not the folder itself — the
   files inside it: `index.html`, `robots.txt`) into the upload area.
4. After deploy, Cloudflare gives you `xeniadata.pages.dev`.
5. To use xeniadata.com:
   - Cloudflare → Pages → xeniadata → Custom domains → Set up a custom domain → `xeniadata.com`
   - Cloudflare automatically configures DNS if xeniadata.com is on Cloudflare's nameservers.
   - If xeniadata.com is still on Porkbun's nameservers (currently true), you have
     two choices:
       - **Easier:** Add a CNAME at Porkbun: host = blank (or `@`), answer = `xeniadata.pages.dev`. (Porkbun supports CNAME flattening for root domains.)
       - **Cleaner long-term:** Move nameservers from Porkbun to Cloudflare. Cloudflare manages all DNS, which makes the rest of D1.B (Email Routing, Workers Routes) much simpler.

## Verification after deploy

Once live, check:

- [ ] `https://xeniadata.com` loads the landing page
- [ ] `https://www.xeniadata.com` redirects to or also loads the page
- [ ] HTTPS shows a valid certificate (green padlock)
- [ ] The page renders on mobile (test on your phone, not just desktop)
- [ ] All footer links (Methodology, Privacy, Terms, DMCA, Crawler) currently 404 — that's expected; they go live when those pages are deployed in D1.B / D2

## Content updates

To change copy on the page, edit `index.html` directly. Then:

- Netlify Drop: re-drag the folder. New deploy replaces the old.
- Cloudflare Pages: re-upload via the dashboard, OR connect to a GitHub repo
  (D1.C creates that repo) and just push commits to trigger auto-deploy.

## What this page does NOT do (intentionally)

- No analytics. Add Plausible or Cloudflare Web Analytics later if needed.
- No newsletter signup or form. Add when there's something to sign up for.
- No claims about features, launch date, pricing, or company facts beyond
  the name and tagline. We avoid making specific commitments until Xenia
  Data, the legal entity, exists.
