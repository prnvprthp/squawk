# Changelog

All notable changes to **Squawk**. Newest first. Downloads live on the [releases page](https://github.com/prnvprthp/squawk/releases).

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
- *(Windows)* The screen saver wouldn't exit on mouse or key input.
- *(Windows)* The tray radar popover couldn't be resized; it now drags from any edge and remembers its size.
- *(Windows)* The screen saver's *Settings* button claimed there were no settings; it now points at the tray's Theme menu.

### Known issues
- **Neither build is code-signed or notarized**, so macOS and Windows each warn once on first launch. The README has the click-through for both. This also stops the macOS *Launch at login* toggle from sticking — add Squawk to *System Settings ▸ General ▸ Login Items* by hand for now.
- The Windows build is **new and lightly tested** — please report anything that looks off.

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
