# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Interactive web presentation (BI Norwegian Business School keynote) — a single-page scrollable slide deck about AI adoption and professional capability frameworks. Hosted on GitHub Pages at the `aiexperience` repo.

## Architecture

Everything lives in one file: **index.html** (~1160 lines).

- **Lines 1–502**: `<style>` block — CSS custom properties, fluid typography via `clamp()`, scroll-snap layout, slide-type variants, responsive breakpoints, print stylesheet
- **Lines 503–1062**: HTML — 46 full-screen `<section class="slide">` elements organized into narrative acts (`open`, `act1`–`act4`)
- **Lines 1063–1161**: `<script>` block — navigation (arrow keys, scroll-snap, dots, progress bar), slide chooser overlay, PDF export, fullscreen toggle

No frameworks, no build tools, no dependencies. Vanilla HTML5/CSS3/JS only.

## Assets

`assets/` contains videos (`.mp4`), background images (`bg*.png`), logos, and photos. All referenced directly from `index.html`.

## Development

Open `index.html` in a browser. Edit the file directly. No build step.

**Keyboard shortcuts in the presentation**: arrow keys navigate, `c` opens slide chooser, `d` triggers PDF export, `p` toggles fullscreen.

## Deployment

Push to `main` — GitHub Pages serves from the repo root. CNAME is configured at repo level.

## Design System

CSS custom properties define the palette:
- `--orange: #FF5722`, `--lime: #D4E157`, `--dark: #0a0a0a`, `--light: #f5f5f0`
- Typography: Inter (body), Space Mono (mono), self-hosted via Google Fonts
- Fluid sizing uses `clamp()` throughout — do not use fixed `px` for text

Slide types are styled via class combinations: `video`, `speaker`, `quote`, `dramatic`, `impact`, `insight`, `content`, `dark`.

## Key Patterns

- **Scroll-snap**: Each slide is `scroll-snap-align: start` inside a `scroll-snap-type: y mandatory` container. Navigation JS syncs dots and progress bar via `IntersectionObserver`.
- **Staggered animations**: Elements use `.stagger-1` through `.stagger-6` delay classes triggered by `.active` on the slide.
- **Responsive**: Mobile hides nav dots and character matrix, collapses multi-column layouts. Always test mobile viewport when changing layout.
- **Print/PDF**: A `@media print` stylesheet ensures slides render as full pages. The `d` key triggers `window.print()`.
