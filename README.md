# The Zodiac Wardrobe

Make your days a little more interesting with a fresh look. The Zodiac Wardrobe reads today's live Los Angeles weather and your zodiac sign, then illustrates a head-to-toe outfit with a new style prompt every day that you can shop across real stores.

## Features

- **Live LA sky** — pulls today's actual temperature, condition, and high/low, and paints a twilight hero scene with your zodiac constellation in gold.
- **Outfit per sign + weather** — combines the real forecast with each sign's fashion personality into a styled "look," palette, and finishing touches.
- **Illustrated model** — a seeded vector croquis that wears the look and adapts to the weather (shorts and a sun hat when it's hot, coat and scarf when it's cool, boots in the rain). Toggle **Minimal / Glam**, and choose skin tone, hair color, and hairstyle — the model stays "you" while the outfit changes per sign.
- **Shop the look** — pick a store, then tap any piece to open a live search for it. Filter stores by budget ($ / $$ / $$$) across 11 retailers (H&M, ASOS, Amazon, Etsy, Macy's, Urban Outfitters, Free People, Revolve, Nordstrom, Lululemon, NET-A-PORTER).

## How it works

- One self-contained HTML file — vanilla JavaScript, hand-drawn SVG, Google Fonts (Fraunces + Jost).
- Weather comes from the free [Open-Meteo](https://open-meteo.com) API, fetched in the browser. If it's unreachable, the page falls back to a pleasant default LA day so it never breaks.
- Shop links are **live search URLs**, not specific products, so they don't go stale. Not affiliated with any retailer; results vary with stock and season.

## Notes

Styling is for delight, not destiny — a small daily nudge to try something new and keep getting dressed fun.
