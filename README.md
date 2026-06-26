# Squawk 🛩️

**A tiny macOS menu‑bar app + screen saver that shows the real aircraft flying over you — on a retro green radar.**

Live ADS‑B data, a sweeping radar, callsigns, altitudes, aircraft types and routes for whatever is in the sky above your actual location. No account, no API keys, no setup.

---

## ⬇️ Download

### **[Download Squawk v1.0.0 (.dmg)](https://github.com/prnvprthp/squawk/releases/latest/download/Squawk.dmg)**

macOS 13 (Ventura) or later · ~1 MB · free

---

## Install

1. Open the downloaded **`Squawk.dmg`**.
2. Drag **`Squawk.app`** onto the **Applications** shortcut.
3. Double‑click **`Squawk.saver`** to install the screen saver, then choose **Squawk** in **System Settings ▸ Screen Saver**.
4. Launch **Squawk** from Spotlight / Applications and **allow location access** so it knows what’s overhead.

### ⚠️ If macOS says *“Squawk can’t be opened…”*

Squawk is free and **not signed with a paid Apple Developer certificate**, so macOS is cautious the first time. It’s safe — just tell macOS to open it:

- **The app:** right‑click **`Squawk.app` ▸ Open ▸ Open** (only needed once).
- **The screen saver:** after double‑clicking it, open **System Settings ▸ Privacy & Security** and click **Open Anyway**.

Or clear the quarantine flag once in Terminal:

```bash
xattr -dr com.apple.quarantine /Applications/Squawk.app
xattr -dr com.apple.quarantine ~/Library/Screen\ Savers/Squawk.saver
```

---

## What you get

- **Menu‑bar radar** — click the icon for a live sweep of nearby traffic: callsign, altitude, speed, aircraft model, and departure → arrival.
- **Screen saver** — the same radar, full‑screen, scanning **50 km** around you whenever your Mac is idle.
- **Real planes, your sky** — positions come from the public ADS‑B network, centered on your location.

---

## Privacy

- Squawk uses your **approximate location** to center the radar and to ask the flight service what’s nearby — nothing is stored, tracked, or shared with anyone.
- The menu‑bar app gets your location from macOS; the screen saver (which can’t request location permission) estimates your **city from your IP address**.
- All flight data is free and public — **[adsb.fi](https://adsb.fi)** / **[adsb.lol](https://adsb.lol)** for positions, **[adsbdb](https://www.adsbdb.com)** for aircraft + routes. No account or key required.

---

<sub>Made by [@prnvprthp](https://github.com/prnvprthp) · This repo distributes the app only — flight data © the adsb.fi / adsb.lol community.</sub>
