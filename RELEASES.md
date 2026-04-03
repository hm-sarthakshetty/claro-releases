# Release Notes

---

## v1.26.404 — 4 April 2026

### Major: Waveform Reports & AASM Compliance

#### Waveform Analysis
- **Unified 6-panel single-night overview** — Event Lanes, Pressure, Airflow, Leak, Snore, Rolling AHI stacked on a single page with gap compression
- **Works with and without SD card** — DAT files give high-resolution traces; SUD-only shows discrete data points. Same 6 panels either way
- **Event Window Analysis** — annotated 3-minute windows around scored apnea/hypopnea events showing:
  - Leak-corrected tidal amplitude (peak-minus-trough per breath, cancels mask leak)
  - Rolling mean tidal amplitude for sustained reduction detection
  - Pre-event baseline and 70% threshold lines
  - Automatic boundary detection from waveform crossings
  - Events without visible waveform reduction are filtered out
  - Clinical explanatory text per event type
- **Mode-aware pressure rendering** — bilevel shows EPAP-IPAP envelope, APAP shows single auto-titrating line, CPAP shows flat trace. Reference lines match mode (EPAP/IPAP, Min/Max, or Rx)

#### AASM Compliance
- All respiratory events (OA, CA, HY) now require **≥10 seconds** duration per AASM standards
- Applied consistently across parser, interactive charts, and PDF reports
- Replaces previous non-standard thresholds (12s OA, no minimum HY)

#### Patient Information
- New Patient Information dialog replaces simple name prompt
- Full demographics: name, patient ID, sex, date of birth, height, weight, telephone
- All fields written to device memory card (SUD ST_PATIENTS struct)

#### Dealer Branding
- Per-field visibility checkboxes on Dealer Information dialog
- Company and email shown by default; name and phone opt-in
- Only checked fields appear on generated reports

#### Report Improvements
- Report title changed to "PAP Sleep Therapy Report" (universal across all modes)
- Therapy mode on cover page now uses most recent device settings
- Pressure trend chart reference lines are mode-dependent
- Removed redundant Device Information section
- Print-optimised gridlines on all chart panels
- Proper axis labels on all panels (cmH₂O, L/min, ev/hr)

#### Security
- API key validation on cloud endpoints
- HTML-escaped user input in PDF templates
- Dealer info passed via environment variable instead of command-line arguments
- Atomic write for serial registry sync
- File validation in DAT and SUD parsers

#### Bug Fixes
- Fixed crash on no-DAT sessions (matplotlib canvas overflow from coordinate transform bug)
- Fixed stacked panels pushed to page 3 (figure height overflow)
- Fixed color mismatch between interactive charts and PDF reports

---

## v1.26.403 — 3 April 2026

### What's New
- **Redesigned clinical report cover page** — clean, professional layout with patient info, equipment details, and dealer information
- **Date range filtering** — generate clinical reports for specific date ranges (7/14/30/60/90 days or custom)
- **Dealer information system** — dealer name, company, phone, and email printed on all reports
- **Improved chart quality** — higher resolution charts with better readability across all reports

### Improvements
- Report titles now use full clinical terminology (e.g. "Bi-Level Positive Airway Pressure Therapy Report")
- AHI severity coloring updated to AASM clinical standards (Normal < 5, Mild 5–15, Moderate 15–30, Severe ≥ 30)
- Night calendar pressure segments refined for smoother gradient display
- Pressure color scale adapts to device type (CPAP vs BiPAP range)
- Respiratory mechanics section prioritized in statistical report
- Clearer error message when trying to save a report that's already open

### Bug Fixes
- Fixed report version number not appearing in generated PDFs
- Fixed Auto On/Auto Off showing in single night prescribed settings
- Resolved file overwrite errors by adding timestamps to report filenames

---
