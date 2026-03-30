# Resume Instructions — Chuby Dice Website

**For the next Claude Code session to continue where this one left off.**

---

## Quick Start

1. **Read this file first**, then `documents/SESSION_RECOVERY.md` for full context.
2. **Checkout the correct branch:** `git checkout feat/release-2a-product-requirements`
3. **Verify you're on the right commit:** `git log --oneline -3` — should show `90fdb08 feat: implement Release 2A product requirements` at HEAD
4. **Check no pablobbk101 files:** There should be NO `shared-theme.css`, NO `images/hero-poster.jpg`, NO `videos/hero-bg.mp4`. If these exist, you're on the wrong branch.
5. **Read the PRD:** `screenshots/Info Architecture - RELEASE 2 08022026.docx` (parse with python-docx)

---

## Critical Context

**The client REJECTED the `/pablobbk101-cloud/chubydice` redesign.** All work must be on the original codebase (Barlow/Bebas Neue fonts, `--yellow`/`--black`/`--dark` design tokens, 5 rotating hero videos). Do NOT merge or reference branches:
- `feat/pablobbk101-cloud-chubydice-changes`
- `feat/release-2a-requirements`

The correct active branch is: **`feat/release-2a-product-requirements`** (based on `00b0168`)

---

## Project Context

- **Project:** Chuby Dice — static HTML website for a Dancehall artist/educator in Melbourne
- **Live URL:** https://www.chubydice.com
- **Hosting:** Netlify (auto-deploys from GitHub)
- **Repo:** `git@github.com:chubyesha/chubydice.git`
- **Tech:** Static HTML, inline CSS/JS per page, no build tools, no shared CSS file
- **Design:** Dark theme with Barlow + Bebas Neue fonts, CSS custom properties (`--yellow`, `--black`, `--dark`, `--pink`, `--border`)

## What Was Completed (Release 2A)

All 7 product requirements implemented on `feat/release-2a-product-requirements`:

1. **Stripe pricing** on `series.html` — 5 tiers ($30/$100/$125/$230/$450), placeholder buttons
2. **Nav menus** standardized across 16 pages (added Clash, Brand Ambassadorship, 2026 Events)
3. **Hero images** — verified `motherland.png` and `dancehall-royalty.png` are in place
4. **Coaching hero** — verified `5015f87ce59f.png` is correct
5. **Hero video** — keeping 5 rotating videos, PRD said "potential" change only
6. **Coaching accordion** — 5 expandable items with content and toggle JS
7. **About accordion** — 6 collapsible biography sections, first open by default

## What Still Needs To Be Done

### Immediate (Client-Dependent)
- **Stripe payment links:** Client needs to create Stripe items for 5 class packages. Replace `data-stripe` placeholder buttons in `series.html` with `onclick="window.open('https://buy.stripe.com/...','_blank')"`. Remove `.pending` class, change text to "Buy Now".
- **New hero images:** If client provides updated flyers for Motherland (May) and Dancehall Royalty (June), replace `images/motherland.png` and `images/dancehall-royalty.png`
- **New hero video:** If client provides a specific video, replace `videos/1.mp4` or add as new rotation

### Future Work (Release 2B — Purple in PRD)
- Clash Inna Dancehall pricing (workshop + clash passes)
- Terms & Conditions page
- Brand Ambassadorship dedicated page (currently links to contact.html)

## Key Patterns

### Nav Menu Updates
16 HTML files have independent nav menus. Use Python batch script:
```python
# Pattern: find menuOverlay div, replace inner links, set active per page
# See SESSION_RECOVERY.md for the exact script used
```

### Accordion Pattern (coaching.html, about.html)
- CSS: `.acc-item.open .acc-body { max-height: 500px; }` with `overflow: hidden; transition: max-height 0.35s ease;`
- HTML: `<div class="acc-header"><span>Title</span><svg class="acc-arrow">...</svg></div><div class="acc-body"><p>Content</p></div>`
- JS: Click handler toggles `.open` class, single-open (closes others)

### Stripe Link Pattern
Existing: `onclick="window.open('https://buy.stripe.com/...','_blank')"`
New pricing cards: `data-stripe` attributes for future wiring

## Critical Warnings

- **NEVER checkout main/master** — work only on feature branches
- **NEVER use pablobbk101 branches** — client rejected that redesign
- **NEVER git stash** — it erases current changes
- **Nav menus duplicated** across 16 files — changes must hit ALL pages
- **No build tools** — HTML/CSS/JS changes take effect immediately
- **Test on mobile** — breakpoints at 900px and 640px

## File Quick Reference

| Need to... | File(s) |
|------------|---------|
| Update nav menu | All 16 `.html` files |
| Add/modify series | `series.html`, `index.html`, new sub-page |
| Update coaching | `coaching.html` |
| Update biography | `about.html` |
| Modify chatbot | `chatbot.js`, `netlify/functions/chat.js` |
| Add Stripe links | Series sub-pages + `series.html` pricing section |
