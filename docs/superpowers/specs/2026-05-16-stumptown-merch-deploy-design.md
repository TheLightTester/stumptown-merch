# Stumptown Disc Golf — Merch Page Deploy Design
**Date:** 2026-05-16

## Overview
Deploy the existing Stumptown Disc Golf merch/swag menu as a static site to Vercel, accessible via QR code. The page will be updated to match the main site's color scheme and use the real club logo.

## Files
- `index.html` — renamed from `stumptown-merch.html`, the single-page merch menu
- `logo.png` — the real Stumptown logo (to be added); referenced by `index.html`

No build tool, no framework, no `vercel.json` needed. Vercel serves static HTML at root automatically.

## Color Scheme Update
Replace current navy/cream palette with the main site's scheme (stumptowndiscgolf.org):

| Token | Old | New |
|---|---|---|
| Background | `#f7f4ee` cream | `#ffffff` white |
| Primary accent | `#2eaad1` teal | `#01add3` teal |
| Accent light | `#4bc4e8` | `#33c4e0` |
| Text main | `#1a2744` navy | `#111111` near-black |
| Text muted | `#5a6a8a` | `#555555` |
| Card background | `#fdfcfa` warm white | `#f4f4f4` light gray |
| Section labels | `#1a2744` navy bg | `#111111` black bg |

## Logo Update
- Remove the placeholder SVG disc icon from the header
- Add `<img src="logo.png" alt="Stumptown Disc Golf">` in its place
- Size: ~80px tall, auto width
- Logo is black-on-white — works cleanly on white background
- Until `logo.png` is dropped in, the header shows text only (graceful fallback)

## Deployment
1. `git init` in project folder
2. Commit `index.html`
3. Create new GitHub repo named `stumptown-merch`
4. Push to GitHub
5. Connect repo in Vercel dashboard (Import Project)
6. Deploy → URL will be something like `stumptown-merch.vercel.app`

## QR Code
- Generated after the Vercel URL is confirmed
- Tool: any free QR generator (qr-code-generator.com or similar)
- Placement: update the existing QR section on the page to include a "Merch Menu" QR card alongside the existing PayPal QR card
- The QR section already has the layout and styling for this — just needs the image

## Success Criteria
- Page is live at a `*.vercel.app` URL
- Colors match stumptowndiscgolf.org
- Real logo displays correctly
- PayPal QR still works
- Merch menu QR code points to the live URL
- Page is mobile-optimized (scanned from phone via QR code)
