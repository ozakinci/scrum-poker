# Scrum Poker — Single-file app

This repository contains a single-page Scrum Poker app (`index.html`) that uses Firebase Realtime Database for live collaboration.

Included files
- `index.html` — main app (HTML/CSS/JS)
- `database.rules.json` — recommended Realtime Database rules (paste into Firebase console)
- `smoke-test.html` — optional automated smoke test for quick verification
- `PROGRESS.md` — progress log and recent changes
- `QA.md` — QA checklist and manual test instructions

Current app highlights
- Single-file app that syncs live across browsers using Firebase Realtime Database.
- Single name per user (add once; owner may delete their name).
- Owner-only voting: only the user who added a name can vote for that name.
- Card modes: Fibonacci and Days. Mode switches clear votes only (names remain).
- `New Round` clears votes (keeps names). `Reset` starts a fresh round and hides previous names/votes.
- Hidden votes show an `X` for rows that have a vote (blank when no vote).
- Connection indicator and status shown in the header (green/orange/red dot).
- Name input is disabled (greyed out) for a user after they add a name; it re-enables after delete or Reset.
- Barco logo added to the header.

Quick setup (Firebase)
1. In the Firebase console enable **Authentication → Sign-in method → Anonymous**.
2. Create a **Realtime Database** in your project (choose region).
3. In Realtime Database → Rules, replace the editor contents with the JSON in `database.rules.json`.
4. Ensure the `databaseURL` in `index.html` matches your project's Realtime Database URL.

Run locally
1. Open a terminal in this folder.
2. Start a simple HTTP server (recommended):

```bash
python -m http.server 8000
# or, if you have Node: npx http-server -p 8000
```

3. Open `http://localhost:8000/index.html` in two browser tabs for testing.

Deploy to GitHub Pages
1. Create a new repository on GitHub and push these files to the `main` branch.
2. In the repository Settings → Pages, set Source to the `main` branch (root) and save.

Security note
- The Firebase API key in `index.html` is not a secret. Enforce security with Realtime Database rules — the provided `database.rules.json` requires authentication and restricts writes to the player owner.

Testing resources
- See `QA.md` for a manual QA checklist and `smoke-test.html` for a quick automated connectivity test.
