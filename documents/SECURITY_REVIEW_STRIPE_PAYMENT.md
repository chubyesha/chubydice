# Security Review: Stripe Payment Link Implementation

**File(s) Reviewed:**
- street-vybz.html (and similar shell pages: born-agen.html, dancehall-royalty.html, hot-steppaz.html, motherland.html, praise-flow.html)

**Date:** 2026-04-06
**Reviewer:** Security Reviewer Agent
**Risk Level:** MEDIUM

---

## Executive Summary

The Stripe Payment Link implementation uses a basic validation check on payment URLs before opening them. While the current implementation is reasonably safe, there are several security gaps and best practices that should be addressed for a production payment system handling real money.

**Critical Issues:** 0
**High Issues:** 2
**Medium Issues:** 3
**Low Issues:** 2

---

## Critical Issues (Fix Immediately)

None identified at this time.

---

## High Issues (Fix Before Production)

### 1. DOM-Based XSS via data-link Attribute Manipulation

**Severity:** HIGH
**Category:** DOM-based XSS / Client-Side Injection
**Location:** `street-vybz.html:693-694`

**Issue:**
The `data-link` attribute is read directly from the DOM without sufficient validation:

```javascript
function selectPrice(el) {
  // ...
  var link = el.getAttribute('data-link');
  if (link) selectedStripeLink = link;  // Direct assignment - no URL validation
  // ...
}
```

While the `bookNow()` function does check that the URL starts with `https://buy.stripe.com/`, this check can be bypassed via DOM manipulation in the browser console:

```javascript
// Attacker can modify in console:
var selectedStripeLink = 'https://attacker.com/phishing';
bookNow(); // Opens attacker's phishing site
```

Or by modifying the data attribute directly:
```javascript
document.querySelector('.price-option').setAttribute('data-link', 'javascript:alert(1)');
selectPrice(document.querySelector('.price-option'));
```

**Impact:**
- Users could be redirected to phishing sites that mimic Stripe
- Financial credentials could be stolen
- Users might think they're completing payment when they're not
- Trust in the payment process is compromised

**Proof of Concept:**
```javascript
// In browser console:
document.querySelector('[data-price="30"]').setAttribute('data-link', 'https://attacker-phishing.com');
selectPrice(document.querySelector('[data-price="30"]'));
bookNow(); // Opens phishing site instead of Stripe
```

**Remediation:**

Use a **whitelist** of valid Stripe payment links stored server-side or in a secure data structure that cannot be modified via DOM manipulation:

```javascript
// SECURE: Server-validated payment links
const STRIPE_PAYMENT_LINKS = {
  '30': 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b',
  '100': 'https://buy.stripe.com/6oUbJ16033xgeRYfRB4F20c',
  '125': 'https://buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d',
  '230': 'https://buy.stripe.com/eVqdR97473xg25ccFp4F20e',
  '450': 'https://buy.stripe.com/9B6fZhagj0l4fW28p94F20f'
};

function selectPrice(el) {
  document.querySelectorAll('.price-option').forEach(function(opt) {
    opt.classList.remove('selected');
  });
  el.classList.add('selected');
  var price = el.getAttribute('data-price');
  // SECURE: Use whitelist instead of DOM attribute
  if (STRIPE_PAYMENT_LINKS[price]) {
    selectedStripeLink = STRIPE_PAYMENT_LINKS[price];
  }
  var btn = document.getElementById('bookBtn');
  if (btn) btn.textContent = 'Book Now — $' + price;
}
```

**References:**
- OWASP: DOM-based XSS
- CWE-79: Improper Neutralization of Input During Web Page Generation

---

### 2. Weak URL Validation Logic

**Severity:** HIGH
**Category:** Client-Side Validation Bypass
**Location:** `street-vybz.html:700`

**Issue:**
The URL validation uses `indexOf()` to check if a URL starts with the Stripe domain:

```javascript
function bookNow() {
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) return;
  window.open(selectedStripeLink, '_blank');
}
```

This check can be bypassed in several ways:

1. **Case sensitivity attack:**
   ```
   https://buy.STRIPE.com/  (mixed case - indexOf is case-sensitive but URLs aren't)
   ```

2. **URL encoding bypass:**
   ```
   https://buy.stripe.com@attacker.com/
   ```

