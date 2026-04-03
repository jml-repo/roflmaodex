# ROFLMAOdex

**Private encrypted resale rolodex — Android PWA.**

A single-file web app for tracking people, properties, and places in the resale/picker world. Who knows who, what they're into, where they frequent, and how to reach them.

## Security
- AES-256-GCM encryption before any data is stored
- Password never leaves your device
- Encryption key exists only in RAM while unlocked
- Auto-locks after 5 min inactivity or when app is backgrounded

## Features (v1.2)
- Add/edit people with interests (LP, 45, hardwood, copper, lamps, etc.)
- Tag-based interest filtering
- Connection network between people
- Global search across all fields
- Encrypted backup export/import (.enc)
- CSV export
- PWA — installable on Android via Chrome "Add to Home Screen"
- Works fully offline after first load

## Roadmap (v2)
See CHANGELOG.md for the full v2 punchlist.
- Three entity types: Person, Property, Public Place
- Multi-member connections
- Phone numbers with copy-to-clipboard
- Google Drive sync
- Long-press context menus with At a Glance popup
- Two-step delete confirmation

## Install on Android
1. Open the GitHub Pages URL in Chrome
2. Tap the three-dot menu → "Add to Home Screen"
3. Set your master password on first launch

---
Built with vanilla JS, sql.js (SQLite/WASM), and Web Crypto API.
