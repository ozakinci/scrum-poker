# Progress — Scrum Poker

## Latest Session (2026-04-27 - Cleanup)

### Removed External Image
- Removed external image link (`https://assets.barco.com/...`) from header
- Removed associated CSS styling for the logo
- Updated README to remove logo reference
- App now displays only emoji title without external dependencies

## Previous Session (2026-03-31 - Continued Development)

### UI Enhancements
- **Logo & Title Sizing**: Logo width reduced from 200px to 100px; title font size increased from 20px to 36px for better visual hierarchy
- **Button Reordering**: Moved "Days" button to the left of "Fibonacci" button for better UX
- **Status Text Color**: Changed "Connected (anon)" text color from muted gray to white for better visibility on blue header background

### Default Mode Change
- Changed default voting mode from **Fibonacci** to **Days** across the application
- Reset button now defaults to "Days" mode instead of "Fibonacci"
- State initialization logic updated to use "Days" as the default

### Statistics Display Feature (NEW)
Added real-time statistics boxes displayed in the Players panel when votes are revealed:
- **Mean**: Average of all numeric votes (to 1 decimal place)
- **Median**: Middle value of sorted votes (to 1 decimal place) 
- **Average**: Duplicate of mean for clarity
- **Suggested**: Intelligent vote recommendation using:
  - **Mode** (most repeated vote) if there's clear consensus (one value appears more frequently)
  - **Median** as fallback when votes are scattered or tied (no clear consensus)
  - Custom rounding rules: decimals ≤0.5 round to .5, decimals >0.5 round to next whole number
- Stats boxes are **only visible when votes are revealed**; hidden otherwise per user request
- Stats correctly filter by current `roundId` to exclude votes from previous rounds

### Bug Fixes
- **Firebase Connection TypeError**: Fixed missing Reveal and New Round buttons in HTML that caused `TypeError: Cannot read properties of null (reading 'addEventListener')`
- **Variable Declaration Duplicates**: Removed duplicate declarations of UI reference variables
- **Stats Calculation Filtering**: Added `roundId` filtering to stats calculation to ensure votes from previous rounds don't contaminate current statistics

### Recent Commits
1. `Fix: Resolve TypeError for addEventListener on mode buttons, ensuring Firebase connection and app functionality.`
2. `Fix: Restore missing Reveal and New Round buttons in Players panel, resolving TypeError`
3. `Feature: Implement missing calculateAndRenderStats function for mean, median, average, and suggested vote display`
4. `Fix: Filter stats calculation by current roundId to exclude votes from previous rounds`
5. `Feature: Improve suggested value logic - use Mode if clear consensus, fallback to Median on ties`

---

## Previous Session Summary (2026-03-31 - Initial Development)

Date: 2026-03-31

Summary
- Implemented a single-file Scrum Poker web app (`index.html`) with Firebase Realtime Database collaboration.
- App is functional locally (served via simple HTTP) and connects to your Firebase Realtime Database using Anonymous Authentication.

Completed features and notable changes
- Single name per user: the UI uses a single input for a user to add their name. A user may not add more than one name simultaneously.
- Owner-only voting: a user may only vote for their own name; votes are stored per-player in the DB.
- Card sets: Fibonacci and Days modes; both start with `?` then `☕` then the numeric sequence. Fibonacci includes an extra number so both sets have the same card count.
- Mode behavior: switching modes clears all existing votes but preserves names.
- New Round: clears votes only (keeps names).
- Reset button: bright red reset at top-right of the name panel that starts a fresh round (new `roundId`) and hides previous names/votes.
- Hidden votes: non-revealed votes show an `X` for players who have voted (rows with no vote remain blank); owners see their own numeric vote even when hidden.
- Sortable table: table columns are sortable by name and by vote value (asc/desc).
- Duplicate prevention: names are case-insensitive and unique.
- Delete: owner sees a left-side `−` control to remove their name; once removed the owner can add again immediately.
- UI polish: added Barco logo in header, connection status dot (green/orange/red), programming-friendly color palette, and disabled/greyed name input after add.

Stability & realtime fixes
- Initial-load: listeners are attached after anonymous auth so the page loads the latest DB snapshot immediately on open.
- Live updates: state and player changes are propagated to all connected clients as soon as they occur (fixes earlier delay where changes appeared only after interaction).
- Resolved race conditions: adding/removing names now double-checks DB state and updates local cache so owners are not blocked from re-adding after reset/delete.

Testing done
- Ran automated smoke test (`smoke-test.html`) to validate auth, add/delete, set vote, read state, and cleanup.
- Manual QA performed locally using two browser tabs and the checklist in `QA.md`.

Files included
- `index.html` — main app (HTML/CSS/JS)
- `database.rules.json` — recommended DB rules (publish these in the Firebase console)
- `README.md`, `PROGRESS.md`, `QA.md` — documentation and instructions
- `smoke-test.html` — automated smoke-test helper
