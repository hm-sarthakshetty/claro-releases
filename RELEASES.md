# Release Notes

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
