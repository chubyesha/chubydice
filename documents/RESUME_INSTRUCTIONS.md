# Resume Instructions — Chuby Dice Website

**For the next Claude Code session to continue where this one left off.**

---

## Quick Start

1. Read this file, then `documents/SESSION_RECOVERY.md` for full context.
2. **Two repositories** exist side-by-side:
   - V1: `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1` → `git@github.com:chubyesha/chubydice.git`
   - V2: `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_2` → `git@github.com:chubyesha/chubydice_v2.git`
3. Check branch: `git branch --show-current` in each repo.
4. PRD document: `documents/Info Architecture - RELEASE 2 08022026.docx` (parse with python-docx).
5. Stripe links document: `documents/Info Architecture - RELEASE 2 STRIPE WORKING NOTES.docx`.

---

## Project Context

- **Client:** Chuby Dice — Dancehall artist/educator in Melbourne, Australia
- **Live URL:** https://www.chubydice.com
- **Tech:** Static HTML, inline CSS/JS, no build tools, 16 pages per version
- **V1 Design:** Barlow + Bebas Neue fonts, `--yellow`/`--black`/`--dark` tokens
- **V2 Design:** Outfit + DM Sans fonts, purple spectrum tokens, `shared-theme.css`

## What Was Completed

**ALL client requirements are DONE across both versions (13/13 V1 + 11/11 V2).**

Key implementations:
- Horizontal swipe carousel with full-image background cards (home + series pages)
- Countdown badges ("Starts in X days") on series cards
- "Dis an Dat" collapsible submenu on all 16 pages (both versions)
- Live Stripe links (5 tiers + coaching) on series sub-pages
- Archived pages (lovers-rock, full-series, in-ya-city-adelaide) have Stripe disabled
- Academy: "DANCEHALL ACADEMY" title, "Out of many, one" byline, flames hero
- Coaching: 60vh hero, subtitle removed, expandable accordion
- About: 6-section biography accordion
- Adelaide event flyer image on in-ya-city.html + in-ya-city-adelaide.html
- HD Entertainment branding (not BBK Productions)
- All fonts unified, headings consistent

## Patterns to Follow

### Nav Menu (Dis an Dat)
All 16 pages have independent nav. Batch update with Python script. Structure:
- 7 main links + "Dis an Dat" collapsible group (Contact, Brand Ambassadorship, Past Events)
- Requires: `.menu-group-toggle`, `.menu-group-items` CSS + `toggleSubMenu()` JS

### Carousel
- CSS: `display: flex; overflow-x: auto; scroll-snap-type: x mandatory; cursor: grab;`
- Cards: `flex: 0 0 min(44%, 340px); scroll-snap-align: start;`
- JS: mousedown/mousemove/mouseup for drag-to-scroll
- Past cards: `.s-past-badge` watermark, muted opacity

### Stripe Links
- Sub-pages (praise-flow, motherland, dancehall-royalty): `data-link` per pricing option + `selectPrice()` + `bookNow()` with URL validation
- series.html: direct `window.open` on pricing card buttons
- Archived pages: `alert('Session ended...')`

### Accordion
- CSS: `.acc-item.open .acc-body { max-height: 500px; }` with `overflow: hidden; transition`
- JS: click toggles `.open` class, single-open behavior

## Critical Warnings

- **NEVER checkout main/master** — work on feature branches only
- **NEVER git stash** — erases current changes
- **Two repos** — commit to the correct one (V1 vs V2)
- **Nav menus duplicated** across 16 files — any change must hit ALL pages
- **JS truncation bug** — watch for missing closing braces in script blocks (was the root cause of broken menus on 4 pages)
- **Countdown badges** — dates are hardcoded in `data-start` attributes, update when series change

## File Quick Reference

| Need to... | File(s) |
|------------|---------|
| Update nav menu | All 16 `.html` files (batch script) |
| Add/modify series | `series.html`, `index.html`, new sub-page |
| Update coaching | `coaching.html` |
| Update biography | `about.html` |
| Modify chatbot | `chatbot.js`, `netlify/functions/chat.js` |
| Add Stripe links | Series sub-pages + `series.html` pricing section |
| Update images | `images/` directory, update refs in HTML |
