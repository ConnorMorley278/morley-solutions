# Morley Solutions LLC Website — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a public single-page website for Morley Solutions LLC on GitHub Pages at `https://connormorley278.github.io/morley-solutions/`.

**Architecture:** Static site — `index.html` + `styles.css` + two SVG assets. No build step, no framework, no JavaScript. Deployed via GitHub Pages from `main` branch root.

**Tech Stack:** HTML5, CSS3, SVG, GitHub Pages, `git` + `gh` CLI.

**Source spec:** `docs/superpowers/specs/2026-05-26-morley-solutions-website-design.md`

**Verification model:** No automated tests (static brochure site). Each task includes manual verification steps. Each task ends with a commit.

---

## File Structure

After this plan, the repo will contain:

```
morley-solutions/
├── .gitignore               (already exists)
├── .nojekyll                (new — empty; opts out of Jekyll processing)
├── README.md                (new — one-paragraph repo description)
├── index.html               (new — the page)
├── styles.css               (new — all styling)
├── assets/
│   ├── logo.svg             (new — copied from logo-export/logo.svg)
│   └── favicon.svg          (new — copied from logo-export/logo-square.svg)
├── logo-export/             (already exists — kept for personal use, not served)
└── docs/                    (already exists — spec + plan)
```

The `logo-export/` folder is not part of the served site but lives in the same repo for convenience. Nothing references it from `index.html`.

---

## Working directory

All commands assume cwd is `C:\Users\javan\Documents\Connor-AI\morley-solutions` (Windows Git Bash syntax shown). Use absolute paths where shown.

---

### Task 1: Create site asset folder and copy logos

**Files:**
- Create: `assets/logo.svg` (copy of `logo-export/logo.svg`)
- Create: `assets/favicon.svg` (copy of `logo-export/logo-square.svg`)

- [ ] **Step 1: Create assets folder**

Run:
```bash
mkdir -p assets
```

- [ ] **Step 2: Copy the wide logo SVG into assets**

Run:
```bash
cp logo-export/logo.svg assets/logo.svg
```

- [ ] **Step 3: Copy the square logo SVG into assets as favicon**

Run:
```bash
cp logo-export/logo-square.svg assets/favicon.svg
```

- [ ] **Step 4: Verify the two files exist and are non-empty**

Run:
```bash
ls -la assets/
```

Expected: `logo.svg` and `favicon.svg` both present, each ~500-700 bytes.

- [ ] **Step 5: Commit**

```bash
git add assets/logo.svg assets/favicon.svg
git commit -m "Add site logo and favicon SVG assets"
```

---

### Task 2: Add `.nojekyll` and `README.md`

**Files:**
- Create: `.nojekyll` (empty file — disables Jekyll on GitHub Pages so files starting with `_` are served as-is)
- Create: `README.md`

- [ ] **Step 1: Create `.nojekyll`**

Run:
```bash
touch .nojekyll
```

- [ ] **Step 2: Create `README.md` with this exact content**

Write file `README.md`:
```markdown
# Morley Solutions LLC

Source for [morleysolutions GitHub Pages site](https://connormorley278.github.io/morley-solutions/) — a one-page brochure for Morley Solutions LLC.

Plain HTML + CSS. No build step.
```

- [ ] **Step 3: Commit**

```bash
git add .nojekyll README.md
git commit -m "Add README and .nojekyll for GitHub Pages"
```

---

### Task 3: Write `styles.css`

**Files:**
- Create: `styles.css`

This file contains all visual styling per the spec's tokens (white background, near-black text, deep-blue accent `#1e3a8a`, system sans-serif, max content width 720px, responsive at 600px).

- [ ] **Step 1: Write `styles.css` with this exact content**

