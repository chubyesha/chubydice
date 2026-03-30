# Chuby Dice Website

Official website for **Chuby Dice** — Dancehall artist, educator, and cultural practitioner based in Naarm (Melbourne), Australia.

**Live site:** [chubydice.com](https://www.chubydice.com)
**Hosting:** Netlify
**Repo:** [github.com/chubyesha/chubydice](https://github.com/chubyesha/chubydice)

---

## Project Structure

```
chubydice/
├── index.html                  # Home page (hero video, series tiles, coaching, academy, artist, vibes, connect)
├── series.html                 # Chuby Dice Series — all current series + collection pricing
├── praise-flow.html            # Praise Flow series (April 2026)
├── motherland.html             # Motherland series (May 2026)
├── dancehall-royalty.html       # Dancehall Royalty series (June 2026)
├── march-back-in-time.html     # March Back in Time series (March 2026)
├── lovers-rock.html            # Lovers' Rock series (past)
├── full-series.html            # Full series collection page
├── past-series.html            # 2026 Events archive / past sessions
├── clash.html                  # Clash Inna Dancehall with Passion Studio
├── coaching.html               # Professional 1:1 Coaching & Programs
├── academy.html                # Dancehall Academy — Launching 2026
├── about.html                  # About Chuby Dice (biography with accordion sections)
├── contact.html                # Contact / Instagram
├── in-ya-city.html             # Chuby Dice in Ya City
├── in-ya-city-adelaide.html    # In Ya City — Adelaide
├── shared-theme.css            # Shared design system (purple/dark theme, typography, nav overrides)
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify.toml                # Netlify config (redirects, headers, cache rules)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers
├── videos/                     # Hero background videos
├── documents/                  # Session recovery and resume instructions
└── .gitignore                  # IDE, node_modules, .env, screenshots, .claude, etc.
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Each page is self-contained with inline `<style>` and `<script>`.
- **Shared Theme** — `shared-theme.css` provides site-wide design tokens, typography (Outfit + DM Sans), nav styling, and overrides via CSS custom properties.
- **Fonts** — Outfit (headings), DM Sans (body), Bebas Neue (legacy/fallback), Barlow (legacy/fallback).
- **Design Tokens** — Purple-dominant palette (`--void`, `--deep`, `--surface`, `--purple-600`, `--gold`, `--pink`, `--cyan`).
- **Netlify Functions** — Serverless chat endpoint at `/.netlify/functions/chat` using Anthropic Claude API.
- **Stripe** — Payment links (`buy.stripe.com`) embedded in series sub-pages. Collection pricing on `series.html` has placeholder buttons pending Stripe setup.

## Pages Overview

### Home (`index.html`)
- Hero video (`videos/hero-bg.mp4`) with poster fallback
- Series tiles grid (March Back in Time, Praise Flow, Motherland, Dancehall Royalty)
- 1:1 Coaching tile, Academy section, Artist bio, Dancehall Vibes playlist, Social connect
- Mobile: horizontal scroll with swipe dots

### Series (`series.html`)
- Individual series cards with images and booking buttons
- **Collection Pricing** section: 5 tiers ($30 single, $100/4, $125/5, $230/10, $450/20) — Stripe buttons pending

### Coaching (`coaching.html`)
- Hero with watermark background
- Expandable accordion with 5 coaching focus areas (foundations, sub-genres, clash vs party, choreography, history)
- Booking card with Stripe link

### About (`about.html`)
- Photo mosaic hero (auto-scrolling lanes of about photos)
- Biography in 6 collapsible accordion sections (first open by default)
- Sections: Spanish Town origins, Black Dice crew, Global performance, Australia, Cultural transmission, Empowerment philosophy

## Navigation

All 16 pages share a standardized dropdown menu:

1. Home
2. Chuby Dice Series
3. Clash Inna Dancehall
4. Professional 1:1 Coaching & Programs
5. Dancehall Academy — Launching 2026
6. About Chuby Dice
7. Brand Ambassadorship
8. Chuby Dice in Ya City
9. 2026 Events (Archive)
10. Contact / Instagram

## Series Images

| Series | Image File |
|--------|-----------|
| March Back in Time | `images/a84b4d3eec82.png` |
| Praise Flow (April) | `images/praise-flow-2026.png` |
| Motherland (May) | `images/motherland-2026.jpeg` |
| Dancehall Royalty (June) | `images/dancehall-royalty-2026.jpeg` |
| Clash Inna Dancehall | `images/clash-inna-dancehall.png` |
| Coaching hero | `images/5015f87ce59f.png` |

## Stripe Pricing (Series Collection)

| Package | Price | Per Class | Stripe Status |
|---------|-------|-----------|--------------|
| Single Class | $30 | $30 | Pending setup |
| 4 Classes | $100 | $25 | Pending setup |
| 5 Classes | $125 | $25 | Pending setup |
| 10 Classes | $230 | $23 | Pending setup |
| 20 Classes | $450 | $22.50 | Pending setup |

## Development

No build step required. Open any `.html` file directly or serve with any static server.

```bash
# Simple local server
npx serve .

# Or Python
python3 -m http.server 8000
```

For Netlify Functions (chatbot), use:
```bash
npx netlify dev
```

## Git Workflow

- **main** / **master** — Production branch. Do not checkout or merge directly.
- Feature branches: `feat/<description>`
- Docs branches: `docs/<description>`
- Chore branches: `chore/<description>`

## Known Pre-existing Issues

1. **OG image broken** — All pages reference `chuby-profile-CkJq2sVN.jpg` which doesn't exist. Should be updated.
2. **CORS wildcard** — `netlify.toml` and chat function use `Access-Control-Allow-Origin: *`. Should restrict to actual domain.
3. **Chat function** — No input validation or rate limiting on the Netlify chat function.
4. **`shared-theme.css` !important** — Forces `body` font-family with `!important`, overriding page-specific fonts.

---

Site made and managed by BBK Productions.
