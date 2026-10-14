# Changelog

## 2026-10 — Bold redesign: Ember look + Dashboard/Shelf views
- New **Ember** visual identity (warm orange accents on a carbon base),
  replacing the previous purple/teal. Recolored app-wide via CSS variables.
- **Cinematic hero** — the next release fills a larger hero with a big
  launch-day number + a monospace HH:MM:SS clock (was four equal boxes).
- **Horizontal cards** in Dashboard view (cover on the left, details on
  the right) for a more premium, console-store feel.
- **New Dashboard ⇄ Shelf toggle** in the controls row. Dashboard = full
  detailed cards; Shelf = an art-forward poster wall with a warmer, distinct
  accent and the heavier action rows tucked away for clean browsing. The
  chosen view is remembered per device (localStorage `gametracker_view`).
- Purely a reskin + view option: every feature, countdown, sync, status,
  edition/free-price handling and bit of logic is unchanged.

## 2026-10 — "What's new" panel
- Added a **🆕 What's new** button to the toolbar and a popup that shows the
  latest updates. It appears automatically once per app version (only the
  entries newer than your last visit), and reopens any time from the toolbar
  with the full history — older entries fold away behind "Show older updates".
- The popup never interrupts a shared read-only view; "seen" is tracked per
  device in localStorage, so bumping the version shows it once, then stops.

## 2026-10 — Per-platform release dates
- Track **different release dates per platform** for staggered launches
  (e.g. PS5 now, PC later). Add them in the Add/Edit form under "Release
  dates by platform"; the card then shows the full schedule
  ("Also: PC Mar 2027"). The main date still drives the countdown, so
  point it at whichever platform matters to you.

## 2026-10 — Discover: cleaner feed + clear item types
- Discover no longer shows games that are **already out** but have a
  future port/edition date (that was making released games look new,
  e.g. 007 First Light). It now surfaces only genuinely upcoming games.
- Each non-standard item is clearly tagged: **DLC**, **Expansion**,
  **Remaster**, or **Remake**. Month-only dates show as "Expected Mar 2027".

## 2026-10 — Genre tags & filter
- Every game now shows **genre tags** (RPG, Shooter, Horror,
  Action-Adventure, ...). Built-ins are tagged; games you add — by hand
  or from Discover — pull their genre from Wikidata (P136), and older
  added games backfill in the background.
- New **Genre** filter in the toolbar narrows the list to one genre.

## 2026-10 — Discover reliability
- Guarded against duplicated cards: `loadDiscover` now renders only the
  latest run, so double-tapping Refresh (or reopening mid-load) can't
  stack duplicates.

## 2026-10 — Discover now flags DLC & expansions
- Discover includes upcoming DLC/expansions (previously excluded) and
  marks each with a **"DLC · expansion"** badge, so add-ons for games
  that are already out are easy to spot next to brand-new releases.
  (Detected via Wikidata's "expansion add-on" / "downloadable content"
  classes; a few feed slots are reserved so DLC always surface.)

## 2026-10 — Discover polish & real covers
- De-duplicated the Discover feed (Wikidata's label service returned
  en+mul labels, which doubled rows) and capped it at 30.
- Fixed missing cover art everywhere: added `pilicense=any` to the
  Wikipedia cover lookups. Game cover art is non-free, which PageImages
  excludes by default — so Discover, the Add-game auto-fill, and the
  title suggestions now show real covers.

## 2026-10 — Discover popular upcoming games & DLC
- New **✨ Discover** panel: browse popular upcoming games and big DLC
  and add them in a tap (opens the Add form prefilled for review).
- **Keyless live feed** via the **Wikidata Query Service**, ranked by how
  many Wikipedia languages cover each game (a popularity proxy). No key,
  no signup. Optionally paste a **RAWG** key to use RAWG's feed instead.
  If neither is reachable, a hand-picked fallback list shows.
- Tapping a title prefills the Add form (date, platforms, cover, official
  link from the web). Games already on your list are marked and skipped.
## 2026-10 — Date auto-update, sharing & spending dashboard
- **Update dates** (toolbar): re-checks each upcoming game on
  Wikipedia/Wikidata and updates any release dates that have shifted.
  It only accepts an *upcoming* date and ignores past or ambiguous
  matches, so it never overwrites a good date with a wrong one.
  Changed games get a green **Date updated** badge.
- **Share your list**: publish a read-only public link (in the ☁ Sync
  panel) so friends can see what you're tracking — with an optional
  "keep it updated automatically" toggle. Opening a share link shows a
  read-only view and never touches the viewer's own saved list.
- **Spending dashboard** (📊): planned spend, spent this year, library
  value and games tracked, plus a bar chart of upcoming spend by month.
- Visual polish: keyboard focus outlines and button press feedback.
- Service worker cache bumped to `gametracker-v5`.
- **Note:** sharing needs the updated Firestore rules (adds the
  `shares` collection) — see `Firebase/firestore.rules`.

## 2026-10 — Sync reliability fix
- Fixed the sync error **"invalid-argument while saving"**: the app
  caches live DOM elements on each game object during render (`_el`
  card, `_cd` countdown), and those were being handed to Firestore,
  which rejects DOM values. Sync now strips any `_`-prefixed field,
  DOM node, function, or `undefined` before writing.
- Fixed `cloudConfigured()` to read `CLOUD` directly — a top-level
  `const` isn't a `window` property, so sync wouldn't activate even
  with valid keys.

## 2026-10 — Firebase sync
- Replaced JSONBin sync (which capped free records at 100 KB) with
  **Firebase Firestore**.
- The whole list, including embedded cover art, now syncs — no size
  limit for personal use.
- **Live two-way updates** between devices via Firestore `onSnapshot`.
- Clearer sync error messages.
- One-tap **Turn on sync** (no API key to paste).
- Service worker cache bumped to `gametracker-v4`.