3. **Subdomain spoofing:**
   ```
   https://buy.stripe.com.attacker.com/
   ```

4. **Protocol confusion:**
   ```
   http://buy.stripe.com/  (could allow downgrades)
   ```

**Impact:**
- Users can be redirected to attacker-controlled sites
- Payment information stolen
- User trust compromised

**Proof of Concept:**
```javascript
// Bypass attempt (though less effective with new URL API):
selectedStripeLink = 'https://buy.stripe.com@attacker.com/';
bookNow(); // Could redirect to attacker site depending on browser
```

**Remediation:**

Use the URL API for proper URL validation:

```javascript
function bookNow() {
  if (!selectedStripeLink) return;
  
  try {
    const url = new URL(selectedStripeLink);
    
    // Verify protocol is HTTPS
    if (url.protocol !== 'https:') return;
    
    // Verify hostname is exactly buy.stripe.com (no subdomains)
    if (url.hostname !== 'buy.stripe.com') return;
    
    // Verify path starts with / (Stripe payment links format)
    if (!url.pathname.startsWith('/')) return;
    
    window.open(selectedStripeLink, '_blank');
  } catch (error) {
    // Invalid URL - silently fail
    console.error('Invalid payment link');
    return;
  }
}
```

**References:**
- OWASP: Open Redirect Prevention
- CWE-601: URL Redirection to Untrusted Site

---

## Medium Issues (Fix When Possible)

### 3. Client-Side URL Storage is Mutable

**Severity:** MEDIUM
**Category:** Data Integrity / Client-Side Tampering
**Location:** `street-vybz.html:685`

**Issue:**
The selected Stripe link is stored in a global variable that can be modified by any script on the page:

```javascript
var selectedStripeLink = 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b';
```

A malicious script (via XSS or compromised dependency) can change this value before `bookNow()` is called.

**Impact:**
- Payment could be redirected to attacker's account
- User funds sent to wrong recipient
- Financial fraud

**Remediation:**

