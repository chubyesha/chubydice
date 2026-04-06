# Animated Gradient Orbs Background

## Overview

4 animated gradient orbs float across every page as ambient background decoration. They create a subtle, dynamic glow effect inspired by Version 2's design. The orbs are purely decorative — non-interactive and accessible.

## Orb Specifications

| Orb | Color | Size (Desktop) | Size (Mobile) | Position | Animation | Duration |
|-----|-------|-----------------|---------------|----------|-----------|----------|
| Orb 1 | Purple `rgba(124,58,237,0.22)` | 700px | 350px | Top-left | orbFloat1 | 18s |
| Orb 2 | Yellow `rgba(245,197,24,0.12)` | 500px | 250px | Right side | orbFloat2 | 22s |
| Orb 3 | Green `rgba(6,214,160,0.1)` | 400px | 200px | Bottom-left | orbFloat3 | 16s |
| Orb 4 | Pink `rgba(244,114,182,0.1)` | 300px | 150px | Bottom-right | orbFloat1 reverse | 20s |

## How It Works

### CSS Architecture

- `position: fixed` — orbs stay in viewport as user scrolls
- `z-index: 1` — floats above the body's dark background, below content
- `filter: blur(90px)` — soft ambient glow, no hard edges
- `will-change: transform` — GPU accelerated for smooth animation
- `pointer-events: none` — clicks pass through to content below
- `border-radius: 50%` — circular shape

### Section Transparency

For orbs to be visible, section backgrounds must be transparent:

- **Transparent sections**: `#series`, `#artist`, `#academy`, `#vibes`, `#connect`, `footer`, `.big-tile-section`, `#clash-section`, `#coaching-section`
- **Body**: keeps `background: var(--black)` as the dark base layer
- **Hero**: keeps its own opaque background (needed for video backdrop)
- **Cards/tiles**: `.s-card`, `.tile`, `.card-bg` keep their own backgrounds — unaffected

### z-index Stack

| Element | z-index | Notes |
|---------|---------|-------|
| Nav bar | 1000 | Always on top |
| Menu overlay | 999 | Below nav |
| Floating sidebar | 950 | Below menu |
| **Gradient orbs** | **1** | Above body bg, below content |
| Body background | — | Base dark layer |

## HTML Structure

Located after `<body>`, before the floating social sidebar:

```html
<!-- ANIMATED GRADIENT ORBS -->
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>
<div class="orb orb-4"></div>
```

## CSS Location

In each page's `<style>` block under the comment:
```
/* --- ANIMATED GRADIENT ORBS --- */
```

## Keyframe Animations

```css
@keyframes orbFloat1 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(60px, 40px) scale(1.08); }
  66% { transform: translate(-40px, 60px) scale(0.95); }
}
@keyframes orbFloat2 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  40% { transform: translate(-80px, 30px) scale(1.05); }
  70% { transform: translate(30px, -50px) scale(0.92); }
}
@keyframes orbFloat3 {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(50px, -70px) scale(1.1); }
}
```

## Mobile Behavior

Below 768px, orb sizes are halved to reduce GPU load:

| Orb | Desktop | Mobile |
|-----|---------|--------|
| Orb 1 | 700px | 350px |
| Orb 2 | 500px | 250px |
| Orb 3 | 400px | 200px |
| Orb 4 | 300px | 150px |

## Accessibility

- `prefers-reduced-motion: reduce` disables all orb animations
- Orbs are decorative only — no semantic meaning, no ARIA roles needed
- `pointer-events: none` ensures no interaction interference

## How to Adjust Orb Colors

Edit the `radial-gradient` in each `.orb-N` CSS rule. The format is:

```css
background: radial-gradient(circle, rgba(R, G, B, OPACITY) 0%, transparent 70%);
```

- **R, G, B**: color values (0-255)
- **OPACITY**: how visible the orb is (0.1 = subtle, 0.3 = prominent)
- Keep opacity below 0.25 to avoid obscuring text

## How to Adjust Orb Size or Position

Edit the corresponding `.orb-N` CSS rule:

```css
.orb-1 {
  width: 700px; height: 700px;    /* Size */
  top: -200px; left: -150px;       /* Position */
  animation: orbFloat1 18s ...;    /* Speed */
}
```

## How to Add a 5th Orb

1. Add HTML: `<div class="orb orb-5"></div>` after the existing orbs
2. Add CSS for `.orb-5` with desired color, size, position, and animation
3. Add a mobile media query rule to reduce its size
4. Apply across all 22 pages

## Troubleshooting

### Orbs not visible on a section
The section likely has an opaque background. Change it to `background: transparent`.

### Orbs causing jank on mobile
Reduce orb sizes further in the `@media (max-width: 768px)` rule, or hide specific orbs on mobile with `display: none`.

### Orbs appearing above text
Verify `z-index: 1` on orbs. Content sections in normal flow render above fixed elements at z-index 1. If a specific element is hidden behind orbs, add `position: relative; z-index: 2` to that element.
