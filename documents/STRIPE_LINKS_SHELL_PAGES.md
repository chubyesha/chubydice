# Stripe Payment Links — Series Pages

## Overview

All Chuby Dice Series pages use the same 5 Stripe Payment Links for class booking. These links are shared across all series — the client confirmed that April, May, June and all future series use identical payment tiers.

## Stripe Payment Links

| Tier | Price | Full Link |
|------|-------|-----------|
| Single Class | $30 | https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b |
| 4 Classes | $100 | https://buy.stripe.com/6oUbJ16033xgeRYfRB4F20c |
| 5 Classes | $125 | https://buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d |
| 10 Classes | $230 | https://buy.stripe.com/eVqdR97473xg25ccFp4F20e |
| 20 Classes | $450 | https://buy.stripe.com/9B6fZhagj0l4fW28p94F20f |

### Coaching (Separate Link)

| Tier | Price | Full Link |
|------|-------|-----------|
| 1:1 Coaching | $120 | https://buy.stripe.com/3cIbJ17470l4cJQ34P4F209 |

## Pages Using These Links

### Series Pages (5-tier pricing selector)

| Page | File | Status |
|------|------|--------|
| Praise Flow | praise-flow.html | Active |
| Motherland | motherland.html | Active |
| Dancehall Royalty | dancehall-royalty.html | Active |
| Street Vybz | street-vybz.html | Shell (Jul 2026) |
| Spain Town Badness | spain-town-badness.html | Shell (Aug 2026) |
| Hot Steppaz | hot-steppaz.html | Shell (Sep 2026) |
| Born Agen | born-agen.html | Shell (Oct 2026) |

### Coaching Page (Single button)

| Page | File | Status |
|------|------|--------|
| Coaching | coaching.html | Active |

### Clash Pages (No Stripe links yet)

| Page | File | Status |
|------|------|--------|
| Litefeet v Dancehall | litefeet-v-dancehall.html | Shell — "Stripe Links Coming Soon" |
| Krump v Dancehall | krump-v-dancehall.html | Shell — "Stripe Links Coming Soon" |

## How the Booking Card Works

### HTML Structure

Each series page has a `.booking-card` with 5 `.price-option` elements:

```html
<div class="price-option selected" data-price="30" data-link="https://buy.stripe.com/..." onclick="selectPrice(this)">
  <div class="price-option-left">
    <div class="price-radio"><div class="price-radio-dot"></div></div>
    <span class="price-option-label">Single Class</span>
  </div>
  <span class="price-option-amount">$30</span>
</div>
```

### JavaScript (Hardened)

Payment links are stored in an immutable whitelist object — NOT read from DOM attributes:

```javascript
var STRIPE_LINKS = {
  '30': 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b',
  '100': 'https://buy.stripe.com/6oUbJ16033xgeRYfRB4F20c',
  '125': 'https://buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d',
  '230': 'https://buy.stripe.com/eVqdR97473xg25ccFp4F20e',
  '450': 'https://buy.stripe.com/9B6fZhagj0l4fW28p94F20f'
};
var selectedPrice = '30';

function selectPrice(el) {
  // Highlights selected tier and updates button text
  if (STRIPE_LINKS[price]) selectedPrice = price;
  btn.textContent = 'Book Now — $' + price;
}

function bookNow() {
  // Validates URL hostname before opening
  var url = new URL(link);
  if (url.hostname !== 'buy.stripe.com') return;
  window.open(link, '_blank', 'noopener,noreferrer');
}
```

### Security Measures

- **Immutable whitelist**: Stripe URLs stored in JS object, not read from DOM `data-link` attributes (prevents DOM manipulation attacks)
- **URL hostname validation**: `new URL()` parsing with `buy.stripe.com` hostname check (prevents subdomain spoofing)
- **noopener,noreferrer**: `window.open` flags prevent reverse tabnapping
- **Protocol check**: Only `https:` protocol accepted

## How to Update Stripe Links

If the client provides new Stripe links:

1. Open each of the 7 series page HTML files
2. Find the `<script>` block containing `var STRIPE_LINKS = {`
3. Update the URLs in the `STRIPE_LINKS` object
4. Also update the `data-link` attributes on each `.price-option` element (for consistency, though the JS whitelist is authoritative)
5. Test by clicking each price tier and verifying "Book Now" opens the correct Stripe page

## How to Add Stripe Links to Clash Pages

When the client provides Stripe links for clash events:

1. Open `litefeet-v-dancehall.html` or `krump-v-dancehall.html`
2. Add `data-link="https://buy.stripe.com/..."` to each `.price-option`
3. Replace `<button class="btn-coming-soon">Stripe Links Coming Soon</button>` with `<button class="btn-book-now" id="bookBtn" onclick="bookNow()">Book Now — $30</button>`
4. Replace the minimal `selectPrice` function with the full hardened JS block (copy from any series page)
