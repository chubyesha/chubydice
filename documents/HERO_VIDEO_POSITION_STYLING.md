# Hero Video Position Styling Guide

## Overview

The homepage hero section uses a full-screen background video (`videos/hero-bg.mp4`) with `object-fit: cover`. Because the video is cropped to fill the viewport, a CSS custom property controls where the vertical crop anchor sits — determining whether faces, chests, or feet are visible.

## How to Tune the Video Position

Open `index.html`, find the `:root` section (near the top of the `<style>` block), and change the `--hero-video-y` value:

```css
:root {
  /* ...other variables... */
  --hero-video-y: 20%; /* Tune this: 0%=top, 50%=center, 100%=bottom */
}
```

Save the file and refresh the browser to see the change.

## Value Reference

| Value | Effect | Notes |
|-------|--------|-------|
| `0%` | Anchored to top of video frame | Shows sky/ceiling — too high |
| `20%` | Sweet spot (current default) | Shows dancer faces + upper body dancing |
| `35%` | Between top and center | More body visible, faces near top edge |
| `50%` | Dead center | Tends to show chests, faces cropped off |
| `75%` | Between center and bottom | Shows lower body, faces fully cropped |
| `100%` | Anchored to bottom of video frame | Shows feet/floor only |

## Technical Details

- **CSS Property**: `object-position: center var(--hero-video-y)`
- **Applied to**: `#hero video` in `index.html`
- **Video file**: `videos/hero-bg.mp4` (11MB, merged mashup of dance clips)
- **Display mode**: `object-fit: cover` — video fills entire hero section, excess is cropped
- **Overlay**: A gradient overlay (`#hero::before`) sits above the video for text readability

## If the Video File Changes

When replacing `hero-bg.mp4` with a new video, the 20% sweet spot may no longer be ideal. Re-tune `--hero-video-y` by:

1. Set to `50%` (center) as baseline
2. If faces are cut off at top, decrease the value (try `30%`, then `20%`)
3. If too much sky/ceiling shows, increase the value (try `25%`, then `35%`)
4. Save and refresh after each change until the framing looks right
