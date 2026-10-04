# Changelog

## 2026-10 — Firebase sync
- Replaced JSONBin sync (which capped free records at 100 KB) with
  **Firebase Firestore**.
- The whole list, including embedded cover art, now syncs — no size
  limit for personal use.
- **Live two-way updates** between devices via Firestore `onSnapshot`
  (no manual refresh, no polling).
- Clearer sync error messages — names the real cause (rules not
  published, domain not authorized, offline) instead of "key rejected".
- One-tap **Turn on sync** (no API key to paste).
- Service worker cache bumped to `gametracker-v4`.
