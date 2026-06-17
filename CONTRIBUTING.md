# Contributing to The Zodiac Wardrobe

Thanks for wanting to help make getting dressed more fun. This is a small, self-contained project and contributions of all sizes are welcome — a new hairstyle, a fixed link, a kinder color palette, a bug report.

## What we'd love most ✦

Two areas are wide open, and we **actively want** help here:

- **More store links.** More retailers across every budget tier, and more *specific*, better-targeted links for each piece. If you know a store's exact search-URL format — or a great niche, vintage, sustainable, plus-size, or local shop — please add it. The more places people can shop a look, the better this gets. Don't be shy about opening a PR that just adds stores.
- **More variations.** More hairstyles, hair textures and colors, skin tones, outfit pieces per weather band, accessories, and per-sign styling. Every new variation makes the wardrobe feel more personal and inclusive. Bring your eye.

If you're deciding what to work on, start with one of these.

## Ground rules

A few constraints keep the project easy to run and easy to trust. Please keep changes within them:

- **Single file, no build.** Everything lives in `angeleno-almanac.html` — vanilla JavaScript, hand-drawn SVG, and inline CSS. No bundler, no framework, no install step.
- **No new runtime dependencies.** The only external calls are Google Fonts and the free [Open-Meteo](https://open-meteo.com) weather API. Don't add npm packages, trackers, or API keys.
- **No browser storage.** Don't use `localStorage` or `sessionStorage`; keep state in plain JS variables.
- **Accessibility matters.** Keep focus styles, `aria-label`s, and `prefers-reduced-motion` support intact. New controls should be keyboard-operable.
- **Stay kind.** Styling copy is for delight, not judgment. Keep skin tones inclusive and language body-positive.

## Getting started

1. Fork and clone the repo.
2. Open `angeleno-almanac.html` in any modern browser — that's it.
3. Make your change, refresh, and check it across a few zodiac signs, both styles (Minimal / Glam), and a couple of weather conditions.

## How to test

There's no framework, but please sanity-check before opening a PR:

- **Syntax:** extract the inline script and run `node --check`. Nothing should error.
- **Render sweep (recommended for figure changes):** the illustration has ~960 combinations (styles × hairstyles × weather bands × signs). A small Node harness that stubs the DOM and calls `buildFigure()` across all of them, asserting each returns one valid `<svg>` with no `undefined`/`NaN`, catches most regressions. Run it before and after your change.
- Eyeball the result on mobile width too — the layout is responsive and shouldn't overflow.

## Where to contribute

**Add or refine a retailer** (`RSHOPS`) — *especially welcome*
- Each entry is `{n, t, u}`: display name, budget tier (`budget` / `mid` / `premium`), and a function that builds a **live search URL** from an encoded query.
- We prefer live search links over specific product pages because product URLs go stale fast — but a more *specific* search (better keywords, a category deep-link, a brand-scoped query) is a great contribution. If you add a deep-link that could change, note it so we can keep an eye on it.
- **Verify the store's current search-URL format before adding it** — a dead link is worse than no link. Mention how you tested it in the PR.
- New tiers, regions, or specialty categories (vintage, sustainable, plus-size, petite, menswear) are all fair game.

**Add a hairstyle** (`buildHair`)
- Return `{back, front}` SVG strings relative to the head at `(130, 72)`.
- Always include the `crown` (or equivalent) in `front` so the scalp is covered — hair drawn only in `back` gets painted over by the head and looks bald.
- Register the new key in `HAIRSTYLES` and `HAIRLABEL`.

**Tune the figure proportions** (`buildFigure`)
- Proportions are driven by a few named anchors (`SHO`, `WAI`, `HIP`, `WR`, `L`). Keep `HIP` near the vertical midpoint of head-top→feet so torso and legs stay balanced.

**Edit zodiac styling** (`SIGNS`)
- Each sign has an element, palette, signature pieces, accessory, and a one-line philosophy. Keep palettes to three named swatches.

**Weather logic** (`band`, `buildLook`, `shopItems`)
- Temperature bands and conditions drive the outfit. New garments should map cleanly onto an existing band.

## Pull requests

- Keep PRs focused — one feature or fix at a time.
- Describe what changed and how you tested it. Screenshots of the affected look(s) are very helpful.
- Match the existing code style (compact, descriptive variable names, comments where geometry is non-obvious).

## Reporting issues

Open an issue with: what you saw, what you expected, your browser, the zodiac sign / style / weather involved, and a screenshot if it's visual. Small, reproducible reports get fixed fastest.

Have fun with it. ✦
