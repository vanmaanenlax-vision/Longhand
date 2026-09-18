Weekly audit of /workspace/<brain>/. Timezone is America/Chicago. Use the local calendar date of this run.

Hard rules (same spirit as memory commit):
- Never edit rules.md, any skill, any watch bar, or any routine (including this one).
- Never move, rewrite, or delete a fact. No inference promoted to fact. Never invent a fact to close a TBD.
- If any store file listed in index.md is missing or unreadable, stop and report what's wrong in the assistant chat. Do not rebuild from memory.
- Snapshot is the only write outside log/. The only delete you ever do is old tars inside snapshots/ (keep newest eight). Never write outside /workspace/<brain>/ except running the check script at /workspace/<brain>-check.sh.
- Every flag in the report ends with "confirm or kill?" You resolve nothing alone. Propose changes; change nothing.
- This report is not a ping. One assistant chat message for the full report.
- Exception: unordered roster mismatch (3a) or Slack `<your-channel>`↔ledger reconcile miss (3b) also gets a delivery via the ping skill (dual-post per skill).

## VALIDATE
Re-read the authoritative source after each claim — not the tool return. Tag every claim:
- **CONFIRMED** — re-read and saw it
- **ACK-ONLY** — tool success only
- **UNVERIFIABLE** — no read path (approval queue, etc.)
Checks:
1. Re-read that today’s snapshot tar exists (stat) → **CONFIRMED** or don’t claim snapshot ok.
2. Re-read the check script output you just produced → **CONFIRMED**.
3. Roster / mirror / Slack `<your-channel>`↔ledger: re-read each source you cite → **CONFIRMED** per observation. Hash dimension UNAVAILABLE while local automation files are stale — do not print false-green hashes.
4. Audit report in assistant chat: in-thread → **CONFIRMED**; else **ACK-ONLY**.
5. Any ping from 3a/3b must pass the ping skill VALIDATE (re-read ledger + Slack `<your-channel>`).
Unexplained green without a CONFIRMED read = fail.

Do this in order:

1. Read /workspace/<brain>/index.md, then rules.md. If either is missing or unreadable, post what's wrong in the assistant chat and stop.

2. Snapshot. Write snapshots/<brain>-YYYY-MM-DD.tar.gz of the whole store excluding snapshots/. Keep newest eight tars. If today’s tar exists, leave it and note that. Then VALIDATE #1.

3. Health check. Run bash /workspace/<brain>-check.sh. If missing, report and skip — never rewrite. Include FAIL/WARN summary. VALIDATE #2.

3a. Roster drift: Read facts/routine-roster.md. Live list = source of truth for enabled/paused and schedule. If local automation files are stale (not reflecting live server state): hash dimension = UNAVAILABLE (do not print passing hashes). Missing local automation.json for expected folder → FAIL. Mismatch the operator did not order → list + one delivery via the ping skill. Do not change routines/roster.

3b. Slack `<your-channel>` ↔ ping-ledger reconcile (7-day or since last Sunday): the assistant's outbound ping-shaped posts must match ledger/pings.jsonl. Side door = channel without ledger; silent drop = ledger without channel. Listener replies don’t need ledger rows. Empty ping-hold ≠ quiet-hours worked unless write path shown. Miss → list + delivery via the ping skill.

4. Contradictions. List disagreeing fact lines / wrong subject. List only.

5. Stale. List [active] facts older than 90 days with no later confirming line. List only.

6. Rules recitation. Locked rules from memory, then paste rules.md, then differences. Do not edit rules.md.

7. Cost pass. Runs since last audit, pings, acted/noise/later. Flag runs-with-zero-pings, one-shots past date, runs outside hours. Propose only.

8. Lessons. Same lesson three times → propose skill. Do not create.

9. Post one assistant chat report covering 3–8 (include 3a/3b). Every flag ends with "confirm or kill?" Include evidence tags. Then run VALIDATE on the whole report.

Quiet example: "Memory audit — snapshot ok [CONFIRMED], check clean [CONFIRMED], roster live match [CONFIRMED], hash UNAVAILABLE (local mirror stale) [CONFIRMED], Slack `<your-channel>`↔ledger reconcile clean [CONFIRMED], contradictions none, stale none, rules match, cost flags none, lessons none."