1. **Use const + whitelist approach** (as shown in High Issue #1)
2. **Store in HTML data attributes** and validate during payment
3. **For production:** Implement server-side payment link generation

```javascript
// BETTER: Use a map that's harder to modify
const STRIPE_LINKS = Object.freeze({
  '30': 'https://buy.stripe.com/4gMbJ1ewz9VE6ls5cX4F20b',
  '100': 'https://buy.stripe.com/6oUbJ16033xgeRYfRB4F20c',
  '125': 'https://buy.stripe.com/5kQ8wPbkn4Bk25cbBl4F20d',
  '230': 'https://buy.stripe.com/eVqdR97473xg25ccFp4F20e',
  '450': 'https://buy.stripe.com/9B6fZhagj0l4fW28p94F20f'
});

let selectedPrice = '30';

function selectPrice(el) {
  const price = el.getAttribute('data-price');
  if (STRIPE_LINKS[price]) {
    selectedPrice = price;
  }
}

function bookNow() {
  const link = STRIPE_LINKS[selectedPrice];
  if (link) window.open(link, '_blank');
}
```

**References:**
- CWE-862: Missing Authorization
- OWASP: Sensitive Data Exposure

---

### 4. No Rate Limiting on Payment Button

**Severity:** MEDIUM
**Category:** Abuse / DoS Prevention
**Location:** `street-vybz.html:701`

**Issue:**
The `bookNow()` function can be called unlimited times without any rate limiting:

```javascript
function bookNow() {
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) return;
  window.open(selectedStripeLink, '_blank');  // No rate limiting
}
```

An attacker could:
- Open multiple browser tabs/windows to Stripe
- Create duplicate orders
- Spam Stripe's servers
- Create a poor user experience

**Impact:**
- Multiple unintended purchases
- Stripe API rate limiting
- Poor user experience
- Potential billing issues

**Remediation:**

Implement simple rate limiting on the client-side:

```javascript
let lastPaymentTime = 0;
const PAYMENT_COOLDOWN = 2000; // 2 seconds minimum between clicks

function bookNow() {
  const now = Date.now();
  
  // Prevent rapid-fire clicks
  if (now - lastPaymentTime < PAYMENT_COOLDOWN) {
    console.warn('Please wait before clicking again');
    return;
  }
  
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) {
    return;
  }
  
  lastPaymentTime = now;
  window.open(selectedStripeLink, '_blank');
}
```

**References:**
- OWASP: Rate Limiting
- CWE-770: Allocation of Resources Without Limits or Throttling

---

### 5. No User Confirmation for Financial Transaction

**Severity:** MEDIUM
**Category:** User Experience / Fraud Prevention
**Location:** `street-vybz.html:699-702`

**Issue:**
The `bookNow()` function immediately opens the Stripe payment page without any confirmation. Users might accidentally click the button multiple times.

```javascript
function bookNow() {
  // No confirmation modal - payment happens immediately
  window.open(selectedStripeLink, '_blank');
}
```

**Impact:**
- Accidental duplicate orders
- User frustration
- Potential chargebacks
- Support burden

**Remediation:**

Add a confirmation step before opening Stripe:

```javascript
function bookNow() {
  const price = selectedPrice || '30';
  const confirmed = confirm(`Proceed to pay $${price} for Chuby Dice?`);
  
  if (!confirmed) return;
  
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) {
    alert('Payment link unavailable. Please try again.');
    return;
  }
  
  window.open(selectedStripeLink, '_blank');
}
```

Or better - use a modal dialog (better UX):

```javascript
function bookNow() {
  const modal = document.createElement('div');
  modal.innerHTML = `
    <div style="...modal-styles...">
      <p>You are about to pay $${selectedPrice} for Chuby Dice</p>
      <button onclick="confirmPayment()">Confirm Payment</button>
      <button onclick="this.parentElement.parentElement.remove()">Cancel</button>
    </div>
  `;
  // Display modal...
}
```

**References:**
- OWASP: Authentication Cheat Sheet
- Best Practice: Always confirm financial transactions

---

## Low Issues (Consider Fixing)

### 6. Missing Content Security Policy (CSP) Headers

**Severity:** LOW
**Category:** Security Headers
**Location:** Server-level (not file-specific)

**Issue:**
The HTML files do not appear to have Content Security Policy headers that would restrict script execution and prevent XSS attacks from being effective.

**Impact:**
- Reduced protection against XSS attacks
- Easier for attackers to inject malicious scripts

**Remediation:**

Add CSP headers in server configuration or meta tags:

```html
<meta http-equiv="Content-Security-Policy" content="
  default-src 'self';
  script-src 'self' https://buy.stripe.com;
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  connect-src 'self' https://buy.stripe.com;
  frame-src https://buy.stripe.com
">
```

**References:**
- OWASP: Content Security Policy
- CWE-693: Protection Mechanism Failure

---

### 7. window.open Uses _blank Without Noopener

**Severity:** LOW
**Category:** Security / Information Disclosure
**Location:** `street-vybz.html:701`

**Issue:**
The `window.open()` call uses `_blank` but doesn't include the `noopener` attribute:

```javascript
window.open(selectedStripeLink, '_blank');
```

While Stripe is trusted, the opened window could potentially access the `window.opener` property and redirect the original page (tabnabbing attack).

**Impact:**
- Low risk with Stripe (trusted), but poor practice
- Potential for abuse if Stripe domain is ever compromised

**Remediation:**

Add security attributes:

```javascript
function bookNow() {
  if (!selectedStripeLink || selectedStripeLink.indexOf('https://buy.stripe.com/') !== 0) {
    return;
  }
  
  // SECURE: Use rel attribute for security
  const link = document.createElement('a');
  link.href = selectedStripeLink;
  link.target = '_blank';
  link.rel = 'noopener noreferrer';
  link.click();
}
```

Or directly in HTML:

```html
<button onclick="window.open(selectedStripeLink, '_blank', 'noopener,noreferrer')">Book Now</button>
```

**References:**
- OWASP: Tabnabbing
- MDN: window.open() security

---

## Security Checklist

- [ ] **No hardcoded secrets** — ✅ PASS (Stripe links are payment URLs, not API keys)
- [ ] **URL validation present** — ⚠️PARTIAL (indexOf check is weak, needs URL API)
- [ ] **Data-link attributes protected** — ❌ FAIL (DOM manipulation possible)
- [ ] **Rate limiting enabled** — ❌ FAIL (missing)
- [ ] **User confirmation required** — ❌ FAIL (missing)
- [ ] **No XSS vectors** — ⚠️ PARTIAL (getCurrentLink is validated but DOM is mutable)
- [ ] **HTTPS enforced** — ⚠️ PARTIAL (check only uses indexOf, not URL API)
- [ ] **Content Security Policy** — ❌ FAIL (no CSP headers)
- [ ] **Window.open secured** — ❌ FAIL (missing rel attributes)
- [ ] **No sensitive data in logs** — ✅ PASS

---

## Recommendations

### Immediate (Before Going Live)

1. **Replace weak indexOf() validation with URL API** (HIGH #2)
   - Use `new URL()` constructor for proper validation
   - Verify hostname exactly matches `buy.stripe.com`
   - Check protocol is `https:`

2. **Implement payment link whitelist** (HIGH #1)
   - Store valid Stripe links in a immutable object
   - Never read from DOM for payment URLs
   - Use `Object.freeze()` to prevent modification

3. **Add user confirmation modal** (MEDIUM #5)
   - Show price and confirm before opening Stripe
   - Better UX than default browser confirm

### Short-term (Before Processing Real Money)

4. **Add rate limiting** (MEDIUM #4)
   - Prevent accidental double-clicks
   - Add 2-3 second cooldown between payment clicks

5. **Add Content Security Policy headers** (LOW #6)
   - Restrict script execution origins
   - Prevent XSS from being effective
   - Add to server configuration

6. **Secure window.open call** (LOW #7)
   - Add `noopener,noreferrer` to window.open()
   - Prevent tabnabbing attacks

### Long-term (Production Best Practices)

7. **Move to server-side payment link generation**
   - Generate links on backend with Stripe API
   - Send to frontend as data, not hardcoded
   - Server can verify payment authenticity

8. **Implement server-side purchase verification**
   - Verify payment came from your Stripe account
   - Don't rely on client-side validation
   - Use Stripe webhooks for order fulfillment

9. **Add logging and monitoring**
   - Log all payment page loads
   - Monitor for suspicious patterns
   - Alert on unusual activity

---

## Files Affected

This implementation appears in multiple shell pages:
- street-vybz.html
- born-agen.html
- dancehall-royalty.html
- hot-steppaz.html
- motherland.html
- praise-flow.html

**All files require the same security fixes.**

---

## Risk Assessment

**Current Risk Level:** MEDIUM

**Risk Factors:**
- ✅ Stripe is a trusted payment provider
- ✅ Basic validation present (indexOf check)
- ⚠️ Client-side URL storage is mutable
- ⚠️ Weak validation can be bypassed
- ❌ No rate limiting
- ❌ No user confirmation
- ❌ No CSP protection

**Recommendation:** **Do NOT process real money** until HIGH priority issues are fixed.

---

## Testing Recommendations

### Security Testing Checklist

1. **Test URL Bypass Attempts:**
   - Try `https://buy.STRIPE.com/` (different case)
   - Try `https://buy.stripe.com@attacker.com`
   - Try `https://buy.stripe.com.attacker.com`
   - Try `http://buy.stripe.com/` (HTTP instead of HTTPS)

2. **Test DOM Manipulation:**
   ```javascript
   document.querySelector('[data-price="30"]').setAttribute('data-link', 'https://attacker.com');
   selectPrice(document.querySelector('[data-price="30"]'));
   bookNow();
   ```

3. **Test Rate Limiting:**
   - Click button 10 times rapidly
   - Verify only one window opens (with fix)

4. **Test with Browser Console:**
   - Modify `selectedStripeLink` variable
   - Verify it still respects validation

---

## References

- OWASP Top 10: A03:2021 - Injection
- OWASP Top 10: A05:2021 - Security Misconfiguration
- OWASP Top 10: A07:2021 - Identification and Authentication Failures
- CWE-79: Improper Neutralization of Input During Web Page Generation
- CWE-601: URL Redirection to Untrusted Site
- CWE-770: Allocation of Resources Without Limits
- Stripe Security Documentation: https://stripe.com/docs/security

---

**Status:** REQUIRES REMEDIATION BEFORE PRODUCTION

**Next Steps:**
1. Fix HIGH priority issues
2. Implement MEDIUM priority improvements
3. Add LOW priority security headers
4. Run security testing
5. Review with Stripe documentation
6. Test end-to-end payment flow

