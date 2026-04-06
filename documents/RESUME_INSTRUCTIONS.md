# Resume Instructions: Stripe Payment Security Fixes

**Previous Session:** 2026-04-06 (Security Review)
**Current Task:** Implement security fixes for Stripe payment links
**Files to Modify:** 6 shell pages (street-vybz.html, born-agen.html, dancehall-royalty.html, hot-steppaz.html, motherland.html, praise-flow.html)

## Quick Context

A security review was completed on the Stripe Payment Link implementation. Five critical and medium security issues were identified that must be fixed before processing real money.

**DO NOT skip reading:** `documents/SECURITY_REVIEW_STRIPE_PAYMENT.md` for full vulnerability details.

## TL;DR - What Needs Fixing

### 1. HIGH Priority - Replace indexOf() with URL API (ALL 6 files)

**Current (WEAK):**
```javascript
function bookNow() {
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) return;
  window.open(selectedStripeLink, '_blank');
}
```

**Replace with (SECURE):**
```javascript
function bookNow() {
  if (!selectedStripeLink) return;
  
  try {
    const url = new URL(selectedStripeLink);
    
    // Verify protocol is HTTPS
    if (url.protocol !== 'https:') return;
    
    // Verify hostname is exactly buy.stripe.com
    if (url.hostname !== 'buy.stripe.com') return;
    
    // Verify path starts with / (Stripe format)
    if (!url.pathname.startsWith('/')) return;
    
    window.open(selectedStripeLink, '_blank', 'noopener,noreferrer');
  } catch (error) {
    console.error('Invalid payment link');
    return;
  }
}
```

### 2. HIGH Priority - Use Immutable Whitelist (ALL 6 files)

**Current (VULNERABLE - DOM can be modified):**
```javascript
var selectedStripeLink = 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b';

function selectPrice(el) {
  var link = el.getAttribute('data-link');
  if (link) selectedStripeLink = link;  // Any script can change this
}
```

**Replace with (SECURE):**
```javascript
// Immutable whitelist - cannot be modified
const STRIPE_PAYMENT_LINKS = Object.freeze({
  '30': 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b',
  '100': 'https://buy.stripe.com/6oUbJ16033xgeRYfRB4F20c',
  '125': 'https://buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d',
  '230': 'https://buy.stripe.com/eVqdR97473xg25ccFp4F20e',
  '450': 'https://buy.stripe.com/9B6fZhagj0l4fW28p94F20f'
});

let selectedPrice = '30';

function selectPrice(el) {
  const price = el.getAttribute('data-price');
  if (STRIPE_PAYMENT_LINKS[price]) {
    selectedPrice = price;
  }
}

function bookNow() {
  const link = STRIPE_PAYMENT_LINKS[selectedPrice];
  if (link) {
    try {
      const url = new URL(link);
      if (url.protocol !== 'https:' || url.hostname !== 'buy.stripe.com') return;
      window.open(link, '_blank', 'noopener,noreferrer');
    } catch (error) {
      console.error('Invalid payment link');
    }
  }
}
```

### 3. MEDIUM Priority - Add Rate Limiting (ALL 6 files)

**Add before bookNow() function:**
```javascript
let lastPaymentTime = 0;
const PAYMENT_COOLDOWN = 2000; // 2 seconds

function bookNow() {
  const now = Date.now();
  
  // Prevent rapid-fire clicks
  if (now - lastPaymentTime < PAYMENT_COOLDOWN) {
    console.warn('Please wait before trying again');
    return;
  }
  
  const link = STRIPE_PAYMENT_LINKS[selectedPrice];
  if (!link) return;
  
  try {
    const url = new URL(link);
    if (url.protocol !== 'https:' || url.hostname !== 'buy.stripe.com') return;
    
    lastPaymentTime = now;
    window.open(link, '_blank', 'noopener,noreferrer');
  } catch (error) {
    console.error('Invalid payment link');
  }
}
```

### 4. MEDIUM Priority - Add User Confirmation (ALL 6 files)

**Update button HTML:**
```html
<button class="btn-book-now" id="bookBtn" onclick="bookNow()">Book Now — $30</button>
```

**Update bookNow() to include confirmation:**
```javascript
function bookNow() {
  const now = Date.now();
  if (now - lastPaymentTime < PAYMENT_COOLDOWN) return;
  
  const price = selectedPrice || '30';
  const confirmed = confirm(`Confirm payment of $${price} for Chuby Dice?`);
  if (!confirmed) return;
  
  const link = STRIPE_PAYMENT_LINKS[selectedPrice];
  if (!link) return;
  
  try {
    const url = new URL(link);
    if (url.protocol !== 'https:' || url.hostname !== 'buy.stripe.com') return;
    
    lastPaymentTime = now;
    window.open(link, '_blank', 'noopener,noreferrer');
  } catch (error) {
    console.error('Invalid payment link');
  }
}
```

