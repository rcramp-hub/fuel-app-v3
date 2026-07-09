# BYD Fuel Calculator — Release Notes

---

## Version 1.14
**Date:** July 2026

### New features
- **Tap-to-map location links on fuel events.** Trip-end and refuel events that were stamped with a GPS location now show a small map link labelled with the fix accuracy (for example, “📍 ±13 m”). Tapping it opens a Google Maps pin drop at those coordinates in a new tab. The link appears in the trip history, on refuel entries, and on the confirmation summary immediately after a location is captured. Events without a stored location show nothing, exactly as before.

### Notes
- The link is built entirely from the coordinates already stored on the device — no map data is fetched until you tap it, and nothing is sent anywhere in the meantime.
- The accuracy shown is the stored fix radius, so a tight head-unit fix reads very small (for example “±0.4 m”) while a phone fix reads larger.

---

## Version 1.13
**Date:** July 2026

### New features
- **Optional GPS location stamping for fuel events.** When enabled, ending a trip or logging a refuel now records a one-shot GPS location (latitude, longitude, accuracy and altitude) alongside the event. The fix is captured while the confirmation summary is on screen, so there is no added delay, and it is stored inside the entry itself. Works on both the BYD head-unit browser (sub-metre fused fix) and a mounted iPhone.
- **Enable/disable in Settings.** A new "GPS location stamping" toggle in the main app settings turns the feature on or off. It is **off by default** and is remembered per vehicle profile. Your device asks for location permission the first time an event is stamped.
- **Per-event Skip button.** Each trip-end and refuel summary shows a Skip button so a single event can be left un-stamped without turning the feature off.

### Notes
- Location capture never blocks or delays saving. If a fix is unavailable, denied, or too weak (worse than 100 m), the event simply saves without a location.
- No coordinates leave the device — the location is stored locally with the event, exactly like the rest of your fuel data.

---

## Version 1.12
**Date:** July 2026

### Improvements
- **Economy chart now re-fits on screen resize / rotation.** The chart re-renders its bars to the new width when the window resizes or the phone rotates, so it stays filled correctly rather than only fitting the width it had when the page first loaded. The handler is debounced and only runs while the chart is visible.

---

## Version 1.11
**Date:** July 2026

### Improvements
- **Economy chart bars now scale to fill the width.** Previously the bars were a fixed 26px, so with only a few trips the chart left large empty space and looked sparse. Bar width is now calculated from the available width so the chart fills the card. With roughly 5+ trips the bars span the full width; with fewer trips they're capped at a sensible maximum and the group is centred, rather than clustered thin on one side.

---

## Version 1.10
**Date:** July 2026

### Improvements
- **Trip reference tags in the history log.** Each trip in the history list now carries the same reference as the economy chart (`Latest`, `T-1`, `T-2` …) as a small tag next to its date, so a bar on the chart can be matched to its row below at a glance. The tag is shown only for the trips that appear on the chart (the most recent 10); the date remains the primary identifier. The latest trip's tag is highlighted in blue to match its row.
- **Full weekday name on timestamps.** Trip and refuel entries in the history log now show the full day name with each timestamp (e.g. "Monday, 6 Jan 2026, 2:32 pm").

---

## Version 1.9
**Date:** July 2026

### Changes
- **Removed the tap-to-edit manual override from the hero number.** The old override on the main litre display was display-only, didn't persist, and was ignored by the HEV page — its real jobs are now covered by Fill to Full mode and HEV refuel logging.
- **New persistent "Manual fuel override" in Settings.** Enter the exact litres in your tank (e.g. from the pump total or a dip test) and tap Apply. Unlike the old one, this override:
  - **persists** across reloads and is stored per vehicle profile;
  - **runs through the whole app** — main display, gauge, distance remaining, and the HEV page (refuel detection, trip economy, and the combined fuel readout all honour it);
  - is cleared by tapping **Clear override** or by moving a fuel slider on the main screen (which resumes calibrated mode);
  - **supersedes Fill to Full mode** if that was active.
- A small "✎ manual override active — set in settings" badge shows under the hero number while an override is in effect. On the HEV page the fuel pill shows the override litres with both % and km derived (each marked `~`).

---

## Version 1.8
**Date:** July 2026

### New Features
- **Combined fuel readout on the HEV page.** The "Current fuel level" pill now shows the litre figure alongside its equivalent **% and dashboard km range** (e.g. `58.3 L` with `300 km · ~62%` beneath it). This lets the driver cross-reference the app against the instrument cluster, which displays km rather than litres.
  - The **unit the user actually entered in the main app** (km or %) is echoed exactly, so it matches what they typed / what the cluster shows.
  - The **other unit is derived** from the litre figure using the same calibration data (including any user overrides) and is prefixed with `~` to indicate it's an estimate. Derived km is rounded to the nearest 5 to reflect the fuel sender's inherent uncertainty.
  - In Fill-to-Full mode the line reads `100% · full tank`.

---

## Version 1.7
**Date:** July 2026

### Changes
- **Auto-detected refuel no longer silently ends the current trip.** When you submit an HEV Odometer reading and the app detects an unaccounted fuel increase (a refuel), the refuel prompt now asks what to do with the odometer reading rather than assuming the trip is over:
  - **End trip & log refuel** — logs the refuel and closes out the current trip at the submitted odometer reading (previous behaviour).
  - **Log refuel only — keep trip open** — logs the refuel like the standalone refuel button and leaves the current trip running. The odometer value stays in the input so the trip can be ended later.
