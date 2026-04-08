# Chuby Dice Website (Version 1)

Official website for **Chuby Dice** — Dancehall artist, educator, and cultural practitioner based in Naarm (Melbourne), Australia.

**Live site:** [chubydice.com](https://www.chubydice.com)
**Hosting:** Netlify
**Repo:** [github.com/chubyesha/chubydice](https://github.com/chubyesha/chubydice)
**Version 2:** [github.com/chubyesha/chubydice_v2](https://github.com/chubyesha/chubydice_v2)

---

## Project Structure

```
chubydice_version_1/
├── index.html                  # Home page (hero video, series carousel, clash tiles, academy, coaching, artist, vibes, connect)
├── series.html                 # Chuby Dice Series — swipe carousel (current + past) + collection pricing
├── praise-flow.html            # Praise Flow series (April 2026) — per-tier Stripe checkout
├── motherland.html             # Motherland series (May 2026) — per-tier Stripe checkout
├── dancehall-royalty.html       # Dancehall Royalty series (June 2026) — per-tier Stripe checkout
├── street-vybz.html            # Street Vybz series (July 2026) — with full write-up content
├── survival-story.html         # Survival Story series (August 2026, formerly Spain Town Badness)
├── hot-steppaz.html            # Hot Steppaz series (September 2026) — with full write-up content
├── born-agen.html              # Born Agen series (October 2026) — with full write-up content
├── march-back-in-time.html     # March Back in Time series (March 2026, past)
├── lovers-rock.html            # Lovers' Rock series (past, Stripe disabled)
├── full-series.html            # Full series collection page (past, Stripe disabled)
├── past-series.html            # Past Events archive
├── clash.html                  # Clash Inna Dancehall with Passion Studio (overarching + 2 events)
├── litefeet-v-dancehall.html   # Litefeet v Dancehall — Clash #1, Sat 23 May 2026
├── krump-v-dancehall.html      # Krump v Dancehall — Clash #2, Sat 1 Aug 2026
├── coaching.html               # Professional 1:1 Coaching & Programs (60vh hero, accordion)
├── academy.html                # Dancehall Academy (flames hero, 4 shell cards: Auditions, Scholarships, Curriculum, Vision 2030)
├── about.html                  # About Chuby Dice (biography accordion, 6 sections)
├── contact.html                # Contact / Instagram / Brand Ambassadorship
├── in-ya-city.html             # Chuby Dice in Ya City (Adelaide card with image)
├── in-ya-city-adelaide.html    # In Ya City — Adelaide (event flyer hero)
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers (optimized JPEGs)
├── videos/                     # Hero background videos (1-5.mp4)
├── documents/                  # Session recovery, resume instructions, reference guides
└── .gitignore
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Inline `<style>` and `<script>` per page.
- **Font** — Bebas Neue (unified across all 22 pages).
- **Design Tokens** — `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--dark (#111111)`, `--pink (#E040FB)`, `--border (#242424)`.
- **Netlify Functions** — Serverless chat at `/.netlify/functions/chat` (Anthropic Claude API).
- **Stripe** — Live payment links for 5 class pass tiers + coaching. Archived pages disabled.

## Key Features

### Home Page (`index.html`)
- Full-screen hero video with `object-position: center 20%` sweet spot
- **7-card horizontal swipe carousel** (Praise Flow → Born Agen) with:
  - Full-image backgrounds with dark gradient overlay for text readability
  - V2-style hover highlight (image brightens, golden glow, spring animation)
  - Client-provided series by-lines and descriptions
- **Clash Inna Dancehall** section with 2 event tiles (flyer images, event details)
- **Dancehall Academy** tile with golden glow border, pulsing "Launching 2026" label
- **Professional 1:1 Coaching** tile with pink (#E040FB) theme accent
- **Animated glow-line separators** between all sections (replaces plain borders)
- Floating social sidebar, animated gradient orbs background
- "Meet Chuby Dice" artist section, Chuby's Playlist, Social connect

### Series Pages (7 shell pages)
- Hero with optimized flyer images (200-323KB JPEGs, from 11-17MB PNGs)
- Full write-up content from client's "Info Architecture" document
- Sub-headings and structured content (Survival Story has "Spanish Town & Other Hardcore Crews", "Dancehall as Witness and Weald")
- 5-tier Stripe pricing with immutable payment link whitelist and URL validation

### Clash Pages
- `clash.html` — Overarching page with hero (clash-overarching-photo.jpg), two-row title layout, flex nav row
- `litefeet-v-dancehall.html` — Sat 23 May 2026, Phil Eazy & Chuby Dice
- `krump-v-dancehall.html` — Sat 1 Aug 2026, Antagonize & Chuby Dice

### Academy Page (`academy.html`)
- Flames-in-frame hero with "Launching June 2026" label
- 4 shell template cards in **2x2 grid** layout: Auditions, Scholarships, Curriculum, Vision 2030
- Golden border, gradient bg, hover lift + glow effects
- Responsive: 2-col desktop, 1-col mobile (480px)

### Sub-Pages
- **Coaching** — 60vh hero, expandable 5-item accordion, Stripe booking, pink theme
- **About** — Photo mosaic hero, 6 collapsible biography accordion sections
- **Adelaide** — Event flyer hero image (client-provided)

## Navigation (Dis an Dat)

All 22 pages share a standardized dropdown with collapsible "Dis an Dat" submenu:

1. Home
2. Chuby Dice Series
3. Clash Inna Dancehall
4. Professional 1:1 Coaching & Programs
5. Dancehall Academy
6. About Chuby Dice
7. Chuby Dice in Ya City
8. **Dis an Dat** (collapsible):
   - Contact / Instagram
   - Brand Ambassadorship
   - Past Events

## Stripe Pricing (Live)

| Package | Price | Per Class | Stripe Link Suffix |
|---------|-------|-----------|-------------------|
| Single Class | $30 | $30 | `...5cX4F20b` |
| 4 Classes | $100 | $25 | `...fRB4F20c` |
| 5 Classes | $125 | $25 | `...bBl4F20d` |
| 10 Classes | $230 | $23 | `...cFp4F20e` |
| 20 Classes | $450 | $22.50 | `...8p94F20f` |
| 1:1 Coaching | $120 | — | `...4P4F209` |

**Archived** (Stripe disabled): lovers-rock.html, in-ya-city-adelaide.html, full-series.html

## UI/UX Design System

### Animated Glow-Line Separator
All section borders use `.section-sep` — a 1px golden gradient line with a sweeping white/gold highlight animation (4s infinite loop). Replaces plain `border-top` across all 22 pages.

### Card Hover Effects
Series cards and Academy tile use V2-adapted hover: image brightens (`filter: brightness(1.15)`), scales (`1.04`), golden glow box-shadow (`0 0 36px rgba(245,197,24,0.18)`), spring `cubic-bezier(0.34,1.56,0.64,1)`.

### Section Theme Colors
| Section | Accent Color |
|---------|-------------|
| Chuby Dice Series | Yellow `#F5C518` |
| Clash Inna Dancehall | Cyan `#00CFFF` |
| Dancehall Academy | Yellow `#F5C518` |
| Professional Coaching | Pink `#E040FB` |

## Development

```bash
npx serve .              # Static server
npx netlify dev          # With Netlify Functions (chatbot)
python3 -m http.server   # Alternative
```

## Git Workflow

- **main** — Production. Never checkout or merge directly.
- `feat/<desc>`, `fix/<desc>`, `docs/<desc>`, `chore/<desc>` — Feature branches.

## Documents Reference

| Document | Purpose |
|----------|---------|
| `documents/SESSION_RECOVERY.md` | Current session state for continuity |
| `documents/RESUME_INSTRUCTIONS.md` | Quick-start guide for new sessions |
| `documents/STRIPE_LINKS_SHELL_PAGES.md` | Stripe payment links reference |
| `documents/SECURITY_REVIEW_STRIPE_PAYMENT.md` | Security audit findings |
| `documents/HERO_VIDEO_POSITION_STYLING.md` | Hero video CSS tuning guide |
| `documents/VERTICAL_FLOATING_MENU_SOCIALS.md` | Floating sidebar reference |
| `documents/ANIMATED_GRADIENT_ORBS_BACKGROUND.md` | Orb CSS architecture |

---

Site made and managed by BBK Productions.
