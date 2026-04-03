# ROFLMAOdex

**Private encrypted resale rolodex — Android PWA.**

Vibecoded by Jamie — Written by [Anthropic Claude](https://anthropic.com)

A single-file web app for tracking people, properties, and places in the resale/picker world. Who knows who, what they're into, where they frequent, and how to reach them. All data encrypted on your device.

---

## Security

- All data encrypted with **AES-256-GCM** before storage
- Password never leaves your device
- Encryption key exists only in RAM while unlocked
- Auto-locks after 5 minutes of inactivity or when app is backgrounded
- Google Drive sync: encrypted blob only — Google never sees plaintext

---

## Features (v2.0)

**Three entity types**
- 👤 **Person** — name, hometown, current town, age, spouse/partner (linked), kids, pets, vehicle, phone numbers, interests
- 🏠 **Property** — nickname, address, type, owner (linked), phone numbers, interests
- 🏢 **Public Place** — name, address, type, Google Maps link, hours of operation (Mon–Sun grid), website, phone numbers, interests

**Connections**
- Multi-member connection threads — no limit on members
- Any mix of entity types in one connection
- Each member gets an optional role note
- Named threads with type tags and notes

**Phone Numbers**
- Multiple numbers per entity
- Display format: `234-567-8910` (USA assumed if no country code)
- 📋 Copy button copies in E.164 format (`+12345678910`) for universal paste compatibility
- Label, carrier notes, date gathered, active toggle per number

**Interface**
- Long-press any card (500ms) for context menu: At a Glance · Connections · Add to Connection · Edit · Delete
- At a Glance read-only popup — adapts layout by entity type
- Two-step staggered delete confirmation — button positions swap to prevent accidental double-tap
- Filter chips on main list: All / People / Properties / Places
- Tag-based interest filtering
- Global search across all fields

**Sync & Backup**
- Google Drive sync — encrypted blob lives in your Drive, syncs on every save
- Encrypted backup export/import (.enc)
- CSV export (unencrypted — personal use only)
- PWA — installs to Android home screen via Chrome

---

## Install on Android

1. Open `https://jml-repo.github.io/roflmaodex/` in Chrome
2. Tap ⋮ → **Add to Home Screen**
3. Set your master password on first launch

---

## Releases

| Version | Notes |
|---------|-------|
| [v2.0](https://github.com/jml-repo/roflmaodex/releases/tag/v2.0) | Three entity types, Drive sync, long-press menus, phone numbers |
| [v1.2](https://github.com/jml-repo/roflmaodex/releases/tag/v1.2) | Initial release — people, interests, connections |

---

## Roadmap

See [CHANGELOG.md](CHANGELOG.md) for the full punchlist.

---

## License

MIT — see [LICENSE](LICENSE)

---

*Single file. No framework. No server. Vanilla JS + sql.js (SQLite/WASM) + Web Crypto API.*
