# Resume Instructions — Chuby Dice Website

**For the next Claude Code session to continue where this one left off.**

---

## Quick Start

1. **Read this file first**, then `documents/SESSION_RECOVERY.md` for full context.
2. **Check current branch:** `git branch --show-current`
3. **Check for uncommitted work:** `git status`
4. **Read the PRD:** `screenshots/Info Architecture - RELEASE 2 08022026.docx` (use python-docx to parse)

---

## Project Context

- **Project:** Chuby Dice — static HTML website for a Dancehall artist/educator
- **Live URL:** https://www.chubydice.com
- **Hosting:** Netlify (auto-deploys from GitHub)
- **Repo:** `git@github.com:chubyesha/chubydice.git`
- **Tech:** Static HTML (no build tools), inline CSS/JS per page, `shared-theme.css` for design system, Netlify Functions for chatbot
- **Design:** Purple/dark theme with Outfit + DM Sans fonts, CSS custom properties for tokens

## What Was Completed (Release 2A)

All 7 product requirements from the PRD have been implemented on branch `feat/release-2a-requirements`:

1. Stripe collection pricing section on `series.html` (5 tiers, placeholder buttons)
2. Nav menus standardized across all 16 HTML pages (added Clash, Brand Ambassadorship, 2026 Events)
3. Hero images updated for Motherland (`motherland-2026.jpeg`) and Dancehall Royalty (`dancehall-royalty-2026.jpeg`)
4. Coaching hero image verified correct (`5015f87ce59f.png`)
5. Hero video already updated to `hero-bg.mp4` by remote
6. Coaching accordion made functional (5 expandable items with content)
7. About page biography converted to 6 collapsible accordion sections

## What Still Needs To Be Done

### Immediate (Client-Dependent)
- **Stripe payment links:** Client needs to create Stripe items for the 5 class packages ($30/$100/$125/$230/$450). Once provided, replace `data-stripe` placeholder buttons in `series.html` with `onclick="window.open('https://buy.stripe.com/...','_blank')"` and change button text from "Coming Soon" to "Buy Now". Remove the `.pending` class.
- **Hero images confirmation:** Client should verify `motherland-2026.jpeg` and `dancehall-royalty-2026.jpeg` are the intended flyers
- **New hero video:** PRD mentioned "potential change" — if client provides a new video file, replace `videos/hero-bg.mp4`

### Pre-existing Issues to Fix (Not Release 2A Scope)
- **Broken OG image:** All 16 pages reference `chuby-profile-CkJq2sVN.jpg` which doesn't exist. Fix by updating all `og:image` and `twitter:image` meta tags to point to an existing image file.
- **CORS wildcard:** `netlify.toml` and `netlify/functions/chat.js` use `Access-Control-Allow-Origin: *`. Restrict to actual domain to prevent API abuse.
- **Chat function input validation:** Add message length/count limits and role validation to `netlify/functions/chat.js`.
- **CSS !important conflicts:** `shared-theme.css` uses `!important` on body font-family, overriding per-page fonts. Resolve by removing `!important` or aligning all pages.
- **`--border` CSS variable:** Conflict between `shared-theme.css` (`rgba(255,255,255,0.08)`) and page-local definitions (`#242424`).
- **Security headers:** Add `X-Frame-Options`, `Content-Security-Policy`, `Referrer-Policy` to `netlify.toml`.

### Release 2B (Purple in PRD — Develop Later)
- **Clash Inna Dancehall pricing:** Workshop and clash pass pricing (not for this release)
- **Terms & Conditions page**
- **Brand Ambassadorship dedicated page** (currently links to contact.html)

## Key Patterns to Follow

### Nav Menu Updates
All 16 HTML files have independent nav menus. Use a Python batch script (see SESSION_RECOVERY.md) to update them consistently. The pattern:
- Find `<div class="menu-overlay" id="menuOverlay">` to `</div>` (before `menu-divider`)
- Replace inner links
- Set `class="active"` per page

### Accordion Pattern
Used in `coaching.html` and `about.html`:
- CSS: `.acc-item.open .acc-body { max-height: Xpx; }` with `overflow: hidden; transition: max-height 0.35s ease;`
- HTML: `<div class="acc-header"><span>Title</span><svg class="acc-arrow">...</svg></div><div class="acc-body"><p>Content</p></div>`
- JS: Click handler toggles `.open` class, single-open behavior (closes others)

### Stripe Link Pattern
Existing pattern on sub-pages: `onclick="window.open('https://buy.stripe.com/...','_blank')"`
New pricing cards use `data-stripe` attributes for future JS wiring.

## Critical Warnings

- **NEVER checkout main/master** — work only on feature branches
- **NEVER git stash** — it erases current changes
- **NEVER force push** to any shared branch
- **Nav menus are duplicated** across 16 files — any change must be applied to ALL pages
- **No build tools** — changes to HTML/CSS/JS take effect immediately, no compilation needed
- **`shared-theme.css` overrides** — It uses `!important` extensively. Be aware when adding new styles.
- **Test on mobile** — The site has specific mobile breakpoints at 900px and 640px

## File Quick Reference

| Need to... | File(s) |
|------------|---------|
| Update nav menu | All 16 `.html` files |
| Add/modify series | `series.html`, `index.html`, create new sub-page |
| Update coaching content | `coaching.html` |
| Update biography | `about.html` |
| Change design tokens | `shared-theme.css` |
| Modify chatbot | `chatbot.js`, `netlify/functions/chat.js` |
| Update Netlify config | `netlify.toml` |
| Add Stripe links | Series sub-pages + `series.html` pricing section |