```css
/* Morley Solutions LLC — site styles */

:root {
  --color-bg: #ffffff;
  --color-heading: #0f172a;
  --color-body: #334155;
  --color-muted: #64748b;
  --color-rule: #f1f5f9;
  --color-accent: #1e3a8a;
  --max-width: 720px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  -webkit-text-size-adjust: 100%;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
  font-size: 17px;
  line-height: 1.6;
  color: var(--color-heading);
  background: var(--color-bg);
}

a {
  color: var(--color-accent);
  text-decoration: none;
  font-weight: 500;
}

a:hover,
a:focus-visible {
  text-decoration: underline;
}

/* Header */
.site-header {
  padding: 32px 48px 24px;
  border-bottom: 1px solid var(--color-rule);
}

.site-header__logo {
  display: block;
  width: 240px;
  max-width: 100%;
  height: auto;
}

/* Hero */
.hero {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 80px 32px 96px;
}

.hero__eyebrow {
  margin: 0 0 16px;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--color-accent);
}

.hero__title {
  margin: 0 0 28px;
  font-size: 44px;
  line-height: 1.15;
  font-weight: 700;
  letter-spacing: -0.5px;
  color: var(--color-heading);
}

.hero__body {
  margin: 0 0 20px;
  font-size: 19px;
  color: var(--color-body);
}

.hero__body:last-child {
  margin-bottom: 0;
}

/* Footer */
.site-footer {
  padding: 32px 48px;
  border-top: 1px solid var(--color-rule);
  text-align: center;
  font-size: 14px;
  color: var(--color-muted);
}

.site-footer__sep {
  margin: 0 8px;
  color: var(--color-rule);
}

/* Responsive */
@media (max-width: 600px) {
  .site-header {
    padding: 24px 20px 20px;
  }

  .site-header__logo {
    width: 200px;
  }

  .hero {
    padding: 48px 20px 64px;
  }

  .hero__title {
    font-size: 32px;
  }

  .hero__body {
    font-size: 17px;
  }

  .site-footer {
    padding: 24px 20px;
  }
}
```

- [ ] **Step 2: Commit**

```bash
git add styles.css
git commit -m "Add site stylesheet"
```

---

### Task 4: Write `index.html`

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write `index.html` with this exact content**

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Morley Solutions LLC — Process automation & remote digital services</title>
  <meta name="description" content="Morley Solutions LLC helps companies automate repetitive processes and provides remote digital assistance.">
  <link rel="icon" type="image/svg+xml" href="assets/favicon.svg">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <header class="site-header">
    <img class="site-header__logo" src="assets/logo.svg" alt="Morley Solutions LLC">
  </header>

  <main class="hero">
    <p class="hero__eyebrow">Morley Solutions LLC</p>

    <h1 class="hero__title">Automating the work that gets in your way.</h1>

    <p class="hero__body">
      Morley Solutions LLC helps companies automate repetitive processes and provides remote digital assistance &mdash; freeing teams to focus on the work that matters.
    </p>

    <p class="hero__body">
      Whether it's streamlining a workflow, integrating tools that don't talk to each other, or handling the back-office tasks that pile up, we get it done remotely and reliably.
    </p>
  </main>

  <footer class="site-footer">
    Primary contact: Connor Morley
    <span class="site-footer__sep">|</span>
    <a href="mailto:cmorleytechservices@gmail.com">cmorleytechservices@gmail.com</a>
  </footer>

