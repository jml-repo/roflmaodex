# ROFLMAOdex — V2 Changelog / Issue Tracker

Started: 2026-04-02
Current version: v1.2

---

## 🔧 Known Issues / Planned Fixes for V2

### Data Model
- [ ] **Three entity types** — `entities` table replaces `people` table; `type` column is 'person', 'property', or 'public_place'; Add/Edit sheet shows a three-way toggle at top that swaps the field set:
  - **👤 Person fields:** first name, last name, hometown, current town, age, spouse/partner (linked entity), kids, pets, vehicle, notes, interests/tags, phone numbers
  - **🏠 Property fields:** nickname/label (e.g. "Bob's barn"), address, owner (linked Person), occupants (linked People), property type tag (residence, storage unit, barn, garage, etc.), notes, interests/tags, phone numbers
  - **🏢 Public Place fields:** place name, address, place type tag (flea market, auction house, antique shop, estate sale co., etc.), Google Maps link (tappable — opens Maps app), hours of operation (editable Mon–Sun grid), website, notes, interests/tags, phone numbers
  - "Look up hours" button on Public Place opens Google Maps link for manual reference — hours entered by hand to keep app free and offline-capable; true API pull deferred to V3
- [ ] **Multi-entity connections — no member limit** — a connection is a named group thread, not just a pair:
  - Fields: title/name, type tag (e.g. "regular crew," "buying group," "household," "auction circuit"), notes, date
  - Members: any number of entities of any type, each with an optional role note ("organizer," "occasional," "lives there," "runs the place," etc.)
  - Replaces the current two-person-only connection model entirely
  - Supports all combinations: Person↔Person, Person↔Property, Person↔Public Place, Place↔Place, etc.
- [ ] **Phone numbers sub-table** (`phone_numbers` linked to any entity id) — multiple numbers per entity, each with:
  - Number — auto-formatted to `234-567-8910` for display (USA/+1 assumed if no country code; non-+1 codes preserved as-entered)
  - Label (cell, home, shop, Google Voice, WhatsApp, etc.)
  - Carrier / notes (e.g. "Verizon prepaid — texts only")
  - Date gathered
  - Active toggle — inactive numbers stay in history but display dimmed
  - 📋 **Copy button** on each number row (44px+ tap target) — copies in E.164 format (`+12345678910`) for universal paste compatibility; shows "📋 Copied" toast
- [ ] **Entity type indicator on all cards and pickers** — 👤 Person · 🏠 Property · 🏢 Public Place

### Sync & Hosting
- [ ] **Google Drive sync** — encrypted `.enc` blob lives in a file in the user's own Drive (`roflmaodex.enc`); read on open, written on every save; local IndexedDB retained as offline cache/fallback:
  - One-time OAuth "Sign in with Google" flow; token stored in sessionStorage (cleared on lock)
  - Google never sees plaintext — they hold the encrypted lockbox, not the key
  - On open: pull from Drive → decrypt with password → load into SQLite
  - On every save: encrypt → push to Drive + write to local IndexedDB
  - Offline: falls back to local IndexedDB automatically; syncs to Drive next time online
  - Conflict resolution (two phones edit simultaneously): last-write-wins for V2; smarter merge logic is V3
  - **Hosting requirement:** OAuth requires the file served from a registered URL — recommend GitHub Pages (free, permanent) or any static host; one-time setup; the HTML file itself stays the single-file deliverable, just served from a URL instead of opened locally

### UX / Navigation
- [ ] **Tap-and-hold context menu on all entity cards** — long-press (500ms) shows bottom-sheet action menu:
  - 👁️ **At a Glance** — read-only popup of all fields, phone numbers, interests, and connections; layout adapts by entity type
  - 🔗 **Connections** — inline list of every connection thread this entity belongs to; tap any to expand and see all members
  - ➕ **Add to Connection** — opens connection editor with this entity pre-loaded as a member
  - ✏️ **Edit** — opens the entity editor (same as a regular tap)
  - 🗑️ **Delete** — triggers two-step confirm flow
- [ ] **Remove Delete button from inside the editor** — only accessible via long-press context menu
- [ ] **Two-step staggered delete confirmation** — affirmative button swaps sides between prompts to prevent mindless double-tap:
  - **Prompt 1:** "Are you sure you want to delete [Name]?" — Cancel (left) | ⚠️ Yes, Delete (right)
  - **Prompt 2:** "This cannot be undone. Their phone numbers, interests, and connections will also be removed." — 🗑️ Delete Forever (LEFT) | Cancel (right)
- [ ] **Import backup password** — replace native `prompt()` with in-app password dialog

---

## ✅ Completed (shipped in v1.2)

- [x] UI now renders immediately — no blank screen while sql.js loads
- [x] sql.js loads on-demand when Unlock/Create is tapped (not at startup)
- [x] All buttons have both `onclick` + `ontouchend` with double-fire prevention
- [x] Unlock button shows spinner + disabled state while loading/decrypting
- [x] Swipe-left on person cards to reveal delete
- [x] Tag picker uses tappable preset chips (LP, 45, HARDWOOD, etc.) instead of keyboard-only entry
- [x] Person picker bottom sheet replaces `<select>` dropdowns for connections
- [x] All tap targets 52px+ minimum height
- [x] `font-size: 16px` on inputs (prevents Android auto-zoom)
- [x] Custom confirm dialog replaces `window.confirm()` (except import backup — still uses `prompt()`)
- [x] Auto-lock: 5 min inactivity + visibilitychange (tab hide)
- [x] AES-256-GCM encryption via Web Crypto API
- [x] Encrypted backup export (.enc) and CSV export
- [x] PWA manifest + inline service worker for offline use

---

## 📝 Notes

- **Single file:** entire app remains one self-contained `.html` file — engine, UI, crypto, service worker all inline; served from a URL for Drive sync but the file itself doesn't change
- **First load** requires internet to fetch sql.js from CDN; after that the service worker caches everything offline
- **Drive sync hosting:** GitHub Pages is the recommended free host — push the HTML file once, get a permanent URL, done; Google OAuth client ID registration is a one-time 10-minute setup in Google Cloud Console (free tier covers all usage at personal scale)
- **Google never sees plaintext data** — the Drive file is the same AES-256-GCM encrypted blob that would otherwise sit in IndexedDB; password never leaves the device
- **V3 horizon:** true multi-device merge/conflict resolution; Google Hours of Operation API pull; possible React Native wrapper for deeper Android integration