- The standalone "Log Refuel" button is unchanged — it still logs a refuel without touching the current trip.

> Note: release notes for versions 1.3–1.6 were not captured in this file; the app version prior to this release was 1.6.

---

## Version 1.2
**Date:** June 2026

### New Features
- **Fuel burn rate slider** — set your vehicle's average fuel consumption in L/100km (range 5–30, default 12.0). Remembered between sessions.
- **Distance remaining stat box** — calculates and displays estimated distance remaining based on fuel in tank and burn rate. Updates live as either the fuel or burn rate slider is moved.
- **Manual litre override** — tap the large green litre number to type in a known fuel amount directly. Gauge, stats and distance all update instantly. An amber "✎ manual override" badge shows when active. Moving either slider resumes normal calibration mode automatically.

### Improvements
- Input type selector (Dashboard km / BYD App %) moved into the input card, sitting directly above the sliders for a cleaner layout
- Hero and stats now appear first so results are immediately visible on open
- Burn rate slider correctly updates distance remaining independently of the fuel sliders

### Bug Fixes
- Fixed step change in fuel remaining between 12% and 13% — caused by duplicate readings in calibration data (20L and 30L both showing 12%). Duplicates are now averaged, eliminating the jump
- Fixed tank capacity display being hardcoded to 80L — now dynamically extrapolated from calibration data
- Fixed colour thresholds — gauge and litre number colour now based on actual litres remaining (not percentage): red ≤10L, red→orange blend 10–20L, orange→green blend 20–30L, green 30L+
- Fixed burn rate slider not updating distance remaining when moved

---

## Version 1.1
**Date:** June 2026

### New Features
- **Settings panel** — expandable section at the bottom of the app with editable calibration tables
- **Editable calibration tables** — fixed rows at 10, 20, 30, 40, 50, 60, 70, 80L. User enters what their dashboard km range and BYD App % shows at each fuel level
- Default values shown greyed out alongside user values for reference
- **Save & apply** — rebuilds the interpolation algorithm instantly from user-entered data
- **Reset to defaults** — restores original BYD calibration data with one tap
- All custom calibration data persists between sessions via localStorage
- **Tank capacity seen by fuel sender** now dynamically derived via extrapolation rather than hardcoded
- **Copyright footer** — © 2026 Ryan Cramp — All Rights Reserved, displayed at bottom of app and in source code comment

### Improvements
- Interpolation engine upgraded to extrapolate beyond calibration table bounds (previously clamped at 80L)
- Duplicate readings in calibration data now averaged to prevent step changes
- Stat box values now displayed in accent green to match the hero number

---

## Version 1.0
**Date:** June 2026

### Overview
A Progressive Web App (PWA) designed for BYD vehicle owners to accurately calculate the actual litres of fuel remaining in their tank, based on real-world calibration data captured from a BYD vehicle.

The app accounts for the non-linear behaviour of the BYD fuel sender unit, which causes the dashboard and BYD app readings to be inaccurate representations of true fuel volume.

### Features
- **Two input modes** — Dashboard km range (0–700km) and BYD App % (0–100%)
- **Calibrated fuel calculation** using real-world BYD measurement data — not a simple percentage formula
- **Piecewise linear interpolation** between calibration points for accurate mid-range estimates
- **Linked sliders** — switching between input modes automatically converts and syncs the equivalent value across both tabs
- **Visual fuel gauge** with colour coding
- **Persistent memory** — remembers last input tab and value when reopened
- **PWA installable** — add to iPhone/Android home screen, works offline
- **Mobile optimised** — designed for Safari on iPhone

### Calibration Data
Built from real measurements taken from a BYD vehicle. The fuel sender unit has a usable range of approximately 5L (empty) to 80L (full).

| Fuel in Tank (L) | Dashboard (km) | BYD App (%) |
|---|---|---|
| ~5 | 0 | 0 |
| 25 | 106 | 12 |
| 45 | 276 | 38 |
| 60 | 475 | 68 |
| 70 | 581 | 83 |
| 80 | 699 | 99 |

**Known limitation:** The fuel sender cannot distinguish between paired readings at the lower end. The app averages these to the midpoint, resulting in ±5L uncertainty below 50L. This is a hardware limitation of the fuel sender, not the app.

---

## Files
| File | Purpose |
|---|---|
| `index.html` | Main app — all UI, logic, and calibration data |
| `manifest.json` | PWA manifest — enables home screen installation |
| `sw.js` | Service worker — enables offline use |
| `icon.svg` | App icon |
| `RELEASE_NOTES.md` | This file |

---

## Hosting
- Hosted via **GitHub Pages** (free)
- Custom domain setup planned for a future release

---

## Planned Features / Future Versions
- Custom domain / proper web address
- Buy Me a Coffee tip jar button
- Cost-to-fill estimator (enter price per litre)
- Additional calibration data points as more measurements are captured
- Potential expansion to other BYD models

---

## Known Issues / Limitations
- OBD2 Bluetooth integration explored but removed — Safari on iPhone does not support Web Bluetooth API
- ±5L uncertainty at lower fuel levels due to fuel sender hardware limitations
- Web Bluetooth (OBD2) would require Chrome on Android or desktop

---

*© 2026 Ryan Cramp — All Rights Reserved*
