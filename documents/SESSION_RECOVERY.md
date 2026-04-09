# Session Recovery: Release 2B Deployment + Critical Corrections

**Session Dates:** 2026-04-08 to 2026-04-09
**Project:** Chuby Dice Website V1
**Working Directory:** `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1`

---

## Session 1 (2026-04-08): Release 2B Images, Write-ups, UI/UX Refactors

### Images & Content Deployment
| Branch | Commit | Description |
|--------|--------|-------------|
| `feat/release-2b-images-content` | `71197f5` | 8 PNG→JPEG optimized, August renamed to Survival Story, clash images deployed |
| `feat/series-writeups-content` | `0b7292e` | Series write-ups from IA document added to 4 shell pages |

### Homepage UI/UX
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/series-card-text-readability` | `dd948c1` | Dark 4-stop gradient overlay on series cards |
| `feat/series-card-hover-highlight` | `22e1c7f` | V2-style hover (image brighten, golden glow, spring animation) |
| `fix/homepage-missing-series-cards` | `a81b91d` | Added Praise Flow, Motherland, Dancehall Royalty to carousel (7 total) |

### Academy & Coaching
| Branch | Commit | Description |
|--------|--------|-------------|
| `feat/academy-tile-glow-highlight` | `f7769a0` | Golden glow border, "Launching 2026" pulsing label |
| `fix/academy-tile-width` | `63fa8f3` | max-width: 960px |
| `feat/academy-shell-cards-horizontal` | `9032945` | 4 shell cards added |
| `fix/academy-cards-2x2-grid` | `264e114` | Changed from 4-col to 2x2 grid |

### Global Separators
| Branch | Commit | Description |
|--------|--------|-------------|
| `feat/section-separator-glow` | `557d757` | Glow-line between Academy and Coaching |
| `feat/global-glow-line-separators` | `e8b192d` | Replaced ALL plain borders across 22 pages |

### Clash & Coaching Fixes
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/coaching-title-theme-color` | `89d25ce` | Pink #E040FB on "1:1 COACHING" |
| `fix/clash-hero-title-layout` | `4336b61` | Title split: gold "CLASH INNA DANCEHALL" above, white "WITH PASSION STUDIO" below |
| `fix/clash-hero-nav-layout` | `f000365` | Back to Home (left) / May 2026 (right) flex row |

### Documentation
| Branch | Commit | Description |
|--------|--------|-------------|
| `docs/session-recovery-update` | `6b0d650` | README, SESSION_RECOVERY, RESUME_INSTRUCTIONS updated |

---

## Session 2 (2026-04-09): Critical Corrections for Live Deployment

Source: `screenshots/Info Architecture - RELEASE 2B CRITICAL CHANGES CORRECTIONS.docx`

### Item 1: Coaching Tile Bigger
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/homepage-clash-label-coaching` | `122b4d5` | Title font-size bumped to clamp(2.4rem,6vw,5rem). By-line already removed. "Clash Events" label already absent. |

### Item 2: Survival Story Text Corrected
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/survival-story-correct-text` | `a7c7715` | Complete rewrite: correct crews (Black Blingaz, Black Dice, Black Eagles, Overload Skankaz), corrected by-line, "Dancehall as witness & persona" sub-heading. Updated card descriptions on index.html + series.html. |

### Item 3: Clash Images — NO PASSION Versions
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/clash-images-no-passion` | `1f0b394` | 5 images replaced: clash-may-photo.jpg (261KB), clash-august-photo.jpg (238KB), clash-overarching-photo.jpg (207KB), clash-overarching.jpg (189KB), clash-may-runsheet.jpg (204KB). Passion Studio branding removed per sponsorship change. |

### Item 4: Clash Hero Corrections
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/clash-hero-corrections` | `3d9b73f` | Title colors: "CLASH INNA" white + "DANCEHALL" blue #00CFFF. Hero desc updated. "WITH PASSION STUDIO" and "May 2026" pill already removed in prior commits. |

### Item 5: Clash Event Bookings Deferred
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/clash-event-bookings-deferred` | `410203c` | Removed 5-tier pricing cards from litefeet-v-dancehall.html and krump-v-dancehall.html. Replaced with "Bookings open 11 April 2026" message. |

### Item 6: Clash Correct Text + Artist Bios
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/clash-correct-text-writeups` | `ac84fa3` | clash.html: "ABOUT CLASH" (white/blue) with correct IA text. litefeet: Phil Eazy write-up + bio. krump: Antagonize write-up + bio. All "Passion Studio" and "@Passion Studio" references removed from meta, titles, alt text, tile descriptions. |

### Item 7: Remove Under-Construction Text
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/remove-esha-refs-acknowledgment` | `59ff4b0` | Academy cards: "Shell" badges → "Launching 2026"/"2026-2027"/"Long-term Vision". Image placeholders removed. "coming soon" text replaced. Clash meta updated. |

### Item 8: Phil Eazy Bio — Missing Content
| Branch | Commit | Description |
|--------|--------|-------------|
| `fix/clash-writeups-complete-word-for-word` | `146aa9c` | Added truncated text: "organising Melbourne's first Litefeet battle, Rhythm of the Lite in 2023..." + full Recent Achievements list (5 items). All other write-ups verified word-for-word — no other omissions. |

---

## Current State

### Pages Live-Ready (no placeholder/construction text)
All 22 HTML pages verified clean — no "Esha", "Passion Studio", "Shell — Content TBC", "coming soon", or "to be provided" user-facing text.

### Pending for Release 3 (10 April 2026)
| Item | Status | Notes |
|------|--------|-------|
| Clash Stripe payment links | Awaiting Stripe items | "Bookings open 11 April" displayed on event pages |
| Academy details (Auditions, Scholarships, etc.) | Awaiting client content | Shell cards present with clean labels |
| Updated Acknowledgment of Country text | May be updated | Current text: "We acknowledge the Traditional Custodians..." |
| Colourful orbs from V2 to V1 | Per discussion 07/04 | Orbs already exist on index.html, may need expansion |

### Files Modified This Session (09 Apr)
- `index.html` — coaching title size, Passion Studio removed from clash tiles, Survival Story card text
- `survival-story.html` — complete body rewrite, hero desc, meta
- `series.html` — Survival Story card text
- `clash.html` — hero colors, About Clash text, meta descriptions, Passion Studio removed
- `litefeet-v-dancehall.html` — full write-up + Phil Eazy bio with achievements, booking card deferred
- `krump-v-dancehall.html` — full write-up + Antagonize bio, booking card deferred
- `academy.html` — shell card labels cleaned for production
- 5 clash images replaced (NO PASSION versions)
