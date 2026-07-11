# Release Notes

---

## v0.1.9 — 11 July 2026

### Electron port, cross-platform releases, and silent updates

#### Windows Update Experience
- In-app Windows updates now run NSIS silently and reopen Claro after completion; users no longer see the setup wizard during an update.
- Versioned installer names and retained blockmaps enable differential downloads between published versions instead of forcing the full installer download whenever reusable blocks are available.
- Existing app data, activation state, registry cache, dealer information, logs, and queued uploads are preserved.

#### Cross-Platform Release Pipeline
- A single push to `main` builds the Windows NSIS installer and universal macOS package.
- Both platform builds must pass typecheck and the complete automated test suite before publication.
- The combined `latest` release contains the Windows installer, macOS DMG, macOS updater ZIP, blockmaps, `latest.yml`, and `latest-mac.yml`.

#### First Launch and Navigation
- Removed the duplicate startup splash; Claro now has one functional welcome screen.
- Dealer Activation is completed before Dealer Registration can open.
- Activation submission shows a visible verification spinner and disables duplicate submission while the server responds.
- Fixed Dealer Registration fields being blocked by startup overlays on Windows; fields are explicitly editable and focused when the dialog opens.
- The Edit menu now contains only app-specific Patient Information and Dealer Registration actions.
- Added a left-panel update control that displays the installed version, update availability, progress, retry state, and restart action.

#### Reports and Viewer
- Completed the Electron report port with full and single-night PDF generation, legacy section/data ordering, DAT waveform context, device imagery, and Chromium pagination checks.
- Improved chart labels, legends, tooltips, event distributions, pressure distributions, weekly trends, and the single-night timeline.
- Added direct report export controls and restored the legacy patient/device/dealer workflows.

#### Validation
- 693 automated tests pass locally, with opt-in PDF, integration, and performance jobs retained separately.
- Windows and macOS release jobs package independently, then publish together only after both succeed.

---

## v1.26.417.50 — 17 April 2026

### Event Window Analysis rewrite, UI tokenization, new modules

#### Event Window Analysis (waveform event detail charts)
- Rewrote smart-centering to use per-breath peak inspiratory flow with flank contrast. Markers now land on the actual reduced-amplitude region, not on the SUD-rounded minute that was often 30–60 s off the real event.
- SUD stores event time at minute resolution (no seconds field) — the new algorithm searches a ±60 s band around the reported minute and places the marker on the most-suppressed `dur_sec` region bounded by normal breathing on both sides.
- Confidence gate: only HIGH-confidence placements render (≥30 % peak-flow drop vs flanks, AASM hypopnea definition). LOW-confidence events are not drawn rather than showing a marker over ambiguous flow.
- Cap at 5 charts per session. Section now shows "Showing N of M scored events (high-confidence waveform alignment)".
- Empirical validation on a real 29-session file: 18 % of scored events render, median shift correction 26 s, max 58 s. Zero silent-fallback or wrong-region placements.
- Per-block INFO-level log: `event_window: 2026-02-22 rendered 5/32 (slot=7)` for field observability.

#### UI Tokenization
- New `ui_tokens.py` as the single source of truth for colors, typography, and spacing.
- `style.qss` removed; all inline `setStyleSheet` calls replaced with object-named selectors tied to the token module.
- Consistent visual language across app views, dialogs, and chart theming.

#### Chart Fixes
- Weekly Trends "Avg Usage / Night": divide by calendar nights, not session count — two long sessions in a week no longer show as 8 h/night.
- Event Distribution: x-axis spans the full therapy clock window; late-night events in gapped sessions no longer get clipped.
- Minutes at Pressure: cap inter-event `dt` at 5 min so idle gaps don't inflate pressure-bucket time.
- Night Calendar: block width uses clock span instead of active therapy time; gap regions render correctly.

#### New Modules
- `dealer.py` — healthcare-provider profile and branded footer for clinical PDFs.
- `updater.py` — silent background update download + install-on-exit.
- `upload_queue.py` — persistent file-based FIFO queue with stale-lock stealing and orphan sweep.

#### Testing
- 275 passed, 21 skipped (was 254). 26 new tests across breath detection, peak-flow centering (HIGH/LOW confidence paths, strong-drop-at-edge), confidence filter gating, selection cap, and window-edge clipping.

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
