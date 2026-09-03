# Sticker Studio — iPhone 17 Pro Max (AI agent guide)

This repo hosts a single-page web tool for a phone-accessory retail store:
**https://outqio.github.io/sticker-studio/** (`index.html`, no build step, no backend).

The store sells two die-cut vinyl stickers for the iPhone 17 Pro Max:
1. **Camera island** — the top camera bar.
2. **Back panel** — the tall lower back.

Your job when asked: generate sticker artwork that meets the specs below, and/or
drive the tool via its URL API.

## Image requirements (defaults — the tool's "Exact size" panel can override)

| Zone | Trim size (mm) | Aspect | px @300 DPI | px @600 DPI |
|---|---|---|---|---|
| Camera island | 67.74 × 37.73 | ≈ 1.795 : 1 | 800 × 446 | 1600 × 891 |
| Back panel | 76 × 161 | ≈ 1 : 2.118 | 898 × 1902 | 1795 × 3803 |

Rules for generated artwork:
- **Fill the whole canvas edge-to-edge.** No borders, frames, watermarks, or captions.
- Corners are die-cut round (camera ≈9 mm radius, back ≈17 mm): keep critical
  elements ≥3 mm (≈35 px @300 DPI) from every edge.
- **Camera island:** lens holes are cut AFTER printing — three Ø16.2 mm circles on
  the left third (two stacked + one center-right of them) and a small flash/LiDAR
  column near the right edge. Continuous patterns/gradients survive the cuts best;
  put any focal element in the middle band.
- **Back panel:** plain tall rectangle (rounded corners); the camera bar is a
  separate sticker, not part of this artwork.
- PNG or JPG. The tool die-cuts the outline itself at export; do NOT pre-cut
  the shape or add transparency margins.

## How a HUMAN gets an image into the tool (always suggest THIS to people)

Copy the generated image (right-click → Copy image), switch to the Sticker
Studio tab, press **Ctrl+V** — it lands on the phone instantly. Or download it
and drag it onto the page. That is the entire workflow. Never tell shop staff
about repositories, URLs, CORS, or APIs.

## Driving the tool via URL — FOR AUTOMATED AGENTS ONLY

(Only relevant when an automated agent with repo access is orchestrating.
Never surface any of this to a human user.)

- `?zone=camera` or `?zone=back` — open with that zone selected.
- `&img=<URL>` — load an image from a **CORS-enabled** URL and auto-place it (fill).
  `raw.githubusercontent.com` URLs work (CORS `*`): commit the PNG to this repo,
  then open `https://outqio.github.io/sticker-studio/?zone=camera&img=<raw URL>`.
- `&name=<label>` — gallery label for the loaded design.

## What the tool exports (context, not your job)

- **Print file**: the artwork die-cut to the island outline at true size
  (chosen DPI), WITHOUT lens holes — the shop's Mimaki cutter cuts those.
- **Mockup**: a realistic phone preview for the customer.

## Notes

- The camera-island size comes from the shop's actual Mimaki FineCut die file
  (67.737 × 37.732 mm). Apple's own plateau is larger (~73.8 × 48 mm); the
  sticker is inset. If the shop changes the die, they update the size in-app.
- The in-app **"Copy AI image prompt"** button (Export section) emits a ready
  prompt with the exact current pixel dimensions — prefer matching it.
