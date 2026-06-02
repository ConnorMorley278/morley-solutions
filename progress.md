# Morley Solutions LLC website — progress log

**Status:** ✅ Shipped 2026-05-27

## Live links

- **Site:** https://connormorley278.github.io/morley-solutions/
- **Repo:** https://github.com/ConnorMorley278/morley-solutions (public)

## What was built

A static single-page brochure site for Morley Solutions LLC, hosted on GitHub Pages.

- `index.html` — header (logo) + hero (eyebrow, headline, two paragraphs) + footer (contact / Kentucky, USA / © 2026)
- `styles.css` — deep-blue accent (`#1e3a8a`), system sans-serif, max-width 720px, responsive at 600px
- `assets/logo.svg` — wide logo with gradient on SOLUTIONS
- `assets/favicon.svg` — square logo variant for browser tab
- `.nojekyll`, `README.md` — GitHub Pages scaffolding

## Approved design decisions

- **Logo:** Concept B1 (continuous `/\/\` zigzag + two-line wordmark). Final v3: peaks at original size, "SOLUTIONS" weight 700 with `#1e3a8a` → `#60a5fa` gradient, peaks vertically centered with the inter-line gap.
- **Copy:**
  - Eyebrow: "MORLEY SOLUTIONS LLC" (22px, bold, deep blue)
  - Headline: "Automating the work that gets in your way." (38px)
  - Para 1: original description verbatim
  - Para 2: added — workflow integration / back-office angle
- **Footer:** contact line, location ("Kentucky, USA"), copyright

## Logo exports (personal use)

Located in `logo-export/`. Wide and square variants at 512 / 1024 / 2048, each in white-background and transparent. SVG masters: `logo.svg`, `logo-square.svg`.

## Legal disclosures included

- Copyright: © 2026 Morley Solutions LLC
- Jurisdiction: Kentucky, USA

Confirmed not required for a static brochure site with no forms / analytics / e-commerce: privacy policy, terms, business address, registered agent, EIN, cookie banner.

## Repo specifics

- Branch: `main`
- Default `gh repo create … --public --push` flow used
- Pages source: `main` branch, root path (`/`)
- HTTPS enforced

## Future edits

1. Edit `index.html` or `styles.css` locally
2. Commit and push to `main` (current `settings.json` blocks `git push * main*` — temporarily relax for the push, then restore; or use a feature branch + PR)
3. Wait 30-60s, refresh the live URL

## Spec & plan

- Design spec: `docs/superpowers/specs/2026-05-26-morley-solutions-website-design.md`
- Implementation plan: `docs/superpowers/plans/2026-05-26-morley-solutions-website.md`
- Products page spec: `docs/superpowers/specs/2026-06-02-products-page-design.md`
- Products page plan: `docs/superpowers/plans/2026-06-02-products-page-nav-drawer.md`

## Change log

- **2026-06-02:** Added hamburger nav drawer (all pages) and Products page with placeholder card. Stripe Payment Link instructions in `products.html` comments. Commit `5c6f419`. Live at `/products.html`.
- **2026-05-27:** Added a third hero paragraph inviting prospective clients to reach out. Commit `f5495c3`. Live.

## Adding products (when ready)

1. In Stripe Dashboard → Payment Links → + New. Add product, enable quantity adjustment, set $0.00 free shipping, require shipping address. Copy the `buy.stripe.com/...` URL.
2. In `products.html`, copy the `TO ADD A REAL PRODUCT` comment block, fill in name/description/price/Stripe URL, paste it inside `.products-grid`.
3. Delete the placeholder card once you have at least one real product.
4. Commit and push (same push procedure).

## Out of scope (deferred)

- Custom domain (e.g. `morleysolutions.com`) — would need domain purchase + `CNAME` file + DNS records
- Search engine submission to Google Search Console
- Analytics, contact form
- Shopping cart (multi-product orders)
- Customer login / approval gating
