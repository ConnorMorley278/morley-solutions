# Products Page & Navigation — Design Spec

**Date:** 2026-06-02
**Owner:** Connor Morley
**Status:** Approved

## Goal

Add a hamburger nav drawer and a Products page to the existing Morley Solutions LLC static site. Each product links to a Stripe Payment Link for upfront card payment with shipping address collection. No backend required.

## Constraints

- Static site on GitHub Pages — no server-side code.
- No product images — text-only cards.
- Free shipping built into product price (no shipping line item at checkout).
- Stripe handles payment, quantity selection, shipping address, and receipt emails.
- Adding new products = paste a Stripe Payment Link URL into one new card in `products.html`. No other changes.

---

## Navigation — Hamburger Drawer

### Trigger
A hamburger button (☰) sits **left of the logo** in the header on all pages. Present on both `index.html` and `products.html`.

### Behaviour
- Clicking ☰ opens a left-side drawer that slides in over the page content.
- A semi-transparent overlay covers the rest of the page.
- Clicking the overlay, pressing Escape, or clicking a nav link closes the drawer.
- Drawer contains two links: **Home** (`index.html`) and **Products** (`products.html`).
- Active page link is visually highlighted (deep blue, bold).

### Implementation
- CSS: `position: fixed` drawer, `transform: translateX(-100%)` when closed, `translateX(0)` when open. CSS transition `0.25s ease`. Overlay is a fixed full-screen `<div>` with `opacity: 0` / `pointer-events: none` toggled via a class.
- JS: ~30 lines of vanilla JS in a `<script>` tag at the bottom of each page (no external file needed). Toggles a class on `<body>` (`nav-open`). No framework.
- No `<script src>` file to maintain — inline in each page.

### Header layout change
Current: `[logo]`
New: `[☰]  [logo]`

Header becomes flex row, align-center, gap 16px.

---

## Products Page (`products.html`)

### URL
`products.html` — accessible at `https://connormorley278.github.io/morley-solutions/products.html`

### Structure (top → bottom)
Same header (with hamburger) and footer as `index.html`.

**Page title section:**
- `<h1>` — "Products"
- Short subtitle — "Browse our catalogue and place an order directly through our secure checkout."

**Product grid:**
- CSS Grid, 2 columns on desktop (≥600px), 1 column on mobile.
- Gap: 24px.
- Each card: border `1px solid #e2e8f0`, border-radius 12px, padding 28px, white background.

### Product card structure
```
┌─────────────────────────────┐
│  Product Name (h2, 20px)    │
│  Description (p, muted)     │
│                             │
│  $XX.XX per unit            │
│                             │
│  [  Order Now  ]            │
└─────────────────────────────┘
```

- **Name:** `<h2>`, 20px, font-weight 700, near-black `#0f172a`
- **Description:** `<p>`, 15px, muted `#64748b`, 2–3 sentences max
- **Price:** `<p>`, 16px, font-weight 600, deep blue `#1e3a8a`
- **Button:** `<a class="btn-order" href="[STRIPE_PAYMENT_LINK]" target="_blank" rel="noopener">Order Now</a>` — deep blue bg, white text, rounded, full-width on mobile

### Button styles
- Background: `#1e3a8a`
- Text: white, font-weight 600, 15px
- Padding: 12px 24px
- Border-radius: 8px
- Hover: `#1e40af` (slightly lighter blue)
- Display: `inline-block`

### Placeholder card (for initial deploy)
One placeholder card is included at launch:
- Name: "Product Name"
- Description: "Product description goes here. Update this card with your real product details and Stripe Payment Link."
- Price: "$0.00 per unit"
- Button href: `#` (disabled visually — `pointer-events: none`, muted colour)

This is replaced when real products are added.

---

## Stripe Integration

### Per-product setup (done in Stripe Dashboard — not code)
1. Stripe Dashboard → **Payment Links** → **+ New**
2. Add product → set name, price per unit
3. Enable **"Let customers adjust quantity"** — yes
4. Under **Shipping** → Add shipping rate → set to **$0.00 Free shipping**
5. Under **Customer information** → require **Shipping address** — yes
6. Click **Create link** → copy the `buy.stripe.com/...` URL
7. Paste URL as `href` in the relevant card in `products.html`

### What Stripe handles automatically
- Quantity selection (customer types how many)
- Shipping address form (required, cannot be skipped)
- Card payment (all major cards, Apple/Google Pay)
- Receipt email to customer
- Order notification email to the Stripe account owner (Connor)
- Payment record + customer profile in Stripe Dashboard

### Viewing orders
Log into **dashboard.stripe.com** → Payments or Customers. All orders, shipping addresses, and payment history are there. No backend needed.

---

## Files Changed

| File | Change |
|---|---|
| `index.html` | Add hamburger button + nav drawer HTML + inline JS |
| `products.html` | New file — products grid page |
| `styles.css` | Add: nav drawer styles, overlay, hamburger button, product card styles, btn-order styles |

No other files touched.

---

## Responsive behaviour

| Viewport | Products grid | Header |
|---|---|---|
| ≥600px | 2 columns | ☰ + logo inline |
| <600px | 1 column | ☰ + logo inline (logo shrinks as before) |

---

## Out of scope

- Product images
- Shopping cart (multi-product orders)
- Invoicing / net-terms payment
- Customer login / approval gating
- Order tracking / fulfilment workflow
- Search or filter on products page
