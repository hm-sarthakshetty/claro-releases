# Release Notes

---

## v1.26.406 — 6 April 2026

### Activation, Auto-Update, Privacy, Testing

#### Activation Gate
- One-time activation code required on first launch
- Validated online against server — code stored locally after success
- Re-validates stored code silently on every subsequent launch
- Revoked codes detected on next launch — prompts for new code
- Offline grace: previously activated apps can still launch without internet

#### Auto-Updater
- Checks GitHub releases for newer version on every launch
- Downloads installer silently in background while user works
- Status bar notification: "Update vX.X ready — will install when you close the app"
- On app close: spawns silent installer with 3-second delay, installs in-place
- No interruption, no popups, no forced restart

#### Privacy & Compliance
- First-launch privacy notice dialog — covers usage analytics, healthcare provider info, device data
- "I Agree" / "Exit" consent gate before any app functionality
- "Healthcare Provider" replaces "Dealer" throughout the UI
- Healthcare Provider dialog: per-field "Show on report" visibility checkboxes

#### Dev Mode
- Automatically active when running from source (version contains "dev")
- Skips: privacy notice, activation, serial registry check
- Allows non-Home Medix devices with warning (for testing with other manufacturers' data)
- No uploads to cloud endpoints — fully offline development

#### Daily Report Email
- Automated email summary sent at 6 AM IST via Google Apps Script trigger
- Covers: report counts (clinical vs single-night), device model breakdown, serial validation against registry, unregistered serial alerts, new serials first seen, reports by city, top healthcare providers by volume, app versions in use
- Unregistered serials highlighted in red alert box
- No-activity days send short notification

#### Testing
- 272 tests total, 0 skipped, 0 failed
- 27 new edge case tests: AASM 10s filter, zero-duration sessions, midnight crossing, pressure/SpO2 bounds, DAT validation, HTML escaping, Unicode, global stats edge cases
- 13 auto-updater tests: version parsing, comparison, mock update, pending update no-ops
- 48 adversarial device gate tests: valid/invalid serials, SQL injection, XSS, path traversal, null bytes, Unicode, registry bypass attempts
- 5 activation tests: network error, success, invalid code handling
- Fixed test paths to match actual workspace layout

---

## v1.26.404c — 4 April 2026

### UI Polish: Unified Pressure Gradient, Patient Profile, Branding

#### Pressure Coloring
- Single source of truth: fixed 27-color gradient from 4–30 cmH₂O
- One gradient used everywhere — legend, calendar bars, all therapy modes
- Legend dynamically shows relevant pressure range based on session data

#### Patient Profile
- Full demographics in sidebar: name, ID, sex, DOB with age, height, weight, phone
- Clean table layout, updates live when edited

#### Branding
- App header: "Claro" / "Clinical Therapy Reports"

---

## v1.26.404b — 4 April 2026

### Polish: Bilevel Coloring, Print Readability

- Bilevel sessions: horizontally split time bars (top = IPAP, bottom = EPAP)
- All chart font sizes raised to minimum 6pt for print
- Pressure trend chart reference lines are mode-dependent
- Weekly trends (was monthly) for denser data
- Animated loading screen with Home Medix logo

---

## v1.26.404 — 4 April 2026

### Major: Waveform Reports & AASM Compliance

- Unified 6-panel single-night overview with gap compression
- Event Window Analysis with leak-corrected tidal amplitude
- AASM-compliant scoring (≥10s for all respiratory events)
- Mode-aware pressure rendering
- API key validation, HTML escaping, atomic registry sync
- File validation in DAT and SUD parsers

---

## v1.26.403 — 3 April 2026

### Initial Release

- Clinical report cover page, date range filtering, dealer information
- Improved chart quality and readability
- AHI severity coloring per AASM standards

---
