# Filter Tabs & Card Format — Design Spec

**Date:** 2026-06-02
**Owner:** Connor Morley
**Status:** Approved

## Goal

Update `products.html` to: (1) use SKU as card name with SKU removed from description, (2) rename nav link to "Products / Services", (3) add tab-style filter above the grid, (4) tag each card with a data-category attribute.

## Constraints

- Static site — no backend, no page reload on filter.
- Filter is pure JS class toggle.
- Two-column grid already exists in CSS; no grid changes needed.

---

## Changes

### 1. Card format rule (applied to existing card + all future cards)

| Field | Content |
|---|---|
| `product-card__name` | SKU only — e.g. `OP-LCR4348RTC` |
| `product-card__desc` | Full description — no SKU repeated |
| `product-card__price` | Price as before |
| `data-category` | `"product"` or `"service"` on the `.product-card` div |

**Existing card update:**
- Name: `OP-LCR4348RTC`
- Description: `Coreless roll, star seal, 10×10 pack. Clear 45-gallon can liners. 100 liners per case.` (SKU removed)
- Add `data-category="product"` to the card div

### 2. Nav drawer label

In both `index.html` and `products.html`, change the Products drawer link text:

```html
<a href="products.html">Products / Services</a>
```

(Active class stays as-is on each respective page.)

### 3. Filter tabs

**HTML** — inserted between `.products-header` and `.products-grid`:

```html
<div class="filter-tabs" role="group" aria-label="Filter by category">
  <button class="filter-tab active" data-filter="all">All</button>
  <button class="filter-tab" data-filter="product">Products</button>
  <button class="filter-tab" data-filter="service">Services</button>
</div>
```

**Behaviour:**
- On page load: "All" tab is active, all cards visible.
- Clicking a tab: sets `active` class on that tab, removes from others. Hides cards whose `data-category` doesn't match (or shows all if "All"). Uses `display: none` to hide.
- JS is inline in `products.html` — appended to the existing IIFE or as a second `<script>` block.

**CSS — filter tab styles (added to `styles.css`):**

```css
.filter-tabs {
  max-width: 960px;
  margin: 0 auto;
  padding: 0 32px 24px;
  display: flex;
  gap: 8px;
}

.filter-tab {
  background: none;
  border: 1px solid #cbd5e1;
  border-radius: 20px;
  padding: 6px 18px;
  font-size: 14px;
  font-weight: 500;
  color: var(--color-muted);
  cursor: pointer;
  transition: background 0.15s, color 0.15s, border-color 0.15s;
}

.filter-tab:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}

.filter-tab.active {
  background: var(--color-accent);
  border-color: var(--color-accent);
  color: #ffffff;
}

@media (max-width: 600px) {
  .filter-tabs {
    padding: 0 20px 20px;
  }
}
```

**JS — filter logic (added to `products.html` inline script):**

```javascript
(function () {
  var tabs = document.querySelectorAll('.filter-tab');
  var cards = document.querySelectorAll('.product-card');

  tabs.forEach(function (tab) {
    tab.addEventListener('click', function () {
      var filter = tab.getAttribute('data-filter');

      tabs.forEach(function (t) { t.classList.remove('active'); });
      tab.classList.add('active');

      cards.forEach(function (card) {
        if (filter === 'all' || card.getAttribute('data-category') === filter) {
          card.style.display = '';
        } else {
          card.style.display = 'none';
        }
      });
    });
  });
})();
```

### 4. Template comment update

The `TO ADD A REAL PRODUCT` comment in `products.html` must be updated to reflect the new card format:

```html
<!--
  TO ADD A PRODUCT OR SERVICE — copy this block:

  <div class="product-card" data-category="product">   ← or data-category="service"
    <h2 class="product-card__name">SKU-OR-CODE-HERE</h2>
    <p class="product-card__desc">Description here. No SKU needed — it's in the name above.</p>
    <p class="product-card__price">$XX.XX / unit</p>
    <a class="btn-order" href="https://buy.stripe.com/YOUR_LINK_HERE" target="_blank" rel="noopener">Order Now</a>
  </div>
-->
```

---

## Files Changed

| File | Change |
|---|---|
| `products.html` | Update existing card (name=SKU, no SKU in desc, add data-category). Add filter tabs HTML. Add filter JS. Update template comment. |
| `index.html` | Update nav drawer Products link text to "Products / Services" |
| `styles.css` | Add filter tab styles |

---

## Out of scope

- Animated card hide/show (fade transitions)
- Persisting filter state across page loads
- More than two categories
