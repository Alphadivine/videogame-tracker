# 🎮 Game Release Tracker

A single-page web app for tracking upcoming video game releases — live countdowns, prices, editions, a budget, cross-device sync, and more. It installs as an app on your phone or desktop and works offline.

No build step, no dependencies. It's one self-contained `index.html` plus an icon, a web-app manifest, and a service worker.

---

## Features

**Tracking**
- Live countdowns to each release, sorted by soonest.
- A **Next up** hero banner, with a dynamic backdrop that themes the whole page to the next release — and follows whichever card you hover.
- **Flexible release timing:** exact date, month, quarter, year, or **TBA**. Non-exact games show an estimated window instead of a fake countdown and sort accordingly (TBA drops to the end).
- Released games get a confetti burst and auto-tuck into a collapsible **Released** section (they stay in your list).

**Your list**
- **Add a game** with type-to-search suggestions from the web — picks the cover art, release date, platforms, and official link automatically. Add a price and you're done.
- **Edit** any game (including the built-in ones) — dates, price, platforms, links, cover. Built-ins have a **Reset to default**. Games you add can be removed.
- **Priority ★ ratings** — mark how excited you are and sort by "Most anticipated".
- **Status** — mark each game Want / Pre-ordered / Got it; the **My list** filter shows just those.
- **Editions** — add Standard / Deluxe / Collector's versions with prices; pick one per game and it drives the card price and your budget.

**Money & buying**
- **Budget** — games marked Want or Pre-ordered are totalled at the top, broken down by month (Free counts as $0).
- **Buy** opens a store picker that sends you to the right storefront per platform: PlayStation Store, Microsoft/Xbox, Steam or Epic (PC), or the Nintendo eShop.
- **Prices are validated** to US format ($X.XX / Free / TBA).

**Extras**
- **▶ Trailer** and **＋ Google Calendar** buttons on every card.
- **Search, sort** (soonest / price / most anticipated) and **group by month**.
- Built-in **☔ How to use** guide.

**Sync & backup**
- **Cross-device sync** via a free **Firebase** project — set it up once (see `Cloud sync setup (Firebase).txt`), tap **Turn on sync**, and a sync code carries it to your other devices. Changes then sync **live**, both ways, in the background.
- **Manual backup** (download a file or copy a code) that needs no account.

**App**
- Installable **PWA** — add to your home screen for a full-screen app with its own icon; works offline.
- Auto-updating cache: when you re-deploy, the app refreshes to the new version on its own.

---

## Files

| File | What it is |
|------|-----------|
| `index.html` | The entire app (HTML, CSS, JS, embedded cover art) |
| `manifest.webmanifest` | App name + icons (makes it installable) |
| `sw.js` | Service worker (offline support, auto-update) |
| `icon-192.png`, `icon-512.png` | App icons |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |
| `Cloud sync setup (Firebase).txt` | One-time setup for cross-device sync |

---

## Host it on GitHub Pages

1. Create a new **public** repository (e.g. `videogame-tracker`).
2. **Add file → Upload files**, and drag in the files from this folder (`index.html`, `sw.js`, `manifest.webmanifest`, both icons, `.nojekyll`). Keep them at the repo root — `index.html` must be at the top level.
3. **Commit changes.**
4. **Settings → Pages → Build and deployment:** Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`. **Save.**
5. Wait ~1 minute. Your site goes live at `https://<your-username>.github.io/<repo-name>/`.

**To update later:** re-upload the changed file(s) to the repo — Pages redeploys automatically, and the app self-updates on next load.

The app uses relative paths and requires HTTPS (which GitHub Pages provides), so it works under the repo subpath with no changes.

---

## Moving your data between devices or hosts

Your games, edits, statuses, and ratings are stored in the browser, tied to the **exact web address** the app is served from. So a new URL (or a new device) starts empty. To carry your list over:

- **Old site:** open **☁ Sync → Copy code** (or **Download backup file**).
- **New site:** open **☁ Sync → Import**, paste the code (or load the file), **Apply**.

Or, once cloud sync is set up, just **Turn on sync** on one device and **Connect with code** on the others — it pulls everything and keeps them in step automatically.

---

## Notes

- **Storage** is per-origin `localStorage`, so it's private to your browser at that URL. Clearing site data wipes it — keep a backup or use sync.
- **Cover-art search** and **auto-fill** use Wikipedia's public API from your browser (no key). Adding a game needs a connection; once added, the cover is saved for offline use.
- **Sync** uses **Firebase Firestore**'s free tier (tens of thousands of reads/writes per day — far more than personal use needs) and updates flow **live** between devices. Your whole list, including cover art, syncs with room to spare. The manual backup always works without any account.
- Everything runs client-side. There's no server of your own and no tracking.
