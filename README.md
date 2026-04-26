# Scrum Poker — Single-file app

This repository contains a single-page Scrum Poker app (`index.html`) that uses Firebase Realtime Database for live collaboration.

Included files
- `index.html` — main app (HTML/CSS/JS)
- `database.rules.json` — recommended Realtime Database rules (paste into Firebase console)
- `PROGRESS.md` — progress log and recent changes
- `QA.md` — QA checklist and manual test instructions

Current app highlights
- Single-file app that syncs live across browsers using Firebase Realtime Database.
- Single name per user (add once; owner may delete their name).
- Owner-only voting: only the user who added a name can vote for that name.
- Card modes: Fibonacci and Days (default). Mode switches clear votes only (names remain).
- **Statistics display** (when votes revealed): Mean, Median, and Suggested value with smart fallback logic (Mode if consensus, Median if scattered votes) + custom rounding rules.
- `New Round` clears votes (keeps names). `Reset` starts a fresh round and hides previous names/votes.
- Hidden votes show an `X` for rows that have a vote (blank when no vote).
- Connection indicator and status shown in the header (green/orange/red dot).
- Name input is disabled (greyed out) for a user after they add a name; it re-enables after delete or Reset.
