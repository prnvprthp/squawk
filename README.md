# Squawk

**A tiny menu‑bar / system‑tray app + screen saver that shows the real aircraft flying over you — on a retro radar.** Native builds for **macOS** and **Windows**, and the screen saver for **Fire TV**.

Live ADS‑B data, a sweeping radar, callsigns, altitudes, aircraft types and routes for whatever is in the sky above your actual location. No account, no API keys, no setup.

---

## Download — v1.3

| Platform | Download | Requires |
|---|---|---|
| **macOS** | **[Squawk.dmg](https://github.com/prnvprthp/squawk/releases/latest/download/Squawk.dmg)** | macOS 13+ · Universal (Apple Silicon & Intel) |
| **Windows** | **[Squawk-Windows.zip](https://github.com/prnvprthp/squawk/releases/latest/download/Squawk-Windows.zip)** | Windows 10/11 · 64‑bit · self‑contained |
| **Fire TV** | **[Squawk-FireTV.apk](https://github.com/prnvprthp/squawk/releases/latest/download/Squawk-FireTV.apk)** | Fire TV · tested on Fire OS 8 · screen saver only |

All free, and none of them needs anything installed first. See the **[changelog](CHANGELOG.md)** for what's new.

---

## Install — macOS

1. Open the downloaded **`Squawk.dmg`**.
2. Drag **`Squawk.app`** onto the **Applications** shortcut.
3. Double‑click **`Squawk.saver`** to install the screen saver, then choose **Squawk** in **System Settings ▸ Screen Saver**.
4. Launch **Squawk** from Spotlight / Applications and **allow location access** so it knows what’s overhead — or skip that and pin a location yourself in **Settings ▸ LOCATION**.

### First launch: *“Apple could not verify…”* / *“can’t be opened”*

Squawk is free and **not signed with a paid Apple Developer certificate**, so macOS blocks it the first time. It’s safe — here’s the standard way to open an un‑notarized app:

1. Double‑click the app (or the screen saver). When the warning appears, click **Done**.
2. Open **System Settings ▸ Privacy & Security** and scroll to the **Security** section.
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

## Install — Windows

1. Download and **unzip** it.
2. **Tray app** — put **`Squawk.exe`** somewhere permanent (it runs from anywhere) and open it. If Windows shows *“Windows protected your PC”*, click **More info → Run anyway** (it’s unsigned, not malware). A radar icon appears in the system tray (bottom‑right, by the clock — you may need the **^** to show hidden icons). **Left‑click** it to open the radar; drag any edge to resize it. **Right‑click** for the menu.

### Screen saver

Copy **`SquawkSaver.scr`** into **`C:\Windows\System32`** — you’ll be asked for administrator permission. Then open **Settings ▸ Personalization ▸ Lock screen ▸ Screen saver** and pick **SquawkSaver** from the dropdown.

To exit it: move the mouse, click, or press any key.

> **Why System32?** Windows only lists screen savers it finds in `C:\Windows\System32`, so that’s the one place it will reliably show up in the dropdown and stay selected. Right‑clicking the `.scr` ▸ **Install** does work from any folder — it points Windows at that exact file — but the saver then won’t appear in the dropdown, and it breaks the moment you move or delete the folder you ran it from. Copying it in avoids both problems.

---

## Install — Fire TV

Fire TV apps outside the Amazon Appstore are installed with the free **Downloader** app.

1. On the Fire TV, search for and install **Downloader** (by AFTVnews) from the Appstore.
2. Open **Settings ▸ My Fire TV ▸ Developer options ▸ Install unknown apps** and turn it on for **Downloader**.
   No *Developer options*? Open **Settings ▸ My Fire TV ▸ About** and click your device's name **7 times**, then go back.
3. Open Downloader, type this address and press **Go**:
   `github.com/prnvprthp/squawk/releases/latest/download/Squawk-FireTV.apk`
4. Choose **Install**, then **Done**. You can delete the downloaded file when Downloader offers.
5. Open **Squawk** from *Your Apps* to choose a theme, range and location (an airport code like `BOS`, or coordinates), and to **Preview** it.

### Making it the screen saver

Fire OS has no menu for choosing a third‑party screen saver, so this takes one command from a computer (or from an ADB app on an Android phone) on the **same Wi‑Fi**:

1. On the Fire TV: **Developer options ▸ ADB debugging ▸ On**. The TV's IP address is under **Settings ▸ My Fire TV ▸ About ▸ Network**.
2. Install Google's [Android platform tools](https://developer.android.com/tools/releases/platform-tools) on the computer, then run:
   ```bash
   adb connect <TV-IP-address>
   adb shell settings put secure screensaver_components com.squawk.tv/.SquawkDream
   ```
   Accept the *Allow USB debugging?* prompt on the TV. There's no need to tick *Always allow*.
3. **Turn ADB debugging back off**, and turn *Install unknown apps* off for Downloader. Squawk keeps working with both off.

The screen saver starts after the TV's usual idle time (**Settings ▸ Display & Sounds ▸ Screensaver**). A Fire OS update can switch it back to Amazon's own; if that happens, repeat these three steps. To return to Amazon's saver yourself, run
`adb shell settings put secure screensaver_components com.amazon.ftv.screensaver/.app.services.ScreensaverService`.

**What it can access:** the only permission it has is Internet. It sends nothing about you or the TV. It fetches public flight data over HTTPS (a rough location goes to the ADS‑B services, and your IP to an IP‑location service unless you pin a location), and only while the screen saver or Preview is on screen.

---

## Settings

**macOS** — click the gear in the radar popover. **Windows** — right‑click the tray icon ▸ **Settings…**

- **Range** — how far out the radar reaches: 10 / 20 / 35 / 50 km.
- **Location** — track this machine, or **pin the radar anywhere**. Type a city or an airport code (`BOS`, `EGLL`, `HND`) and hit **FIND**, or enter a latitude and longitude yourself. Handy for watching a hometown airport, or if you'd rather not grant location access at all.
- **Theme** — three looks: **Green**, **Red**, or **White**.
- **Screen saver** — its **own** theme, range and location, set from the app. Applies the next time it starts.

The screen saver can also be themed on its own: **macOS** — *System Settings ▸ Screen Saver ▸ “Screen Saver Options…”*; **Windows** — everything lives in the app's Settings dialog.

---

## What you get

- **Menu‑bar / tray radar** — a live sweep of nearby traffic: callsign, altitude, speed, aircraft type, tail number, and departure → arrival.
- **Screen saver** — the same radar, full‑screen, whenever your machine is idle.
- **A real‑radar feel** — contacts persist between sweeps and only move when the beam reaches them, each leaving a fading trail.
- **Emergencies** — squawk **7500 / 7600 / 7700** pulse red with a warning banner. **Military** aircraft show amber + **MIL**.
- **“Overhead now”** — the plane most directly above you, called out at a glance.
- **Click a plane** → its **photo** and **operator**.
- **Overhead alerts** — an optional notification when a plane is about to pass over you.
- **Point it anywhere** — pin the radar to any city, airport code, or coordinate, on either platform.
- **Start at login** — macOS: *Settings ▸ LAUNCH AT LOGIN*. Windows: tray ▸ *Start with Windows*.

Full history in the **[changelog](CHANGELOG.md)**.

---

## Privacy

- Squawk uses your **approximate location** to center the radar and to ask the flight service what’s nearby — nothing is stored, tracked, or shared with anyone.
- The desktop apps get your location from the OS; the screen saver (which can’t request location permission) estimates your **city from your IP address**. Pin a location in Settings and neither is used.
- Searching for a place by name sends just that search text to Apple's geocoder (macOS) or **[Nominatim](https://nominatim.openstreetmap.org)** (Windows). Airport codes are resolved offline, on your machine.
- All flight data is free and public — **[adsb.fi](https://adsb.fi)** / **[adsb.lol](https://adsb.lol)** for positions, **[adsbdb](https://www.adsbdb.com)** for aircraft, photos + routes. No account or key required.

---

<sub>Made by [@prnvprthp](https://github.com/prnvprthp) · This repo distributes the apps only — flight data © the adsb.fi / adsb.lol community.</sub>
