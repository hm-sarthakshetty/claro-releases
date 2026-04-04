# Release Notes

---

## v1.26.404c — 4 April 2026

### UI Polish: Unified Pressure Gradient, Patient Profile, Branding

#### Pressure Coloring
- **Single source of truth** — fixed 27-color gradient from 4–30 cmH₂O used everywhere (night calendar bars, legend, all therapy modes)
- No more separate bilevel vs CPAP/APAP color systems — one gradient, consistent colors
- Legend dynamically shows the relevant pressure range based on actual session data
- Fixed bug where legend showed 4–10 when sessions had pressures up to 13

#### Patient Profile
- Sidebar now shows full patient demographics: name, ID, sex, date of birth with age, height, weight, phone
- Clean table layout with section headers (Patient / Device)
- Empty fields display "—"
- Updates live when patient info is edited

#### Branding
- App header: "Claro" / "Clinical Therapy Reports"
- Removed native browser tooltip from night calendar rows

#### Weekly Trends
- Overview trends changed from monthly to weekly grouping for denser data points

---

## v1.26.404b — 4 April 2026

### Polish: Bilevel Coloring, Print Readability

#### Night Calendar
- Bilevel sessions show horizontally split time bars (top = IPAP, bottom = EPAP)
- "How to read" explanatory text added to calendar legend

#### Print Readability
- All chart font sizes raised to minimum 6pt
- Enlarged pressure gradient bar and AHI/Leak/SpO₂ legend

#### Report Changes
- Pressure trend chart reference lines are mode-dependent (bilevel = EPAP/IPAP, APAP = min/max, CPAP = Rx)
- Dealer dialog: per-field "Show on report" checkboxes
- Full patient demographics dialog (name, ID, sex, DOB, height, weight, phone)
- Animated loading screen with Home Medix logo

---

## v1.26.404 — 4 April 2026

### Major: Waveform Reports & AASM Compliance

#### Waveform Analysis
- **Unified 6-panel single-night overview** — Event Lanes, Pressure, Airflow, Leak, Snore, Rolling AHI with gap compression
- **Works with and without SD card** — DAT files give high-resolution traces; SUD-only shows discrete data
- **Event Window Analysis** — annotated apnea/hypopnea windows with leak-corrected tidal amplitude, rolling mean, baseline/threshold detection, and clinical annotations
- **Mode-aware pressure rendering** — bilevel envelope, APAP single line, CPAP flat trace

#### AASM Compliance
- All respiratory events (OA, CA, HY) require ≥10 seconds duration per AASM standards
- Applied across parser, interactive charts, and PDF reports

#### Security
- API key validation on cloud endpoints
- HTML-escaped user input in PDF templates
- Dealer info via environment variable
- Atomic write for serial registry sync
- File validation in DAT and SUD parsers

---

## v1.26.403 — 3 April 2026

### What's New
- Redesigned clinical report cover page
- Date range filtering for clinical reports
- Dealer information system
- Improved chart quality and readability

### Bug Fixes
- Fixed report version number not appearing in PDFs
- Fixed Auto On/Auto Off in single night settings
- Resolved file overwrite errors

---
