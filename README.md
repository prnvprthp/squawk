# Squawk

**A tiny menu‑bar / system‑tray app + screen saver that shows the real aircraft flying over you — on a retro green radar.** Native builds for **macOS** and **Windows**.

Live ADS‑B data, a sweeping radar, callsigns, altitudes, aircraft types and routes for whatever is in the sky above your actual location. No account, no API keys, no setup.

---

## Download — macOS

### **[Download Squawk v1.0.0 (.dmg)](https://github.com/prnvprthp/squawk/releases/latest/download/Squawk.dmg)**

macOS 13 (Ventura) or later · Universal — Apple Silicon &amp; Intel · free

---

## Install — macOS

1. Open the downloaded **`Squawk.dmg`**.
2. Drag **`Squawk.app`** onto the **Applications** shortcut.
3. Double‑click **`Squawk.saver`** to install the screen saver, then choose **Squawk** in **System Settings ▸ Screen Saver**.
4. Launch **Squawk** from Spotlight / Applications and **allow location access** so it knows what’s overhead.

### First launch: *“Apple could not verify…”* / *“can’t be opened”*

Squawk is free and **not signed with a paid Apple Developer certificate**, so macOS blocks it the first time. It’s safe — here’s the standard way to open an un‑notarized app:

1. Double‑click the app (or the screen saver). When the warning appears, click **Done**.
2. Open **System Settings ▸ Privacy & Security** and scroll down to the **Security** section.
3. You’ll see *“Squawk” was blocked…* — click **Open Anyway** and authenticate.
4. Confirm **Open Anyway** once more. It opens, and won’t ask again.

Do this once for **`Squawk.app`** and once for **`Squawk.saver`**.

> On **macOS Sequoia** the old *right‑click ▸ Open* shortcut no longer works — use the steps above. (On Ventura/Sonoma, right‑click ▸ Open ▸ Open also works.)

Prefer Terminal? Clear the quarantine flag instead:

```bash
sudo xattr -rd com.apple.quarantine /Applications/Squawk.app
sudo xattr -rd com.apple.quarantine ~/Library/Screen\ Savers/Squawk.saver
```

---

## Windows (preview)

A Windows build — system‑tray app **and** screen saver — is in early testing.

### **[Download Squawk for Windows (.zip)](https://github.com/prnvprthp/squawk/releases/download/windows-preview/Squawk-Windows-preview.zip)**

Windows 10/11 · 64‑bit · self‑contained (no .NET install needed)

1. Download and **unzip** it.
2. **Tray app** — run **`Squawk.exe`**. If Windows shows *“Windows protected your PC”*, click **More info → Run anyway** (it’s unsigned, not malware). A green radar icon appears in the system tray (bottom‑right, by the clock); left‑click it to open the radar.
3. **Screen saver** — right‑click **`SquawkSaver.scr` → Install**, then Preview / Save.

No account or keys — it finds your city and shows real nearby planes. ⚠️ This is the first Windows build and is still being tested; feedback welcome.

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
