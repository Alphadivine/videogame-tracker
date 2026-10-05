# Changelog

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
