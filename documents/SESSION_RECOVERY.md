# Session Recovery — Chuby Dice Website

**Last Updated:** 2026-04-01
**V1 Path:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1`
**V2 Path:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_2`

---

## Session Summary

This session implemented the client's Release 2A product requirements and subsequent "final changes" across both Version 1 (original Barlow/Bebas theme) and Version 2 (Outfit/DM Sans purple theme). Client rejected the pablobbk101-cloud redesign — all work was done on the original V1 codebase.

---

## V1 Commits (chubydice_version_1 → git@github.com:chubyesha/chubydice.git)

### Release 2A Implementation
- `90fdb08` — Nav standardization (16 pages), pricing section, coaching accordion, about accordion
- `e86f09c` — Wire live Stripe payment links (5 tiers) to all series pages
- `ef1d6cd` → `14325f4` — Series.html carousel with current + past tabs, drag-to-scroll
- `33f9748` — Center dropdown menu below MENU button
- Various image updates: coaching-hero.jpg, motherland-may-2026.jpg, dancehall-royalty-june-2026.jpg, academy-tile-bg.jpg, academy-hero.jpg

### Client Final Changes (feat/client-final-changes-v1)
- `12e2b22` — Home page: carousel, collection pack button, countdown badges, academy text, playlist text, title sizes
- `514f259` — Academy hero position (flames), one-line title, coaching hero 60vh
- `36da83c` — Dis an Dat grouped submenu on all 16 pages

### Carousel & Image Fixes
- `d09f7df` → `a1cf163` — Home carousel: portrait cards → full-image background cards with visible countdown badges
- `4234e18` — Dis an Dat vertical stack alignment
- `493714d` + `09cb862` — Adelaide In Ya City image on both in-ya-city-adelaide.html and in-ya-city.html
- `13d06c6` — Fix menu dropdown broken JS on 4 pages (truncated script blocks)

### Stripe Links (Live)
- Single $30: `buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b`
- 4 Classes $100: `buy.stripe.com/6oUbJ16033xgeRYfRB4F20c`
- 5 Classes $125: `buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d`
- 10 Classes $230: `buy.stripe.com/eVqdR97473xg25ccFp4F20e`
- 20 Classes $450: `buy.stripe.com/9B6fZhagj0l4fW28p94F20f`
- Coaching $120: `buy.stripe.com/3cIbJ17470l4cJQ34P4F209`
- Archived: lovers-rock, in-ya-city-adelaide, full-series (show "Session Ended")

---

## V2 Commits (chubydice_version_2 → git@github.com:chubyesha/chubydice_v2.git)

- `847c8b1` — Academy + coaching images from client assets
- `372810b` — Hero eyebrow text, remove glitch, smaller title, consistent headings, carousel
- `54543bf` — Dis an Dat nav on all 16 pages, academy/coaching fixes
- `c548423` — Playlist text: CDDA PLAYLIST
- `0e4df5b` — Dis an Dat dropdown fix (toggleSubMenu JS + vertical stack)
- `aa2f5e3` — Carousel swiping on home + series page
- `e23e088` — Portrait cards, full-image backgrounds, coaching centered, countdown badges
- `a37fd36` — Coaching card centered
- `80fbee3` + `a82584b` — Adelaide image on in-ya-city-adelaide.html + in-ya-city.html
- `02ec7ab` — Fix menu dropdown broken JS on 4 pages

---

## All Client Requirements — Final Status

### V1 (13/13 DONE)
| # | Requirement | Status |
|---|------------|--------|
| 1 | Home page carousel (full-image cards, swipe) | DONE |
| 2 | Series Collection Pack button (home + series) | DONE |
| 3 | Countdown badges (Starts in X days) | DONE |
| 4 | In Ya City Adelaide carousel/image | DONE |
| 5 | Academy image flames in frame | DONE |
| 6 | Academy: "DANCEHALL ACADEMY" + "Out of many, one" | DONE |
| 7 | Academy sub-page title one line | DONE |
| 8 | Meet Chuby Dice one line | DONE |
| 9 | Dis an Dat submenu (all 16 pages) | DONE |
| 10 | Clash/Coaching titles bigger + matching | DONE |
| 11 | CDDA Playlist | DONE |
| 12 | Coaching hero shorter (60vh) + subtitle removed | DONE |
| 13 | Adelaide In Ya City image | DONE |

