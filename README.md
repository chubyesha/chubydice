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
├── index.html                  # Home page (hero video, series carousel, coaching, academy, artist, vibes, connect)
├── series.html                 # Chuby Dice Series — swipe carousel (current + past) + collection pricing
├── praise-flow.html            # Praise Flow series (April 2026) — per-tier Stripe checkout
├── motherland.html             # Motherland series (May 2026) — per-tier Stripe checkout
├── dancehall-royalty.html       # Dancehall Royalty series (June 2026) — per-tier Stripe checkout
├── march-back-in-time.html     # March Back in Time series (March 2026, past)
├── lovers-rock.html            # Lovers' Rock series (past, Stripe disabled)
├── full-series.html            # Full series collection page (past, Stripe disabled)
├── past-series.html            # Past Events archive
├── clash.html                  # Clash Inna Dancehall with Passion Studio
├── coaching.html               # Professional 1:1 Coaching & Programs (60vh hero, accordion)
├── academy.html                # Dancehall Academy (flames hero, one-line title)
├── about.html                  # About Chuby Dice (biography accordion, 6 sections)
├── contact.html                # Contact / Instagram / Brand Ambassadorship
├── in-ya-city.html             # Chuby Dice in Ya City (Adelaide card with image)
├── in-ya-city-adelaide.html    # In Ya City — Adelaide (event flyer hero)
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers
├── videos/                     # Hero background videos (1-5.mp4)
├── documents/                  # Session recovery and resume instructions
└── .gitignore
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Inline `<style>` and `<script>` per page.
- **Fonts** — Bebas Neue (headings), Barlow / Barlow Condensed (body/UI). Unified Google Fonts URL across all 16 pages.
- **Design Tokens** — `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--dark (#111111)`, `--pink (#E040FB)`.
- **Netlify Functions** — Serverless chat at `/.netlify/functions/chat` (Anthropic Claude API).
- **Stripe** — Live payment links for 5 class pass tiers + coaching. Archived pages disabled.

## Key Features

### Home Page (`index.html`)
- Hero video (5 rotating videos with crossfade)
- **Horizontal swipe carousel** with full-image background cards (current + past series with "Past Session" watermark)
- **Countdown badges** — "Starts in X days" on each current series
- **Series Collection Pack** button linking to pricing section
- Clash Inna Dancehall tile, Dancehall Academy section ("Out of many, one" byline)
- 1:1 Coaching tile, "Meet Chuby Dice" (one line), CDDA Playlist, Social connect

### Series Page (`series.html`)
- **Horizontal swipe carousel** with All/Current/Past tab filter
- Drag-to-scroll on desktop, touch swipe on mobile
- **Collection Pricing** section (5 live Stripe links): $30/$100/$125/$230/$450

### Sub-Pages
- **Coaching** — 60vh hero, expandable 5-item accordion, Stripe booking
- **Academy** — Flames-in-frame hero (`object-position: center 60%`), one-line title
- **About** — Photo mosaic hero, 6 collapsible biography accordion sections
- **Adelaide** — Event flyer hero image (client-provided)

## Navigation (Dis an Dat)

All 16 pages share a standardized dropdown with collapsible "Dis an Dat" submenu:

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

## Development

```bash
npx serve .              # Static server
npx netlify dev          # With Netlify Functions (chatbot)
python3 -m http.server   # Alternative
```

## Git Workflow

- **main** — Production. Never checkout or merge directly.
- `feat/<desc>`, `fix/<desc>`, `docs/<desc>`, `chore/<desc>` — Feature branches.

---

Site made and managed by BBK Productions.
