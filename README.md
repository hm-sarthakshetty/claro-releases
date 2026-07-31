# Home Medix Claro — Downloads

Desktop software for reading and reporting CPAP/BiPAP therapy data from Home Medix devices.

## Downloads

**[Download the latest Home Medix Claro release](https://github.com/hm-sarthakshetty/claro-releases/releases/latest)**

Current release: **v0.1.17** — 31 July 2026

Choose the installer for your platform:

- **Windows 10/11 (64-bit):** `Home_Medix_Claro_Setup_0.1.17.exe`
- **macOS (Intel and Apple silicon):** `Home_Medix_Claro_mac_0.1.17.dmg`

The `.yml`, `.zip`, and `.blockmap` files are updater metadata. Most users do not need to download them manually.

## Supported Devices

| Model | Type |
|-------|------|
| HM-CV-20 | CPAP |
| HM-BV-30 | BiPAP |

## Features

- Read SD card data from Home Medix CPAP/BiPAP devices
- Interactive session-by-session viewer with charts
- Clinical PDF reports (full analysis + single-night detailed)
- **Unified 6-panel therapy overview** — events, pressure, airflow, leak, snore, rolling AHI on one page
- **Breath-by-breath waveform analysis** from SD card DAT files (pressure, flow, snore at 5–10 Hz)
- **Event Window Analysis** — annotated detail views of apnea/hypopnea events with leak-corrected tidal amplitude
- **AASM-compliant scoring** — all respiratory events require ≥10s duration
- Gap compression for multi-segment sessions
- Date range filtering for targeted reporting
- Patient demographics (name, ID, DOB, sex, height, weight) stored on device
- Healthcare provider branding with per-field visibility control on reports
- In-app updates with background differential downloads and a silent restart-based install on Windows
- Weekly trend analysis for therapy adherence tracking
- Night calendar with compact nightly usage and clear four-hour compliance coloring
- Graceful recovery when an SD card is incomplete, unreadable, or disconnected

## Report Structure

### Clinical Report (full analysis)
1. Cover page — patient info, device info, analysis period
2. Therapy summary — per-night table with KPIs
3. Night calendar — color-coded therapy usage grid with bilevel pressure split
4. Statistical report — aggregate metrics across all sessions
5. Trend charts — usage, leak, event index, pressure over time
6. Settings history — chronological therapy parameter changes

### Single-Night Report
1. Clinical summary — KPIs, prescribed settings, events, outcomes
2. Therapy overview — 6-panel stacked chart with gap compression
3. Event window analysis (SD card data) — annotated apnea/hypopnea waveforms

## First Launch

1. Accept the data and privacy notice.
2. Enter the one-time dealer activation code. A progress indicator remains visible while the code is verified.
3. Complete Dealer Registration for report identification and support contact details.

Contact your Home Medix representative or email **claro@homemedix.in** to request an activation code.

## Updates

Claro checks for updates in the background. The left panel shows the installed version and update status. When an update is ready, select **Restart to update**.

On Windows, the app closes, applies the update silently to the existing installation, and reopens. The setup wizard is not shown. Electron still replaces packaged application files during this restart; it does not modify the running application in place.

## SD Card Troubleshooting

If Claro cannot open the selected device data:

1. Remove and reinsert the SD card.
2. Confirm the card contains a Home Medix device data file.
3. Try copying the card contents to the computer and opening the copied file.
4. If the card remains unreadable, use a replacement card and contact your Home Medix representative.

Claro keeps the application open after a card-read failure. Technical details are written to the local application log for support without exposing parser or system errors in the user interface.

## Release Notes

See [RELEASES.md](RELEASES.md) for version history.

## Support

For device or software support, contact your Home Medix dealer or email **claro@homemedix.in**.