### V2 (11/11 DONE)
| # | Requirement | Status |
|---|------------|--------|
| 1 | Eyebrow: "Home of Chuby Dice Series & Australia's Dancehall Academy" | DONE |
| 2 | Remove glitch animation | DONE |
| 3 | Chuby Dice font smaller & one line | DONE |
| 4 | Consistent heading sizes (clamp 2.2-3.8rem) | DONE |
| 5 | Carousel for home + series page | DONE |
| 6 | All titles/tiles match V1 | DONE |
| 7 | Dis an Dat submenu | DONE |
| 8 | Adelaide image | DONE |
| 9 | Coaching card centered | DONE |
| 10 | Countdown badges | DONE |
| 11 | Portrait cards with full-image backgrounds | DONE |

---

## Images Added This Session
- `images/coaching-hero.jpg` (324KB) — 1:1 Coaching flyer
- `images/motherland-may-2026.jpg` (162KB) — May series flyer
- `images/dancehall-royalty-june-2026.jpg` (223KB) — June series flyer
- `images/academy-tile-bg.jpg` (514KB) — Jamaican flag texture
- `images/academy-hero.jpg` (362KB) — Fire breather performance
- `images/adelaide-in-ya-city.jpg` (204KB) — Adelaide workshop flyer

---

## Mobile UX Optimization (2026-04-03)

### V1 (fix/mobile-optimization branch, commit e5523d3)
- All 16 pages: Enhanced mobile CSS with WCAG 2.5.5 tap targets (min 44px)
- Breakpoints added: 480px (small phones), 360px (smallest devices)
- Common: nav sizing, menu overlay width, footer stacking, social icons
- Page-specific: index (hero, tiles, carousel, artist), series (pricing 1-col), coaching (accordion, banner), about (mosaic, bio), sub-pages (pricing cards, hero)

### V2 (fix/mobile-optimization branch, commit 0c28c8d)
- shared-theme.css: Global mobile responsive rules (768px, 480px, 360px)
- All 16 pages: Page-specific mobile CSS blocks
- index.html: Animated orb sizes reduced at 640px to prevent overflow

---

## Release 2B — chubydice_version_2b (2026-04-03)

**Path:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_2b`
**Branch:** `feat/release-2b` (commit `bf42aa2`)
**PRD:** `screenshots/Info Architecture - RELEASE 2 B.docx`

### Architecture
- 5 external CSS: shared-theme.css (tokens), components.css (nav/footer/buttons/cards), carousel.css, hero.css, utilities.css (animations/breakpoints)
- 3 external JS: nav.js (menu/submenu), carousel.js (drag-swipe/dots/countdown), reveal.js (IntersectionObserver)
- CSS custom properties for design tokens (purple/gold theme from V2)
- Responsive breakpoints: 1024px, 768px, 480px, 360px + prefers-reduced-motion

### Pages (15 total)
- **index.html** — Hero, series carousel (4 new), clash section (2 events), coaching CTA, academy tile, artist, playlist, connect, acknowledgment of country, footer
- **series.html** — All series cards carousel + 5-tier pricing grid
- **street-vybz.html, spain-town-badness.html, hot-steppaz.html, born-agen.html** — Shell detail pages with placeholder image/text/Stripe
- **clash.html** — 2-column grid (Litefeet May, Krump July)
- **litefeet-v-dancehall.html, krump-v-dancehall.html** — Shell detail pages with Stripe placeholders
- **coaching.html** — 3 coaching cards ($120/$440/$800) with Stripe placeholders
- **academy.html, about.html, in-ya-city.html, contact.html, past-series.html** — Carry-forward pages

### Placeholder Strategy
- `Shell` = `.placeholder-image` (gradient bg with series name)
- `Image` = placeholder awaiting client assets
- `Write-up` = `.placeholder-text` (dashed border, italic)
- `Stripe links` = `.btn-stripe-placeholder` (disabled with "Coming Soon" badge)

---

## Known Pre-existing Issues (Not In Scope)
1. Broken OG image meta tags (`chuby-profile-CkJq2sVN.jpg` doesn't exist)
2. CORS wildcard on Netlify chat function
3. Chat function: no input validation or rate limiting
4. V2 `shared-theme.css` uses `!important` on body font-family
