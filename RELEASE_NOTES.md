# BYD Fuel Calculator — Release Notes

---

## Version 1.0
**Date:** June 2026

### Overview
A Progressive Web App (PWA) designed for BYD vehicle owners to accurately calculate the actual litres of fuel remaining in their tank, based on real-world calibration data captured from a BYD vehicle.

The app accounts for the non-linear behaviour of the BYD fuel sender unit, which causes the dashboard and BYD app readings to be inaccurate representations of true fuel volume.

---

### Features
- **Two input modes:**
  - Dashboard km range (0–700 km)
  - BYD App % (0–100%)
- **Calibrated fuel calculation** using real-world BYD measurement data — not a simple percentage formula
- **Piecewise linear interpolation** between calibration points for accurate mid-range estimates
- **Linked sliders** — switching between input modes automatically converts and syncs the equivalent value across both tabs
- **Visual fuel gauge** with colour coding:
  - Green — healthy fuel level
  - Orange — getting low (≤30% of tank)
  - Red — very low (≤12% of tank), with urgent warning message
- **Key stats displayed:**
  - Litres remaining
  - Litres to fill to fuel sender capacity
  - Tank capacity seen by fuel sender (80L)
- **Persistent memory** — app remembers your last input tab and value when reopened on iPhone
- **PWA installable** — can be added to iPhone/Android home screen and works offline
- **Mobile optimised** — designed for Safari on iPhone, respects safe area insets

---

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

**Known limitation:** The fuel sender cannot distinguish between paired readings at the lower end (e.g. both 20L and 30L read as 12% on the BYD app). The app correctly estimates the midpoint (25L) in these cases, resulting in a ±5L uncertainty below 50L. This is a hardware limitation of the fuel sender, not the app.

---

### Files
| File | Purpose |
|---|---|
| `index.html` | Main app — all UI, logic, and calibration data |
| `manifest.json` | PWA manifest — enables home screen installation |
| `sw.js` | Service worker — enables offline use |
| `icon.svg` | App icon |

---

### Hosting
- Hosted via **GitHub Pages** (free)
- Custom domain setup planned for future release

---

### Planned Features / Future Versions
- Custom domain / proper web address
- Buy Me a Coffee tip jar button
- Cost-to-fill estimator (enter price per litre)
- Additional calibration data points as more measurements are captured
- Potential expansion to other BYD models

---

### Known Issues
- OBD2 Bluetooth integration was explored but removed in v1.0 due to Safari on iPhone not supporting Web Bluetooth API
- ±5L uncertainty at lower fuel levels due to fuel sender hardware limitations

