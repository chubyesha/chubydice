# Resume Instructions: Chuby Dice V1

**Last Updated:** 2026-04-09
**Previous Sessions:** Release 2B images/write-ups (08 Apr) + Critical corrections for live deployment (09 Apr)
**Project:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1`

---

## Quick Context

Chuby Dice V1 is a **static HTML site (22 pages)** with no build system. All CSS/JS is inline per page. Unified font: **Bebas Neue**. Design tokens: `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--pink (#E040FB)`.

**V2 reference (DO NOT modify):** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_2/`

**Client IA documents:** `screenshots/Info Architecture - RELEASE 2B INFO ARCHITECTURE.docx` and `screenshots/Info Architecture - RELEASE 2B CRITICAL CHANGES CORRECTIONS.docx`

---

## Start of Session Checklist

1. Read `documents/SESSION_RECOVERY.md` for full state
2. Read `README.md` for project structure
3. `git log --oneline -10` for recent commits
4. `git branch -a` for all branches
5. **NEVER checkout main/master** — always create feature branches

---

## Current State (as of 2026-04-09)

### LIVE-READY — All 22 pages verified clean
- No "Esha", "Passion Studio", "Shell — Content TBC", "coming soon", "to be provided" user-facing text
- All write-ups word-for-word from client IA document (verified all 7 pages)
- All clash images are NO PASSION versions (sponsorship changed)

### What's done:
- 7-card homepage series carousel with dark gradient + hover highlight
- Animated glow-line separators across all 22 pages
- All series write-ups (Street Vybz, Survival Story, Hot Steppaz, Born Agen)
- All clash write-ups + artist bios (Phil Eazy with 5 achievements, Antagonize)
- Clash hero: "CLASH INNA" white + "DANCEHALL" blue, no Passion Studio, no May 2026 pill
- Clash event booking cards replaced with "Bookings open 11 April 2026"
- Academy: 4 shell cards in 2x2 grid with production-ready labels
- Coaching: pink theme, enlarged title, no by-line
- Acknowledgment: "We acknowledge the Traditional Custodians..."

### Pending for Release 3 (10 April 2026):
| Item | Status | Action |
|------|--------|--------|
| Clash Stripe payment links | Awaiting Stripe items from client | Replace "Bookings open 11 April" with actual pricing cards |
| Academy card content | Awaiting client | Replace shell card text with actual Auditions/Scholarships/Curriculum/Vision content |
| Acknowledgment update | May be updated | Client may provide revised text |
| Colourful orbs V2→V1 | Per discussion 07/04 | Orbs already on index.html, may need to expand to other pages |
| `spain-town-badness-flyer.jpg` | Unused cleanup | Old image in images/, safe to delete |
| Clash runsheet images | Ready, not deployed | `clash-may-runsheet.jpg`, `clash-august-runsheet.jpg` optimized |

---

## Write-Up Content Sources

**ALL write-ups must be word-for-word from the IA document.** Do not paraphrase, truncate, or reword.

Source file: `screenshots/Info Architecture - RELEASE 2B INFO ARCHITECTURE.docx` → "WRITE-UPS - ESHA TO PROVIDE" section.

| Page | Write-up Status | Verified |
|------|----------------|----------|
| street-vybz.html | Complete (cleared by client) | Word-for-word verified |
| survival-story.html | Complete (corrected per critical doc) | Word-for-word verified |
| hot-steppaz.html | Complete (cleared by client) | Word-for-word verified |
| born-agen.html | Complete (cleared by client) | Word-for-word verified |
| clash.html (About Clash) | Complete | Word-for-word verified |
| litefeet-v-dancehall.html | Complete (Phil Eazy bio + 5 achievements) | Word-for-word verified |
| krump-v-dancehall.html | Complete (Antagonize bio) | Word-for-word verified |

---

## Key Design Patterns

### Glow-Line Separator (`.section-sep`)
Present in ALL 22 pages. Insert `<div class="section-sep"></div>` between sections.

### Card Hover (`.s-card` on homepage)
Image: `brightness(1.15)` + `scale(1.04)`. Card: `translateY(-6px) scale(1.01)` + golden glow. Spring `cubic-bezier(0.34,1.56,0.64,1)`.

### Card Overlay (`.s-card-overlay`)
4-stop: `rgba(10,10,10,0.05) 0%, 0.2 35%, 0.8 60%, 0.95 100%`.

### Clash Title Colors
"CLASH INNA" = `color: var(--white)`, "DANCEHALL" = `color: #00CFFF`

### Stripe Security
Immutable `STRIPE_LINKS` object + `new URL()` validation. See `documents/SECURITY_REVIEW_STRIPE_PAYMENT.md`.

---

## 22-Page Reference

| Page | Purpose |
|------|---------|
| `index.html` | Homepage (hero, 7-card carousel, clash, academy, coaching, artist, vibes, connect) |
| `series.html` | Series listing with All/Current/Past tabs |
| `praise-flow.html` | April 2026 series |
| `motherland.html` | May 2026 series |
| `dancehall-royalty.html` | June 2026 series |
| `street-vybz.html` | July 2026 series (full write-up) |
| `survival-story.html` | August 2026 series (corrected write-up) |
| `hot-steppaz.html` | September 2026 series (full write-up) |
| `born-agen.html` | October 2026 series (full write-up) |
| `march-back-in-time.html` | March 2026 (past) |
| `lovers-rock.html` | Past series |
| `full-series.html` | Full collection (past) |
| `past-series.html` | Past events archive |
| `clash.html` | Clash Inna Dancehall (overarching + 2 event cards) |
| `litefeet-v-dancehall.html` | Clash #1: Phil Eazy & Chuby, Sat 23 May |
| `krump-v-dancehall.html` | Clash #2: Antagonize & Chuby, Sat 1 Aug |
| `coaching.html` | Professional 1:1 Coaching (pink theme) |
| `academy.html` | Dancehall Academy (4 shell cards, 2x2 grid) |
| `about.html` | About Chuby Dice |
| `contact.html` | Contact / Instagram |
| `in-ya-city.html` | Chuby Dice in Ya City |
| `in-ya-city-adelaide.html` | Adelaide event |

---

## Critical Rules

1. **V1 ONLY** — Do not touch V2 or V2B
2. **Never checkout main/master** — Always branch from current HEAD
3. **Bebas Neue only** — No other fonts on V1
4. **Write-ups word-for-word** — Do not paraphrase or truncate client IA content
5. **NO PASSION** — All clash images use NO PASSION versions (sponsorship changed)
6. **Image optimization** — `convert input.png -resize 1200x -quality 85 -strip output.jpg`
7. **Create git branches** — Every change: `feat/`, `fix/`, `docs/`, `chore/`
8. **No under-construction text** — Site is LIVE. No "Esha to provide", "Shell", "coming soon"
