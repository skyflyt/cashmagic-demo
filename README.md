# Cash Magic — site redesign (first pass, 2026-08-27)

Full revamp of cashmagiccasino.com. **Single self-contained `index.html`** — no build step,
no dependencies, official logo embedded as a data URI. Deploy anywhere static.

## What it is
- Hash-routed views: Home · Locations · Rewards · Careers · Contact (footer keeps
  Privacy/Terms/Responsible Gaming links pointing at the live site for now).
- **Location finder is the centerpiece** (Steve's ask): interactive Louisiana outline
  (simplified from public-domain state-boundary GeoJSON, equirectangular projection),
  26 star markers with collision-relaxed positions for the tight clusters (Amite Hwy 16
  trio, Vinton pair, Houma trio, Berwick pair). Click/tap/keyboard opens a glass popout —
  parish, 24/7 badge, address, phone (tel:), amenities, Directions (Google Maps) + Call.
  Bottom-sheet popout on phones.
- **Light theme default** (marketing-friendly), dark "casino night" theme behind the
  header sun/moon toggle (persisted in localStorage).
- All 26 locations crawled from the live site 2026-08-27 (`crawl/` has the full dump).
  Manager names/photos deliberately dropped (too hard to keep current).

## Stubs — wiring points for later
- **Rewards** (`data-stub="rewards-balance"` / `"rewards-enroll"`): forms are live UI,
  handlers call `window.REWARDS_STUB.checkBalance/enroll` and show a "coming soon" notice.
  The OLD site does this via on-site WordPress forms (not an external service) —
  `/rewards-club/check-your-balance/` + `/enroll-your-card/`. Replace REWARDS_STUB when
  the rewards backend is chosen.
- **Contact form** (`data-stub="contact-form"`): composes a mailto to
  cashmagiccontact@cashmagic.com (zero-hosting-cost). Swap for a form service
  (Cloudflare Worker, Formspree, etc.) later.
- Careers "Search Job Openings" links to the live UKG/SaaShr ATS — real and working.

## Fixed vs. the live site
- Live-site bug: Fuel & Stores page shows ccowie@bhwk.com but the mailto points at
  jladner@bhwk.com. New site links ccowie@bhwk.com correctly (on the Contact page).

## Hosting plan
- Demo: local file / any static host.
- Approved → **Cloudflare Pages free tier** (or Netlify) on a bhwk-owned account —
  one static file, ~173 KB, VERY low traffic. `www.cashmagiccasino.com` CNAME cut-over
  when ready. Production `<title>` to restore: see comment at top of index.html.

## Files
- `index.html` — the site (theme, map data, and JS are all inline and commented)
- `crawl/site-content.md` — exhaustive content dump of the old site
- `crawl/locations.json` — structured 26-location dataset (lat/lng included)
- `crawl/la-path.js` — Louisiana outline path + projection (source for the inline copy)
