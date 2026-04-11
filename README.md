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
├── index.html                  # Home page (hero video, 7-card series carousel, clash tiles, academy, coaching, artist, vibes, connect)
├── series.html                 # Chuby Dice Series — swipe carousel (current + past) + collection pricing
├── praise-flow.html            # Praise Flow series (April 2026) — per-tier Stripe checkout
├── motherland.html             # Motherland series (May 2026) — per-tier Stripe checkout
├── dancehall-royalty.html       # Dancehall Royalty series (June 2026) — per-tier Stripe checkout
├── street-vybz.html            # Street Vybz series (July 2026) — full write-up content
├── survival-story.html         # Survival Story series (August 2026) — full write-up content
├── hot-steppaz.html            # Hot Steppaz series (September 2026) — full write-up content
├── born-agen.html              # Born Agen series (October 2026) — full write-up content
├── march-back-in-time.html     # March Back in Time series (March 2026, past)
├── lovers-rock.html            # Lovers' Rock series (past, Stripe disabled)
├── full-series.html            # Full series collection page (past, Stripe disabled)
├── past-series.html            # Past Events archive
├── clash.html                  # Clash Inna Dancehall (overarching + 2 event cards)
├── litefeet-v-dancehall.html   # Clash #1: Litefeet v Dancehall — Sat 23 May 2026, Phil Eazy & Chuby Dice
├── krump-v-dancehall.html      # Clash #2: Krump v Dancehall — Sat 1 Aug 2026, Antagonize & Chuby Dice
├── coaching.html               # Professional 1:1 Coaching & Programs (pink #E040FB theme)
├── academy.html                # Dancehall Academy (4 shell cards: Auditions, Scholarships, Curriculum, Vision 2030)
├── about.html                  # About Chuby Dice (biography accordion, 6 sections)
├── contact.html                # Contact / Instagram / Brand Ambassadorship
├── in-ya-city.html             # Chuby Dice in Ya City (Adelaide card with image)
├── in-ya-city-adelaide.html    # In Ya City — Adelaide (event flyer hero)
├── chatbot.js                  # AI chatbot widget (Anthropic API via Netlify function)
├── netlify/functions/chat.js   # Serverless chat function (Anthropic Claude API)
├── images/                     # All site images and flyers (optimized JPEGs)
├── videos/                     # Hero background videos (1-5.mp4)
├── screenshots/                # Client screenshots and IA documents (not deployed)
├── documents/                  # Session recovery, resume instructions, reference guides
└── .gitignore
```

## Tech Stack

- **Static HTML** — No build tools, no framework. Inline `<style>` and `<script>` per page.
- **Font** — Bebas Neue (unified across all 22 pages).
- **Design Tokens** — `--yellow (#F5C518)`, `--black (#0A0A0A)`, `--dark (#111111)`, `--pink (#E040FB)`, `--border (#242424)`.
- **Netlify Functions** — Serverless chat at `/.netlify/functions/chat` (Anthropic Claude API).
- **Stripe** — Live payment links for 5 class pass tiers + coaching + CLash 3-tiered passes + Dancehall Academy registration (free).

## Key Features

### Home Page (`index.html`)
- Full-screen hero video with `object-position: center 20%` sweet spot
- **7-card horizontal swipe carousel** (Praise Flow → Born Agen) with dark gradient overlay, V2-style hover highlight
- **Clash Inna Dancehall** section (no "Clash Events" label) with 2 event tiles using NO PASSION flyer images
- **Dancehall Academy** tile with golden glow border, "Launching 2026" pulsing label
- **Professional 1:1 Coaching** tile with pink (#E040FB) theme, enlarged title (`clamp(2.4rem,6vw,5rem)`)
- **Animated glow-line separators** between all sections
- Floating social sidebar, animated gradient orbs background

### Clash Pages
- `clash.html` — Hero: "CLASH INNA" (white) + "DANCEHALL" (blue #00CFFF), no "WITH PASSION STUDIO", no May 2026 pill. About Clash text from IA. NO PASSION images.
- `litefeet-v-dancehall.html` — Full write-up + Phil Eazy bio with Recent Achievements (5 items). Booking cards deferred ("Bookings open 11 April 2026").
- `krump-v-dancehall.html` — Full write-up + Antagonize bio. Booking cards now implemented.

### Series Pages
- All write-ups word-for-word from client's IA document
- Survival Story (August): Corrected text — Black Blingaz, Black Dice, Black Eagles, Overload Skankaz
- Street Vybz, Hot Steppaz, Born Agen: Client-cleared write-ups

### Academy Page (`academy.html`)
- Auditions Now Open card is active for registration via Stripe (13 June 2026).
- 3 remaining shell cards have been consolidated into one shell.
- Hero image is removed to improve UX
- Chuby Dice V_3 had 4 shell cards in 2x2 grid: Auditions (13 Jun 2026), Scholarships, Curriculum, Vision 2030
- Chuby Dice V_3 had no "Shell — Content TBC" or "coming soon" text — production-ready labels

## Stripe Pricing (Live)

| Package | Price | Per Class |
|---------|-------|-----------|
| Single Class | $30 | $30 |
| 4 Classes | $100 | $25 |
| 5 Classes | $125 | $25 |
| 10 Classes | $230 | $23 |
| 20 Classes | $450 | $22.50 |
| 1:1 Coaching | $120 | — |
|Full Pass | $45 | $45 |
| Workshop Only | $35 | $35 |
|Clash Only | $20 | $20 |
| Dancehall Academy Registration | $0 | — |


**Clash Stripe links:** Now included (bookings opened 11 April 2026).

## UI/UX Design System

### Animated Glow-Line Separator (`.section-sep`)
Golden gradient line with sweeping white/gold highlight animation (4s infinite loop). Replaces all plain `border-top` across all 22 pages.

### Card Hover Effects
Image brightens (`filter: brightness(1.15)`), scales (`1.04`), golden glow box-shadow, spring `cubic-bezier(0.34,1.56,0.64,1)`.

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

## Release History

- **Release 2B** (08-09 Apr 2026): Images, write-ups, clash deployment, UI/UX refactors, critical corrections
- **Release 3** (10 Apr 2026): Clash Stripe payment links, Academy details, Acknowledgment update
- **Release 3A** (11-12 Apr 2026): Clash Stripe payment links + image updates, Academy Audition details + redesign, Chuby Dice Series clean-up

## Release Planning

- **Release 3B** (24 Apr 2026): Dancehall Academy Drop 2 (Auditions Details for DJs & Dancers) + Terms & Conditions + Dancehall Fitness
- **Release 3C** (8 May 2026): Dancehall Academy Drop 3 (video + scholarships info)
- **Release 3D** (22 May 2026): Dancehall Academy Drop 4
- **Release 3E** (5 Jun 2026): Dancehall Academy Drop 5
- **Future Releases**: Chuby Dice Interviews + Performances + Video Projects + Funding + Consulting + Sponsorships  

---

Site made and managed by BBK Productions.
