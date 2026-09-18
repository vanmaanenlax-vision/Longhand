Nightly commit of /workspace/<brain>/. This run writes the day down whether or not it was remembered during the day. Timezone is America/Chicago. Use the local calendar date of this run.

Hard rules:
- Write only what the operator said or what actually happened. No inferences. No conclusions of your own promoted to facts.
- Never edit rules.md, any skill, or any watch bar. Never write to snapshots/. Never create or change a routine, including this one.
- Never invent a fact to close a TBD.
- If any store file listed in index.md is missing or unreadable, do not rebuild it from memory. Post what's wrong in the assistant chat and stop.
- If nothing durable happened, that is a real result. Still post the status-counts line in the assistant chat.
- The status-counts line is not a ping. Do not use the ping skill for it. Status counts: one assistant chat message every night. Do not post status counts to Slack.
- **Phone-path rule:** Never post to Slack `<your-channel>` from this routine. Anything that should reach the phone (including the below-bar digest) goes through `ledger/ping-hold.jsonl` for the 7:00 AM `ping quiet flush`, which delivers via the ping skill (quiet-hours gate). Direct `<your-channel>` posts from memory-commit are forbidden.

## VALIDATE
After writes and the status post, **re-read the authoritative source** — not the tool return. Tag every claim with exactly one of:
- **CONFIRMED** — re-read and saw it
- **ACK-ONLY** — tool success only; nothing read back
- **UNVERIFIABLE** — no read path (e.g. the operator’s approval queue)
Checks:
1. Re-read each file you claim to have appended; cite the new line. Missing → do not claim written. **CONFIRMED** per file found.
2. Status message in assistant chat: visible in-thread → **CONFIRMED**; else **ACK-ONLY**.
3. Digest hold: re-read `ledger/ping-hold.jsonl` for the hash → **CONFIRMED** or fail the claim. Never claim a Slack `<your-channel>` digest post.
4. Approval-gated actions: **UNVERIFIABLE** / SUBMITTED-PENDING-APPROVAL until the operator confirms card clear.
Unexplained “done” without a CONFIRMED read = fail.

Do this in order:

1. Read /workspace/<brain>/index.md, then rules.md. If either is missing or unreadable, post what's wrong in the assistant chat and stop.

2. Review today's assistant chat with the operator and every routine run since the last memory-commit (or since local midnight if this is the first commit). Look up connector tools each run. Facts only: what was said, what ran, what was sent. Review Slack `<your-channel>` as needed for act/noise/later and below-bar digest acts.

3. Append what happened to log/YYYY-MM.md for today's month. Dated lines. Facts only. If that month file does not exist yet because the month just changed, create it and then append. Do not rebuild any other missing file.

4. Append any decision the operator made today to decisions.md (append-only). Edit affected facts/ lines in place: mark the old line superseded YYYY-MM-DD and add the new one. Never delete a line.

5. Route learning. Any correction the operator made goes to learning/lessons.md. Any scorecard run goes to learning/bets.md. Any act/noise/later reaction (on Slack `<your-channel>` or in this chat; silence stays unknown — per the ping skill; backfilled unknowns stay unknown unless the operator later replies) updates that line in ledger/pings.jsonl and the tally in learning/signal.md. If the operator replied act on a below-bar digest line (this chat or Slack `<your-channel>`), loosen that topic in learning/signal.md. Any new unknown goes to learning/questions.md.

6. Durable routine log. Read log/routines.md (create with the header from index if missing — never invent past runs). For every standing routine that ran today, ensure one append-only line exists: `- YYYY-MM-DD HH:MM CT | <routine name> | <outcome> | <pinged|quiet>`. Prefer the routine's own append if present; only backfill gaps. Count lines added.

7. Check learning/bets.md for revisit dates on or before today. Flag those bets. Do not fill outcomes yourself.

8. Below-bar digest (calibration window only): during your first ~2 calibration weeks. After that window ends, skip permanently. From today's ledger/below-bar.jsonl, pick up to 5 notable one-liners. Format: `- <item> — <below-bar|dedupe|promo>`. If none, omit.

9. Post status counts in assistant chat: "Memory commit — N log lines, N decisions, N fact edits, N lessons, N ping reactions, N routine-log lines. Flags: ..." Quiet example with Flags: none. Do **not** append digest lines to the night message; if digest exists say only "Below-bar digest: N lines held for 7:00 AM flush."

10. Calibration window only, if digest has lines: append one JSON line to ledger/ping-hold.jsonl for 7:00 AM flush. Do **not** post to Slack `<your-channel>`. Then VALIDATE re-read of that hold line.

Finally run VALIDATE on all claims in this run before finishing. Do not write to snapshots/. Do not change skills, rules.md, watch bars, or routines.
