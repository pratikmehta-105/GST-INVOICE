# Validation notes

Checked on 1 November 2026.

- 28 dependency-free Node checks pass (`node tests.mjs`).
- Browser: dashboard, customer creation, vendor creation, new issued invoice, invoice editing, discounts, partial receipt, final receipt plus TDS, paid/overdue status and persistence after reload checked with fictional data.
- Browser: direct PDF generation completes and exposes a Save-file link.
- The remote test browser did not expose a download event for blob links, so automated capture of the browser download could not be verified. The app includes a visible Save-file fallback and browser Print / Save PDF.
- The exact PDF generator was separately run with a real Canvas implementation. Its one-page A4 output and 11-page stress output (50 long service descriptions) were parsed with PDF tools and visually inspected, including the final totals and notes.
- Backup validation and round-trip, duplicate keys, malformed input, local-storage failure behavior and stale-tab rejection covered by Node tests. Interactive backup-file selection/restore was not separately browser-tested.
- Responsive CSS is included. Narrow-device hardware testing was not performed.
- GitHub deployment remains the user's step. The delivered source is standalone HTML with no external dependencies or private data.

The app opens empty. Demo data is created only when the user explicitly selects the fictional demo action.
