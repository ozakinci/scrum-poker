# QA Checklist — Scrum Poker

## Automated Smoke Test (2026-03-31)
All passed:
- Anonymous sign-in
- Add player
- Set vote
- Read player back
- Set state (revealed=true)
- Read state back
- Delete player
- Reset state

## Manual QA (open two browser tabs)

1. Start a local HTTP server in the project folder:

```bash
python -m http.server 8000
```

2. Open two browser tabs (Tab A and Tab B) at `http://localhost:8000/index.html`.

3. Wait for the status in the header to show `● Connected (anon)` (green dot). If it's orange the page is connecting; red indicates a problem.

4. Add a player in Tab A:
   - In the name input type `Alice` and press Enter or click `Add`.
   - Expected: `Alice` appears in Tab A and within a moment in Tab B.
   - After adding, the name input and `Add` button in the adding client should be disabled/greyed until the owner deletes their name or Reset is pressed.

5. Add another player in Tab B:
   - Type `Bob` and press Enter or click `Add`.
   - Expected: `Bob` appears in both tabs.

6. Vote as Alice (Tab A):
   - Click a card value (e.g., `3`) in Tab A.
   - Expected: In Tab A you see your numeric vote in the table. In Tab B the vote remains hidden and the row shows `X` if Alice voted (blank if no vote yet).

7. Hidden vote behavior:
   - Non-owner clients see `X` in rows where a vote exists while votes are hidden; owners always see their own numeric vote even when hidden.

8. Reveal votes (either tab):
   - Click `Reveal`.
   - Expected: Both tabs now display all votes.

9. New Round:
   - Click `New Round`.
   - Expected: All votes clear on both tabs and `Reveal` returns to hidden. Names remain.

10. Reset button:
   - Click the red `Reset` button in the top-right of the name panel.
   - Expected: The app starts a fresh round (previous names and votes are hidden), `Reveal` resets to hidden, and everyone can add names again immediately.

11. Mode toggle:
   - Click `Days` mode; expected: cards switch to day values and existing votes clear (names remain).
   - Note: Switching mode clears all existing votes.

12. Sorting:
   - Click the `Name` header to toggle asc/desc; verify ordering.
   - Click the `Story Points` header to sort by vote value.

13. Delete name:
   - Click the left-side `−` button next to your name to remove it.
   - Expected: Your name disappears and you can add again immediately (input re-enables on that client).

14. Duplicate name validation:
   - Try adding `ALICE` (different case); expected: blocked with an alert (names are case-insensitive unique).

15. Initial load & realtime check:
   - Open Tab A, add a player, then open Tab B (fresh tab). The name should appear in Tab B automatically within a few seconds without requiring additional interaction.
   - If Tab B does not reflect changes immediately, open DevTools → Console and paste any errors here.

16. Smoke test (optional):
   - Open `smoke-test.html` and click **Run Smoke Test**. It will sign in anonymously, add a `qa-test-<timestamp>` player, set a vote, and clean up. Use this to confirm DB connectivity programmatically.

Notes
- If you want Reset to physically delete all players from the DB (instead of hiding via `roundId`), that requires an admin/CLI action or relaxed rules for a deletion endpoint — I can help implement that if desired.
- If you see any problems or console errors, copy and paste them here and I will debug immediately.