</body>
</html>
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "Add index.html with hero copy and contact footer"
```

---

### Task 5: Local browser verification

No code changes — this is a manual smoke test before publishing.

- [ ] **Step 1: Open `index.html` in your default browser**

Run (Git Bash on Windows):
```bash
start index.html
```

- [ ] **Step 2: Visually verify**

Check each:
- Header shows the Morley Solutions logo, left-aligned, with the deep-blue gradient on "SOLUTIONS".
- A thin grey line sits below the header.
- Hero section shows: uppercase "MORLEY SOLUTIONS LLC" eyebrow in deep blue → large headline "Automating the work that gets in your way." → two body paragraphs.
- Footer shows: "Primary contact: Connor Morley | cmorleytechservices@gmail.com" with the email as a blue link.
- The favicon (small square logo) appears in the browser tab.

- [ ] **Step 3: Click the `mailto:` link in the footer**

Expected: your default mail client opens with a new message addressed to `cmorleytechservices@gmail.com`. Cancel out without sending.

- [ ] **Step 4: Test responsive layout**

In the browser, open devtools (F12), toggle device toolbar (Ctrl+Shift+M), set width to 375px. Expected:
- Logo shrinks (~200px wide).
- Headline drops to ~32px font.
- Content remains in one column, no horizontal scroll.

Set width to 1280px and verify it looks the same as the desktop default.

- [ ] **Step 5: Fix any issues, then proceed**

If something looks wrong, edit `index.html` or `styles.css`, reload the browser, and commit fixes with a clear message like `Fix mobile padding on hero`. Only proceed to Task 6 once the local site looks correct.

No commit needed for this task unless fixes were made.

---

### Task 6: Create the GitHub repo and push

**Tooling:** GitHub CLI (`gh`) is already installed on this machine (verified earlier in `which gh`).

- [ ] **Step 1: Confirm `gh` is authenticated**

Run:
```bash
gh auth status
```

Expected: shows you are logged in as `ConnorMorley278` (or similar) with `repo` scope. If not, run `gh auth login` and follow the prompts (choose GitHub.com → HTTPS → authenticate via web browser).

- [ ] **Step 2: Verify current local git state**

Run:
```bash
git status
git log --oneline
```

Expected: working tree clean, several commits visible (spec + the tasks above).

- [ ] **Step 3: Create the public repo and push `main` in one command**

Run:
```bash
gh repo create ConnorMorley278/morley-solutions --public --source=. --remote=origin --push
```

Expected output:
- "✓ Created repository ConnorMorley278/morley-solutions on GitHub"
- Several lines of git push progress
- A URL to the new repo

- [ ] **Step 4: Verify the remote is set and the push succeeded**

Run:
```bash
git remote -v
gh repo view --web
```

Expected: `origin` points to `https://github.com/ConnorMorley278/morley-solutions.git`, and the browser opens the new repo page showing the files.

No commit needed for this task.

---

### Task 7: Enable GitHub Pages

- [ ] **Step 1: Enable Pages from `main` branch root via `gh`**

Run:
```bash
gh api -X POST repos/ConnorMorley278/morley-solutions/pages \
  -f "source[branch]=main" \
  -f "source[path]=/"
```

Expected: JSON response containing `"html_url": "https://connormorley278.github.io/morley-solutions/"` and `"status": null` or `"queued"`.

If the command fails with "Pages already enabled," that's fine — proceed.

- [ ] **Step 2: Wait for the first build**

GitHub Pages typically takes 30-90 seconds for the first deploy. Check status:

```bash
gh api repos/ConnorMorley278/morley-solutions/pages/builds/latest
```

Repeat until `"status": "built"` appears.

- [ ] **Step 3: Open the live URL**

Run:
```bash
start https://connormorley278.github.io/morley-solutions/
```

Expected: the same page you verified locally, now served from GitHub Pages over HTTPS.

If you get a 404 instead, wait another minute and refresh — GitHub Pages DNS can take a moment.

No commit needed for this task.

---

### Task 8: Live verification

- [ ] **Step 1: Repeat the visual checks from Task 5, Step 2, against the live URL**

Confirm logo, header divider, hero text, footer, favicon, and `mailto:` link all work on the live site.

- [ ] **Step 2: Test the live site on a phone**

Open `https://connormorley278.github.io/morley-solutions/` on your phone. Confirm the page reads cleanly, no horizontal scroll, and the email link opens your phone's mail app.

- [ ] **Step 3: Validate HTML (optional but quick)**

Visit `https://validator.w3.org/nu/?doc=https%3A%2F%2Fconnormorley278.github.io%2Fmorley-solutions%2F` — expected: "Document checking completed. No errors or warnings to show."

If validation reports errors, fix `index.html` and push (`git add index.html && git commit -m "Fix HTML validation" && git push`). Wait ~1 minute for Pages to redeploy.

- [ ] **Step 4: Final commit (only if any live-only fixes were needed)**

If no fixes were made in Step 3, nothing to commit. The site is live.

---

## Done criteria

- [ ] The live URL `https://connormorley278.github.io/morley-solutions/` returns HTTP 200 and renders the expected page.
- [ ] The page passes the manual checks in Task 5 and Task 8.
- [ ] The repo at `https://github.com/ConnorMorley278/morley-solutions` is public.
- [ ] All commits are pushed to `main`.

---

## Rollback / change procedure

For any future content edit (typo, new tagline, etc.):

1. Edit `index.html` or `styles.css` locally.
2. `git add ... && git commit -m "..." && git push`.
3. Wait ~30-60 seconds.
4. Refresh the live URL.

No build step. No Pages reconfiguration needed unless changing the domain.
