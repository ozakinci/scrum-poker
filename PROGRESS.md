# Progress — Scrum Poker

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

Files added / updated
- `index.html` — main app (updated iteratively during development).
- `database.rules.json` — recommended DB rules (publish these in the Firebase console).
- `README.md`, `PROGRESS.md`, `QA.md` — documentation and instructions (this file included).
- `smoke-test.html` — automated smoke-test helper.

Next steps
1. Push repository to GitHub and enable GitHub Pages for public hosting.
2. Optionally tighten database rules further (restrict by domain or user claims) if you move to production.
3. Optional: implement admin cleanup for old rounds if you prefer physical deletion instead of round scoping.
