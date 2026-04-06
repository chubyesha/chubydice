# Vertical Floating Menu — Social Sidebar

## Overview

A fixed-position vertical sidebar on the right side of every page, providing quick access to social media profiles, phone contact, and the location/contact page. Inspired by Jungle City Projects website.

## What Is Implemented Across All 22 Pages

- Floating vertical sidebar fixed to the right side, vertically centered
- 5 icon buttons stacked vertically:
  - **Instagram** — opens instagram.com/chuby_dice in new tab
  - **Facebook** — opens facebook.com/chubydice in new tab
  - **TikTok** — opens tiktok.com/@chuby_dice in new tab
  - **Phone** — triggers native dialer (tel:+61449726776)
  - **Location** — navigates to contact.html
- Hover effects: icons scale up (1.12x), background fills yellow, tooltip label appears to the left
- Keyboard accessible: focus-visible outline + tooltips show on keyboard focus
- Mobile: hidden below 768px (social links still available in footer)
- z-index 950: sits below nav (1000) and menu overlay (999)
- Accessibility: aria-label on all links, aria-hidden on decorative SVGs, semantic `<aside>` landmark

## Icon Specifications

| Icon | Size | Gap | Border |
|------|------|-----|--------|
| Container | 44px x 44px circle | 12px vertical | 1.5px solid yellow |
| SVG | 20px x 20px | — | — |

## Social Links Reference

| Platform | URL | Opens In |
|----------|-----|----------|
| Instagram | https://www.instagram.com/chuby_dice | New tab |
| Facebook | https://www.facebook.com/chubydice | New tab |
| TikTok | https://www.tiktok.com/@chuby_dice | New tab |
| Phone | tel:+61449726776 | Native dialer |
| Location | contact.html | Same tab |

## How to Update a Social Link

1. Open any HTML page
2. Find the `<!-- FLOATING SOCIAL SIDEBAR -->` section (near the top of `<body>`)
3. Edit the `href` attribute of the relevant `<a>` tag
4. Repeat across all 22 pages (or use find-and-replace across files)

## How to Add or Remove an Icon

### Adding a new icon:
1. Add a new `<a>` element inside the `<aside class="floating-sidebar">` block
2. Use the same structure: `class="sidebar-icon"`, `data-tooltip="LABEL"`, `aria-label="Description"`
3. Include an SVG icon with `aria-hidden="true"`
4. If 6+ icons, consider reducing gap from 12px to 10px in CSS

### Removing an icon:
1. Delete the entire `<a>...</a>` block for that icon
2. If fewer than 4 icons, consider increasing gap from 12px to 16px

## CSS Location

The sidebar styles are in each page's `<style>` block under the comment:
```
/* --- FLOATING SOCIAL SIDEBAR --- */
```

Key CSS classes:
- `.floating-sidebar` — the fixed container
- `.sidebar-icon` — each circular button
- `.sidebar-icon::after` — the hover/focus tooltip
- `@media (max-width: 767px)` — mobile hide rule

## z-index Stack

| Element | z-index |
|---------|---------|
| Nav bar | 1000 |
| Menu overlay | 999 |
| **Floating sidebar** | **950** |
| Page content | 0-2 |

## Theme Colors

- Icon default: yellow outline (#F5C518) on transparent dark
- Icon hover: yellow fill with black icon
- Tooltip: white text on black background with dark border
