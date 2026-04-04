# Release Notes

---

## v1.26.404b — 4 April 2026

### Polish: Bilevel Coloring, Weekly Trends, Print Readability

#### Night Calendar
- **Bilevel pressure visualization** — time bars are now horizontally split: top half coloured by IPAP (warm amber/orange), bottom half by EPAP (cool blue). Gives clinicians an at-a-glance view of both pressure levels
- Two-tone pressure gradient legend adapts to device mode
- "How to read" explanatory text added below the calendar legend
- Consistent coloring between interactive app and PDF report

#### Weekly Trends
- Overview trends changed from monthly to **weekly** grouping for denser, more useful data points
- X-axis labels show the Monday date of each ISO week

#### Print Readability
- All chart font sizes raised to minimum 6pt for legibility on standard office printers
- Pressure gradient bar enlarged with bolder labels
- AHI/Leak/SpO₂ legend squares and text enlarged

#### Report Improvements
- Trend chart pressure reference lines now mode-dependent: bilevel shows Rx EPAP/IPAP, APAP shows min/max auto range, CPAP shows fixed Rx pressure
- Dealer Information dialog now has per-field "Show on report" checkboxes — company and email shown by default, name and phone opt-in

#### Patient Information
- New full-demographics dialog: name, patient ID, sex, date of birth, height, weight, telephone
- All fields written to the device memory card and used in reports

#### Loading Screen
- Animated Home Medix logo with pulsing opacity effect while files load
- Clean branded transition instead of frozen UI

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

#### Security
- API key validation on cloud endpoints
- HTML-escaped user input in PDF templates
- Dealer info passed via environment variable instead of command-line arguments
- Atomic write for serial registry sync
- File validation in DAT and SUD parsers

#### Bug Fixes
- Fixed crash on no-DAT sessions (matplotlib canvas overflow)
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
- AHI severity coloring updated to AASM clinical standards
- Night calendar pressure segments refined for smoother gradient display
- Respiratory mechanics section prioritized in statistical report
- Clearer error message when trying to save a report that's already open

### Bug Fixes
- Fixed report version number not appearing in generated PDFs
- Fixed Auto On/Auto Off showing in single night prescribed settings
- Resolved file overwrite errors by adding timestamps to report filenames

---
