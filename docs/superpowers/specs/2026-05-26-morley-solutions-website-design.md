# Morley Solutions LLC — Website Design

**Date:** 2026-05-26
**Owner:** Connor Morley
**Status:** Approved (pending user review of this spec)

## Goal

Publish a public, single-page website that briefly explains what Morley Solutions LLC does and provides a contact email. Hosted free on GitHub Pages.

## Constraints

- Must be public.
- Must be hosted on GitHub.
- Keep it basic — no marketing fluff, no JavaScript apps, no CMS.
- No third-party dependencies (no Google Fonts, no analytics, no frameworks).
- Maintainable by editing two text files.

## Architecture

Static single-page site, served by GitHub Pages.

```
morley-solutions/                       (GitHub repo, public)
├── index.html                          single page
├── styles.css                          all visual styling
├── assets/
│   ├── logo.svg                        primary header logo (vector)
│   └── favicon.svg                     square version for browser tab
├── README.md                           one-paragraph repo description
└── .nojekyll                           opt out of Jekyll processing
```

- No build step. No JS. No framework.
- Files served directly from the `main` branch root.

**Hosting**

- GitHub user: `ConnorMorley278`
- Repo: `ConnorMorley278/morley-solutions` (public)
- GitHub Pages: source = `main` branch, `/` (root)
- Live URL: `https://connormorley278.github.io/morley-solutions/`
- No custom domain (can be added later by adding a `CNAME` file).

## Page structure

Top-to-bottom, all in `index.html`:

1. **Header** — left-aligned logo (`<img src="assets/logo.svg" alt="Morley Solutions LLC">`); ~32px top/bottom padding; thin bottom divider.
2. **Hero** — centered content column, max-width 720px:
   - Eyebrow label: "Morley Solutions LLC" in deep blue, uppercase, letter-spaced.
   - H1 tagline: **"Automating the work that gets in your way."**
   - Paragraph 1: *"Morley Solutions LLC helps companies automate repetitive processes and provides remote digital assistance — freeing teams to focus on the work that matters."*
   - Paragraph 2: *"Whether it's streamlining a workflow, integrating tools that don't talk to each other, or handling the back-office tasks that pile up, we get it done remotely and reliably."*
3. **Footer** — full-width, top divider, centered text, ~14px font, muted color:
   > Primary contact: Connor Morley | <cmorleytechservices@gmail.com>
   The email is a `mailto:` link in deep blue.

## Visual design

| Token | Value |
|---|---|
| Background | `#ffffff` |
| Body text | `#111` (heading) / `#334155` (paragraphs) / `#64748b` (footer) |
| Accent / deep blue | `#1e3a8a` |
| Accent / light blue (gradient end) | `#60a5fa` |
| Body font | System sans-serif stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif` |
| Max content width | 720px |
| Hero vertical padding | 80px top / 96px bottom |

### Logo (final, approved)

- Two-line wordmark: **"Morley"** (700, 38px, near-black) and **"SOLUTIONS"** (700, 28px, letter-spaced 3px) with a horizontal gradient from `#1e3a8a` → `#60a5fa`.
- Mark: a continuous `/\/\` zigzag of two equal-height triangle peaks (deep blue, 6px stroke, rounded joins) placed to the left of the wordmark. The mark's vertical midpoint aligns with the gap between "Morley" and "SOLUTIONS".
- Master SVG: `logo.svg` (wide) and `logo-square.svg` (square favicon variant).
- Asset exports already produced in `logo-export/` (PNGs at 512/1024/2048, white + transparent, wide + square) for personal use; the website itself uses the SVG masters.

### Responsiveness

- Single column always. No layout switching needed.
- Hero padding shrinks on narrow viewports (`@media (max-width: 600px)`: padding 48px 20px, H1 32px).
- Logo scales down with a CSS `max-width` cap.

## Error handling

- 404 handled by GitHub Pages default page (acceptable for a one-page site). Optional improvement later: add a `404.html`.
- No forms, no JS — nothing else can fail at runtime.

## Testing

- **Local preview:** open `index.html` directly in Edge/Chrome (no server required). Confirm header, hero, footer render correctly.
- **Responsive check:** browser devtools at 375px, 768px, 1280px widths.
- **Link check:** click the `mailto:` link; confirm it opens default mail client with the right address.
- **Live deployment check:** after pushing and enabling Pages, wait ~1 minute, load the live URL on phone and desktop, confirm same render.

## Out of scope

- Contact form, CAPTCHA, anti-spam.
- Analytics.
- Custom domain (deferred — easy to add later).
- Blog, services pages, case studies.
- Dark mode.
- Multi-language.

## Files to create / change

- `index.html` (new)
- `styles.css` (new)
- `assets/logo.svg` (new — copy of approved `logo-export/logo.svg`)
- `assets/favicon.svg` (new — copy of approved `logo-export/logo-square.svg`)
- `README.md` (new — one short paragraph)
- `.nojekyll` (new — empty file)

## Deployment steps (summary — full sequence will be in the implementation plan)

1. Create local project folder `Documents/Connor-AI/morley-solutions/` (already exists).
2. Author the files listed above.
3. `git init`, initial commit on `main`.
4. `gh repo create ConnorMorley278/morley-solutions --public --source=. --push`.
5. Enable GitHub Pages via `gh api` or the web UI: source = `main`, path = `/`.
6. Wait ~1 minute, verify live URL.