## Implementation Plan

### Step 1: Create Feature Branch
```bash
git checkout -b fix/stripe-payment-security
```

### Step 2: Fix Each File in Sequence

For each of the 6 shell pages (in this order):
1. street-vybz.html
2. born-agen.html
3. dancehall-royalty.html
4. hot-steppaz.html
5. motherland.html
6. praise-flow.html

**For each file:**
1. Locate the script block with `var selectedStripeLink = ...`
2. Replace entire script block with secure version (see above)
3. Test in browser that price selection works
4. Test that clicking "Book Now" opens Stripe correctly
5. Git add and commit with message: `fix: secure Stripe payment validation in [filename]`

### Step 3: Verify All Files

After fixing all 6:
```bash
git log --oneline | head -6  # Verify 6 commits
grep -l "STRIPE_PAYMENT_LINKS" *.html | wc -l  # Should be 6
```

### Step 4: Testing Checklist

For EACH file, test these scenarios in browser DevTools:

```javascript
// Test 1: Normal flow works
// 1. Click $30 option
// 2. Click Book Now
// 3. Verify Stripe payment page opens
// Expected: Opens https://buy.stripe.com/... in new tab

// Test 2: DOM manipulation doesn't work (CRITICAL)
document.querySelector('[data-price="30"]').setAttribute('data-link', 'https://attacker.com');
bookNow();
// Expected: Still opens Stripe URL, NOT attacker URL

// Test 3: Modifying global variable doesn't work
selectedStripeLink = 'https://attacker.com';
bookNow();
// Expected: Opens Stripe URL, NOT attacker URL
// (This variable should no longer exist in secure version)

// Test 4: Rate limiting works
// Click button 5 times rapidly
// Expected: Only opens once, subsequent clicks blocked

// Test 5: Invalid URLs are rejected
// This is automatic with URL API - any non-HTTPS or non-buy.stripe.com fails
```

### Step 5: Commit Changes

After all files are fixed and tested:

```bash
git add street-vybz.html born-agen.html dancehall-royalty.html hot-steppaz.html motherland.html praise-flow.html

git commit -m "fix: secure Stripe payment validation and add rate limiting

- Replace weak indexOf() validation with URL API
- Use immutable whitelist instead of DOM attributes
- Add 2-second rate limiting to prevent double-clicks
- Add user confirmation modal before payment
- Add noopener,noreferrer to window.open()
- Apply fixes to all 6 shell pages consistently

Fixes security issues identified in SECURITY_REVIEW_STRIPE_PAYMENT.md:
- HIGH: DOM-based XSS via data-link manipulation
- HIGH: Weak URL validation (indexOf bypass)
- MEDIUM: Client-side URL storage is mutable
- MEDIUM: No rate limiting
- MEDIUM: No user confirmation"
```

### Step 6: Create Pull Request

```bash
gh pr create --title "Fix Stripe payment security vulnerabilities" --body "..."
```

## Key Points to Remember

1. **Same fix for all 6 files** - They all have identical vulnerable code
2. **Test after each fix** - Don't batch them without testing
3. **Use STRIPE_PAYMENT_LINKS object** - This is the core security improvement
4. **Verify window.open() has noopener,noreferrer** - For LOW issue fix
5. **Data-link attributes remain in HTML** - Just not used by JavaScript anymore
6. **Remove old selectedStripeLink global** - It's now in the STRIPE_PAYMENT_LINKS object

## File Locations

All files in: `/var/www/html/contract/daniel_projects/esha_chuby/chubydice_version_1/`

1. street-vybz.html (line ~685-702)
2. born-agen.html (similar script block)
3. dancehall-royalty.html (similar script block)
4. hot-steppaz.html (similar script block)
5. motherland.html (similar script block)
6. praise-flow.html (similar script block)

## Testing Evidence

After implementing, share screenshots of:
1. Browser payment flow working with new code
2. DevTools console showing rate limiting in action
3. Confirmation modal appearing before payment
4. Failed DOM manipulation attempt (attacker URL ignored)

## When You Have Questions

Refer to: `documents/SECURITY_REVIEW_STRIPE_PAYMENT.md`

This document has:
- Detailed explanations of each vulnerability
- Proof of concept attacks
- Why each fix is important
- Alternative implementation approaches
- Testing recommendations

## Success Criteria

- All 6 files updated consistently
- bookNow() uses URL API for validation
- STRIPE_PAYMENT_LINKS is immutable (Object.freeze)
- Rate limiting implemented (2-second cooldown)
- User confirmation modal present
- window.open includes noopener,noreferrer
- All tests pass (normal flow + security tests)
- Tests pass in multiple browsers (Chrome, Firefox, Safari)

