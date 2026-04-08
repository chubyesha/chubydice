# Resume Instructions: Chuby Dice V1

**Last Updated:** 2026-04-08
**Previous Session:** Release 2B images, write-ups, and UI/UX refactors
**Project:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1`

---

## Quick Context

Chuby Dice V1 is a **static HTML site (22 pages)** with no build system. All CSS/JS is inline per page. The site uses **Bebas Neue** as the unified font. Design tokens: `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--pink (#E040FB)`.

**V2 exists at:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_2/` — used as design reference only. **DO NOT modify V2.**

---

## Start of Session Checklist

1. Read `documents/SESSION_RECOVERY.md` for full state of completed work
2. Read `README.md` for project structure and feature overview
3. Check `git log --oneline -10` to see recent commits
4. Check `git branch -a` to see all branches
5. **NEVER checkout main/master** — always create feature branches from current HEAD

---

## Current State (as of 2026-04-08)

### What was done this session:

1. **Release 2B images**: 8 PNG flyers optimized to JPEG, deployed to 6 pages
2. **August series renamed**: "Spain Town Badness" → "Survival Story" (new page, old deleted)
3. **Clash flyer images**: Deployed to clash.html, litefeet-v-dancehall.html, krump-v-dancehall.html, homepage tiles
4. **Series write-ups**: Full client-provided content added to Street Vybz, Survival Story, Hot Steppaz, Born Agen
5. **Homepage carousel**: Added 3 missing cards (Praise Flow, Motherland, Dancehall Royalty) — now 7 total
6. **Card UI/UX**: Dark gradient overlay for text readability + V2-style hover highlight (brighten, glow, spring animation)
7. **Glow-line separators**: Replaced ALL plain `border-top` borders with animated golden glow-line across all 22 pages
8. **Academy tile**: V2-style glow border, hover effects, "Launching 2026" pulsing label
9. **Academy shell cards**: 4 cards (Auditions, Scholarships, Curriculum, Vision 2030) in 2x2 grid
10. **Coaching title**: Pink theme color (#E040FB) applied to "1:1 COACHING"
11. **Clash hero**: Title split into 2 rows (gold/white), nav row flex layout (back-link left, date right)

### What's pending:

| Item | Status | Action |
|------|--------|--------|
| Clash write-ups | NOT READY | Wait for Esha to provide Litefeet and Krump text |
| Clash Stripe links | NOT READY | Wait for client to provide Stripe links for clash events |
| Academy card content | NOT READY | Wait for Esha: Auditions, Scholarships, Curriculum, Vision 2030 |
| Acknowledgment of Country | Placeholder | Wait for Esha to provide final text and image |
| Clash runsheet images | Ready | `clash-may-runsheet.jpg` and `clash-august-runsheet.jpg` optimized, deploy when page design finalized |
| `spain-town-badness-flyer.jpg` | Cleanup | Old unused image in `images/`, safe to delete |

---

## Key Design Patterns

### Animated Glow-Line Separator (`.section-sep`)
```css
.section-sep {
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(245,197,24,0.4), rgba(255,255,255,0.15), rgba(245,197,24,0.4), transparent);
  position: relative; overflow: hidden;
}
.section-sep::after {
  content: ''; position: absolute; top: 0; left: -100%;
  width: 60%; height: 100%;
  background: linear-gradient(90deg, transparent, rgba(245,197,24,0.7), rgba(255,255,255,0.6), rgba(245,197,24,0.7), transparent);
  animation: separatorSweep 4s ease-in-out infinite;
}
```
This CSS + `@keyframes separatorSweep` exists in ALL 22 pages. Insert `<div class="section-sep"></div>` between sections.

### Card Hover Effect (`.s-card` on homepage)
- Image: `filter: brightness(1.15)` + `transform: scale(1.04)` on hover
- Card: `translateY(-6px) scale(1.01)` + golden glow box-shadow
- `::before`: golden gradient overlay fades in
- Transition: `cubic-bezier(0.34,1.56,0.64,1)` spring

### Series Card Overlay (`.s-card-overlay`)
4-stop gradient: `rgba(10,10,10,0.05) 0%, 0.2 35%, 0.8 60%, 0.95 100%` — keeps top clear, bottom dark for text.

### Stripe Payment Security
All series pages use immutable `STRIPE_LINKS` object with `new URL()` validation. See `documents/SECURITY_REVIEW_STRIPE_PAYMENT.md` and `documents/STRIPE_LINKS_SHELL_PAGES.md`.

---

## File Reference

### 22 HTML Pages
| Page | Purpose |
|------|---------|
| `index.html` | Homepage (hero, 7-card carousel, clash tiles, academy, coaching, artist, vibes, connect) |
| `series.html` | Series listing with All/Current/Past tabs |
| `praise-flow.html` | April 2026 series |
| `motherland.html` | May 2026 series |
| `dancehall-royalty.html` | June 2026 series |
| `street-vybz.html` | July 2026 series (full write-up) |
| `survival-story.html` | August 2026 series (full write-up, formerly Spain Town Badness) |
| `hot-steppaz.html` | September 2026 series (full write-up) |
| `born-agen.html` | October 2026 series (full write-up) |
| `march-back-in-time.html` | March 2026 (past) |
| `lovers-rock.html` | Past series |
| `full-series.html` | Full collection (past) |
| `past-series.html` | Past events archive |
| `clash.html` | Clash Inna Dancehall overarching + 2 event cards |
| `litefeet-v-dancehall.html` | Clash #1: Litefeet v Dancehall, Sat 23 May |
| `krump-v-dancehall.html` | Clash #2: Krump v Dancehall, Sat 1 Aug |
| `coaching.html` | Professional 1:1 Coaching |
| `academy.html` | Dancehall Academy + 4 shell cards (2x2 grid) |
| `about.html` | About Chuby Dice |
| `contact.html` | Contact / Instagram |
| `in-ya-city.html` | Chuby Dice in Ya City |
| `in-ya-city-adelaide.html` | Adelaide event |

### Key Image Assets
| Image | Size | Used On |
|-------|------|---------|
| `street-vybz-flyer.jpg` | 269KB | street-vybz.html, index.html, series.html |
| `survival-story-flyer.jpg` | 323KB | survival-story.html, index.html, series.html |
| `hot-steppaz-flyer.jpg` | 210KB | hot-steppaz.html, index.html, series.html |
| `born-agen-flyer.jpg` | 226KB | born-agen.html, index.html, series.html |
| `clash-overarching-photo.jpg` | 241KB | clash.html hero |
| `clash-may-photo.jpg` | 297KB | litefeet-v-dancehall.html, clash.html, index.html |
| `clash-august-photo.jpg` | 307KB | krump-v-dancehall.html, clash.html, index.html |
| `clash-may-runsheet.jpg` | 231KB | Not deployed yet |
| `clash-august-runsheet.jpg` | 248KB | Not deployed yet |

### Reference Documents
| Document | Purpose |
|----------|---------|
| `STRIPE_LINKS_SHELL_PAGES.md` | All Stripe payment links, page mapping, JS code |
| `SECURITY_REVIEW_STRIPE_PAYMENT.md` | Security audit + fix instructions |
| `HERO_VIDEO_POSITION_STYLING.md` | `--hero-video-y` CSS tuning (20% sweet spot) |
| `VERTICAL_FLOATING_MENU_SOCIALS.md` | Floating sidebar specs |
| `ANIMATED_GRADIENT_ORBS_BACKGROUND.md` | Orb CSS architecture, z-index stack |

---

## Critical Rules

1. **V1 ONLY** — Do not touch V2 or V2B directories
2. **Never checkout main/master** — Always branch from current HEAD
3. **Bebas Neue only** — No Barlow, no Outfit, no Arial Narrow (V1 uses Bebas Neue exclusively)
4. **No `any` types** — If TypeScript is used, create proper interfaces
5. **Immutable patterns** — Use `Object.freeze()` for payment link whitelists
6. **Image optimization** — Convert PNGs to JPEG: `convert input.png -resize 1200x -quality 85 -strip output.jpg`
7. **Create git branches** — Every change gets its own branch: `feat/`, `fix/`, `docs/`, `chore/`
