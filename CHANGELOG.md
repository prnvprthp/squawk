# Changelog

All notable changes to **Squawk**. Newest first. Downloads live on the [releases page](https://github.com/prnvprthp/squawk/releases).

---

## v1.2 — *29 Jul 2026*

**Point the radar anywhere, and set up the screen saver from the app.** [Download](https://github.com/prnvprthp/squawk/releases/tag/v1.2.0) · macOS `Squawk.dmg` · Windows `Squawk-Windows.zip`

### Added
- **Location override.** The radar no longer has to be centred on the machine it's running on. Pick *CUSTOM* in Settings and type a city, an **airport code** (`BOS`, `EGLL`, `HND`), or a latitude and longitude. Airport codes resolve offline; place names go to Apple's geocoder on macOS and [Nominatim](https://nominatim.openstreetmap.org) on Windows. Useful for keeping an eye on a hometown airport — or for skipping the location permission entirely.
- **The screen saver is configured from the app.** Its **theme, range and location** now live in the app's Settings, under *SCREENSAVER*. Changes reach a saver that's already running, not just the next start.
- **A Settings dialog on Windows** (right-click the tray icon ▸ *Settings…*) — range, location, theme, and the screen saver's own three, matching the macOS panel. Windows previously had no settings window at all.

### Changed
- **Bigger click targets.** Buttons in the macOS Settings panel and the range strip respond anywhere in the button, not only on the label text.
- **Radar range is remembered** between launches on macOS; it used to reset to 20 km every time.
- *(Windows)* The **Overhead alerts** toggle is remembered too — it used to reset on every launch.
- *(Windows)* The screen saver's *Settings* button now points at the app's new SCREENSAVER section.
- Moving the radar's centre clears the contacts painted at the old one, instead of briefly plotting them against the new position.

### Fixed
- *(macOS)* Squawk stored credentials for a flight service it **stopped using in v1.0** — a username and password, in plain text, in its preferences file. The feature is long gone; this release deletes the leftover code and **erases those saved credentials** from your machine on first launch. If you ever entered an OpenSky password here and reuse it anywhere, change it.

### Known issues
- Still **not code-signed or notarized**, so both platforms warn once on first launch — see the README. The macOS *Launch at login* toggle still needs a notarized build to stick.
- The Windows Settings dialog is **new and unproven on-screen** — its layout has only been compile-checked. Please report anything that looks wrong.
- **Updating the Windows screen saver:** copy the new `SquawkSaver.scr` over `C:\Windows\System32\SquawkSaver.scr`, then re-pick **SquawkSaver** in *Settings ▸ Personalization ▸ Lock screen ▸ Screen saver*.

---

## v1.1 — *16 Jul 2026*

**macOS + Windows, together, with themes.** [Download](https://github.com/prnvprthp/squawk/releases/tag/v1.1.0) · macOS `Squawk.dmg` · Windows `Squawk-Windows.zip`

### Added
- **Themes — Green, Red, White.** Applies to the app *and* the screen saver.
  macOS: *Settings ▸ THEME* (app) and *Screen Saver Options…* (saver — the saver keeps its own setting).
  Windows: right-click the tray icon ▸ *Theme* (one setting covers the tray app and the saver).
- **Emergency squawks.** 7500 / 7600 / 7700 pulse red with a warning banner in the list.
- **Military aircraft** show amber with a **MIL** badge.
- **More per-plane detail** — tail number, aircraft category (HELICOPTER / HEAVY / DRONE…), and squawk code.
- **OVERHEAD readout** — the one plane most directly above you, called out above the radar.
- **Click a plane → photo + operator** (and country of registration), fetched on demand.
- **Overhead alerts** — an optional notification when a plane will pass within 3 km of you in the next 4 minutes. macOS: notification; Windows: tray balloon. Toggle in Settings / the tray menu.
- **Launch at login** toggle *(macOS only; needs a notarized build to stick — see Known issues)*.
- **Windows is now a full release**, no longer a preview, and reached feature parity with macOS.

### Changed
- **The radar behaves like a real radar.** Contacts persist between sweeps instead of fading to black, and a blip only moves to its new position when the sweep beam actually reaches it — no more blinking or teleporting. Each contact leaves a short fading trail.
- **Polling is 4× more frequent** — every 10s instead of 30s, so a plane has actually moved by the time the beam comes back around to it.
- **Smoother sweep.** Reworked how the radar draws and how updates reach it, fixing the periodic frame drops.

### Fixed
- **The radar could go empty for no reason.** When the primary flight feed returned a valid-but-empty response, Squawk accepted it instead of falling back to the backup feed. Both feeds are now tried properly.
- Selecting a plane no longer makes its photo and operator flicker on each refresh.
- *(Windows)* **The screen saver could take over the screen and refuse to close** — no key, click or mouse movement would dismiss it, leaving locking the machine as the only way out. Every exit path depended on the app's UI thread being responsive, so a single stall took all of them out at once. Dismissal is now handled by a watchdog that runs independently of the app's UI, polls the mouse and keyboard directly from the OS, and force-quits the saver if it doesn't close gracefully. The saver also now takes keyboard focus properly on start.
- *(Windows)* The tray radar popover couldn't be resized; it now drags from any edge and remembers its size.
- *(Windows)* The screen saver's *Settings* button claimed there were no settings; it now points at the tray's Theme menu.
- *(Windows)* Install instructions now say to copy `SquawkSaver.scr` into `C:\Windows\System32` — Windows only lists screen savers found there, so the previous right-click ▸ Install advice left it missing from the Screen saver dropdown.

### Known issues
- **Neither build is code-signed or notarized**, so macOS and Windows each warn once on first launch. The README has the click-through for both. This also stops the macOS *Launch at login* toggle from sticking — add Squawk to *System Settings ▸ General ▸ Login Items* by hand for now.
- The Windows build is **new and lightly tested** — please report anything that looks off.
- **Updating the Windows screen saver:** re-downloading the zip does **not** update an installed saver. Copy the new `SquawkSaver.scr` over `C:\Windows\System32\SquawkSaver.scr`, then re-pick **SquawkSaver** in *Settings ▸ Personalization ▸ Lock screen ▸ Screen saver* — if it was ever installed from another folder, Windows still points at that old file until you re-select it.

---

## Squawk for Windows (preview) — *15 Jul 2026*

First Windows build, published as a pre-release for testing: system-tray radar app plus screen saver, rebuilt natively in C# / .NET 8, self-contained (no .NET install needed).

> **Superseded by v1.1** — that release includes the Windows build proper. Don't download this one.

---

## v1.0.0 — *26 Jun 2026*

First public release. macOS menu-bar app **and** screen saver, universal (Apple Silicon + Intel).

- Live radar of the aircraft overhead: callsign, altitude, speed, aircraft type, and route.
- Screen saver runs the same radar full-screen, and is **fully self-sufficient** — it finds your location from your IP and pulls flights on its own, so you never have to open the app first.
- Keyless and accountless throughout: positions from **adsb.fi** / **adsb.lol**, aircraft and routes from **adsbdb**.
