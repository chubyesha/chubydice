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
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers
├── videos/                     # Hero background videos (1-5.mp4)
├── documents/                  # Session recovery and resume instructions
└── .gitignore                  # IDE, node_modules, .env, screenshots, .claude, etc.
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Each page is self-contained with inline `<style>` and `<script>`.
- **Fonts** — Bebas Neue (headings), Barlow / Barlow Condensed (body/UI).
- **Design Tokens** — CSS custom properties: `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--dark (#111111)`, `--pink (#E040FB)`.
- **Netlify Functions** — Serverless chat endpoint at `/.netlify/functions/chat` using Anthropic Claude API.
- **Stripe** — Payment links (`buy.stripe.com`) embedded in series sub-pages. Collection pricing on `series.html` has placeholder buttons pending Stripe setup.

## Pages Overview

### Home (`index.html`)
- Hero video (5 rotating videos with crossfade) with poster fallback
- Series tiles grid (March Back in Time, Praise Flow, Motherland, Dancehall Royalty)
- Mobile: flyer carousel with dots
- Clash Inna Dancehall tile, Academy section, 1:1 Coaching tile
- Artist bio, Dancehall Vibes playlist, Social connect (Instagram)

### Series (`series.html`)
- Individual series cards with images and booking buttons
- **Collection Pricing** section: 5 tiers ($30 single, $100/4, $125/5, $230/10, $450/20) — Stripe buttons pending
- Mobile: swipeable card stack

### Coaching (`coaching.html`)
- Hero with watermark background
- Expandable accordion with 5 coaching focus areas
- Booking card with Stripe link

### About (`about.html`)
- Photo mosaic hero (6 cells placeholder)
- Biography in 6 collapsible accordion sections (first open by default)

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
npx serve .
# Or
python3 -m http.server 8000
```

For Netlify Functions (chatbot): `npx netlify dev`

## Git Workflow

- **main** / **master** — Production branch. Do not checkout or merge directly.
- Feature branches: `feat/<description>`
- Docs branches: `docs/<description>`
- Chore branches: `chore/<description>`

---

Site made and managed by BBK Productions.
