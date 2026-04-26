# Progress — Scrum Poker

## Latest Session (2026-04-27 - Cleanup & Improvements)

### Removed External Image
- Removed external image link (`https://assets.barco.com/...`) from header
- Removed associated CSS styling for the logo
- Updated README to remove logo reference
- App now displays only emoji title without external dependencies

### Removed Smoke Test
- Deleted `smoke-test.html` (duplicated Firebase config, maintenance burden)
- Removed smoke test references from `QA.md` and `README.md`

### Stats Display Cleanup
- Removed duplicate "Average" stat (identical to Mean)
- Added mouse-over tooltips to Mean, Median, and Suggested boxes with brief explanations

### Removed Dead Code
- Removed commented-out Firebase DB rules at bottom of `index.html`
- Removed unused Firebase Analytics import and initialization

### Documentation Cleanup
- Cleaned up `QA.md`: removed outdated dates, conversational text, and developer notes
- Cleaned up `PROGRESS.md`: removed redundant historical summaries and commit lists

### Accessibility Improvements
- Changed card `<div>` elements to `<button>` elements for keyboard/screen-reader support
- Added `aria-sort` attributes to sortable table headers
- Added `aria-label` to connection status indicator
