# Affiliate Marketing Guide

The Zodiac Wardrobe already deep-links every outfit piece to a live search on 11 real retailers. With affiliate programs, those clicks can earn a commission when they lead to a sale — without changing the shopping experience. This guide explains the options, how to wire it into the code, and the rules you must follow.

> **Status today:** the app is **not** affiliated and the UI says so. Turning on affiliate links is a deliberate choice that comes with disclosure obligations (see *Compliance*). Don't ship it without them.

---

## Two ways to do it

### Option A — Aggregator network (recommended to start)

A single integration that monetizes *all* outbound retailer links at once. You add one script (or wrap links through one API), and it auto-converts any merchant it has a relationship with. Best fit for this app, since it links to many stores.

Common aggregators:
- **Skimlinks** and **Sovrn //Commerce** — drop-in JavaScript; outbound links are rewritten on click. Lowest effort.
- **Rakuten Advertising**, **CJ (Commission Junction)**, **Awin**, **Impact** — large networks hosting many of our retailers; more setup, more control, often better rates.
- **LTK** and **ShopMy** — creator-focused; great if the project has a personality/social presence.

Trade-off: aggregators take a cut and you have less per-merchant control, but you cover 11 stores with one approval instead of eleven.

### Option B — Direct programs per retailer

Apply to each retailer's program individually (usually *through* a network). More work and more approvals, but typically the best commission and cleanest attribution. Worth it for your top-converting stores.

---

## Where each store's program lives

Networks and terms change constantly — **always confirm on the retailer's current affiliate page before relying on this.** As a starting map (2026):

| Store | Typically via | Notes |
|---|---|---|
| Amazon | **Amazon Associates** (direct) | Easiest approval; low rates; short cookie |
| H&M | Awin / aggregators | Beginner-friendly |
| ASOS | Awin / Skimlinks | Broad catalog |
| Etsy | Awin | Unique/handmade angle |
| Macy's | Rakuten / FlexOffers | Department breadth |
| Urban Outfitters | Rakuten / aggregators | Verify current program |
| Free People | Rakuten / aggregators | Verify current program |
| Revolve | REVOLVE program / LTK | Strong for trend content |
| Nordstrom | **Rakuten Advertising** | Up to low single-digit % |
| Lululemon | **Awin** | ~30-day cookie; athletic premium |
| NET-A-PORTER | Partnerize / aggregators | Luxury; rewards editorial framing |

Don't pick a program on commission rate alone — the store your audience already trusts converts better than a higher rate they won't buy from.

---

## Wiring it into the code

All shop links come from one place: the `RSHOPS` array in `angeleno-almanac.html`, where each store has a `u(q)` function that builds its search URL. That's the single seam to monetize.

**With an aggregator script (Option A):** usually no code change at all — include the provider's snippet and it rewrites the outbound links automatically. Keep `RSHOPS` exactly as is.

**With a deep-link/affiliate URL (Option B):** wrap each destination through your network's deep-link format. Sketch:

```js
// one helper per network — example shape, not a real ID
const AFF_ID = 'YOUR_PUBLISHER_ID';
function rakuten(mid, dest, subid){
  return `https://click.linksynergy.com/deeplink?id=${AFF_ID}&mid=${mid}` +
         `&murl=${encodeURIComponent(dest)}` + (subid?`&u1=${encodeURIComponent(subid)}`:'');
}

// then in RSHOPS:
{ n:'Nordstrom', t:'premium',
  u:q => rakuten('MERCHANT_ID', `https://www.nordstrom.com/sr?keyword=${q}`) }
```

**Attribution (SubIDs):** pass a tag describing the click so you can see what converts — e.g. `sign-weather-piece` like `leo-warm-coat`. Most networks accept a SubID parameter (`u1`, `subId`, `sid`, etc.). The app already knows the sign, weather band, and piece at link-build time, so this is easy to thread through.

Keep the rule from `CONTRIBUTING.md`: links stay **live searches**, not pinned product pages, so affiliate links don't rot.

---

## Compliance (non-negotiable)

- **Disclose.** US law (FTC) requires a clear, conspicuous disclosure that links may earn commission. Replace the current "Not affiliated" line with something like *"We may earn a commission from links — it never changes which looks we show you."* Other regions (UK ASA, EU) have similar rules.
- **Don't let money bias styling.** Commission must never influence which pieces or stores get recommended. If it ever would, don't do it. Consider keeping store order neutral (or letting the user choose, as it does now).
- **Cookies/consent.** Affiliate scripts set cookies; if you serve the EU/UK, fold them into a consent banner.
- **Follow each program's terms.** Some prohibit paid search traffic, coupon framing, or certain placements. Read before you promote.
- **Tax & payments.** Commission is income; networks require tax details and have minimum payout thresholds.

---

## Measuring success

- Use SubIDs to learn which **signs**, **weather bands**, and **pieces** drive clicks and sales.
- Watch **EPC** (earnings per click) per store, not just commission rate.
- Prune stores that never convert; double down on the ones your audience trusts.

---

## A note on tone

This project's whole point is delight, not selling. Keep affiliate integration invisible and honest: the look comes first, the links stay neutral, and the disclosure is upfront. If monetization ever makes the experience worse, it isn't worth it.
