# AGENTS.md

Guidance for agents working in this repository.

## Project

A single-page Scrum Poker app in one `index.html`, syncing live across browsers through Firebase Realtime Database. Players add a name once and only the owner of a name can vote for it. Votes stay hidden until reveal, then the app shows mean, median and a suggested value.

## Files

- `index.html` - the whole app: markup, styles, client logic and the Firebase config.
- `database.rules.json` - the recommended Realtime Database rules. Paste them into the Firebase console; this file is not loaded by the app.
- `PROGRESS.md` - progress log, newest session on top.
- `QA.md` - manual QA checklist across two browser tabs.
- `README.md` - what the app does and how to run it.

## Run

Serve the folder over HTTP (the app needs a real origin for Firebase auth):

```powershell
python -m http.server 8000
```

Then open `http://localhost:8000/index.html` in two tabs.

## Rules

- Keep it one file. The app is deliberately a single `index.html` with no build step.
- Access control lives in `database.rules.json`, never in the client. When the data shape changes, update the rules in the same change and paste them into the Firebase console.
- Preserve the role model: one name per user, owner-only voting, `New Round` clears votes and keeps names, `Reset` clears names and votes.
- A mode switch (Fibonacci, Days) clears votes only and leaves the names.
- Add each change to `PROGRESS.md` under a dated session heading, and update `QA.md` when behaviour a tester would check changes.
- Verify a change with `QA.md` in two live tabs before calling it done: names sync, hidden votes show `X`, reveal shows the statistics, and the connection dot goes green.

## Session triggers (clock in / clock out)

1. **Project memory** - this file is auto-loaded; use it directly.
2. **README freshness** - check that `README.md` matches the current behaviour and files; update it when they drift.
3. **Global blocks** - no project-specific start or end steps; the global blocks apply as-is.
