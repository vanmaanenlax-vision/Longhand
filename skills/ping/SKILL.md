---
name: ping
description: >-
  Use when sending any proactive alert to the operator from a watch, scout, or routine.
  Dual-post assistant chat + Slack <your-channel>. Not for conversational replies,
  memory-commit status lines, or quiet runs.
---
# ping

Self-describing recipe. A cold reader (any Bot on this account) can run it without prior chat context.

## When to use
- A standing watch or routine found something that clears that watch’s bar and needs the operator’s attention.
- Delivery is **dual-post**: assistant chat **and** Slack `<your-channel>`.
- Do **not** use for: ordinary chat answers, the nightly memory-commit status line (counts), or “nothing to report” silence.
- Watches bind to this skill for delivery. Quiet / skip is a delivery outcome of this skill — do not invent a parallel quiet path that bypasses it.

## Required inputs and access
- **Item** — one concrete finding (fact, link, why it matters).
- **Watch name** — which routine/scout produced it (for ledger + signal).
- **Source URL** — original link when one exists (not a repost/summary account).
- **Store** — `/workspace/<brain>/ledger/pings.jsonl` (dedupe + sent), `ledger/ping-hold.jsonl` (quiet-hours hold), `ledger/below-bar.jsonl` (calibration near-misses), `learning/signal.md` (tallies).
- **Delivery** — assistant chat **and** Slack `<your-channel>` (same body).

## Quiet hours (America/Chicago)
Quiet hours are **9:00 PM–7:00 AM** local. **Always evaluate this gate before posting** — never skip it unconsciously.
- **Outside** quiet hours: deliver immediately (steps below).
- **During** quiet hours, post **only** for:
  1. family-relevant (per `facts/people.md`), OR
  2. a real security alert, OR
  3. a same-day deadline (must act before next morning), OR
  4. **operator-requested path-check / test ping only** — the operator explicitly asked to send a test, or `watch:test` after the operator ordered that test. Still take this as an **explicit exempt branch** (do not “just send”). On the ledger line set `quiet-hours=exempt:operator-test`. No other category may use this exemption (not newsletters, scouts, below-bar digests, or “useful FYI”).
- Non-exceptions during quiet hours: append one JSON line to `ledger/ping-hold.jsonl` (`date`, `item`, `url`, `hash`, `watch`, `why_it_matters`, `next_step`, `held_at`) and **stop**. Do **not** write `pings.jsonl` yet. Do **not** post. Dedup against both `pings.jsonl` and `ping-hold.jsonl` before holding.
- Morning flush: the quiet-flush routine (daily 7:00 AM) delivers held items via this skill, then clears that batch from the hold file.

## Sequence
1. Read `/workspace/<brain>/learning/signal.md` for that watch’s bar; if below bar, go to **Quiet / below-bar path** (do not post).
2. Dedupe: hash/normalize the item + URL against `ledger/pings.jsonl` **and** `ledger/ping-hold.jsonl`. If already sent or held, stop (optionally log `dedupe` on the below-bar path during calibration — see below).
3. Compose **one** message body, **four lines max**:
   1. WHAT — one sentence, plain English.
   2. WHY IT MATTERS — one sentence tied to `<your venture / products / positions>`, or family.
   3. LINK — original source URL, or “none” if none.
   4. NEXT STEP — one concrete action, or “watch only.”

### Substantiated-change reports
When the ping reports a **substantiated change** (servicer move, date retarget, status flip, etc.):
- State explicitly **what does NOT change** (terms, account numbers, logins, payment methods, etc. still the same).
- Do not only describe the delta and leave the rest implied.
- If unsure what is unchanged, say so — do not invent “unchanged” claims.
4. **Quiet-hours gate (always run):** if now is 9:00 PM–7:00 AM America/Chicago, check the exception list (family / security / same-day deadline / operator-requested path-check). If none apply, append to `ledger/ping-hold.jsonl` and stop (no post, no `pings.jsonl`). If operator-test exempt applies, proceed and set `quiet-hours=exempt:operator-test` on the ledger line.
5. Post that **same** message to **assistant chat** and Slack `<your-channel>`. Do not follow, like, or reply on X. If Slack post fails, still post to assistant chat and note Slack failure there.
6. Append one JSON line to `ledger/pings.jsonl`: `date`, `item`, `url`, `hash`, `reaction` (`unknown` until the operator replies), `watch`.
7. If this run is a standing routine, append one line to `log/routines.md`: `- YYYY-MM-DD HH:MM CT | <routine> | <outcome> | pinged` (America/Chicago).

## Quiet / below-bar path (nothing meets the bar / skipped)
- Do not post. If a standing routine: `quiet` in `log/routines.md`.
- **Calibration near-misses** (America/Chicago dates in **your calibration window**): when an item was **considered** and skipped, append one JSON line to `ledger/below-bar.jsonl`: `date`, `item`, `watch`, `reason` (`below-bar` | `dedupe` | `promo`). Notable only — skip trivia. After **your calibration window**, do not write `below-bar.jsonl` (retired with the digest).
- If calibration shows a watch skipping notable items **without** reaching this quiet path, flag the operator — that watch is bypassing the skill and needs a fix.

## VALIDATE
Re-read from the authoritative source after every delivery attempt — **not** the tool return value. Tag every claim with exactly one evidence tag:
- **CONFIRMED** — re-read the source and saw it
- **ACK-ONLY** — tool returned success; nothing read back
- **UNVERIFIABLE** — no read path from this Bot (e.g. the operator’s approval queue)

Checks:
1. Re-read `ledger/pings.jsonl` (or `ledger/ping-hold.jsonl` if held): new line with expected hash/watch present → **CONFIRMED**; else do **not** claim sent/held.
2. Re-read Slack `<your-channel>` recent history for the matching outbound body → **CONFIRMED**; Slack tool ok but unread → **ACK-ONLY**; no read path → **UNVERIFIABLE**.
3. Assistant chat: message visible in-thread → **CONFIRMED**; else **ACK-ONLY** on send success.
3b. **Phone push delivery is always UNVERIFIABLE.** Slack/`<your-channel>` presence (or assistant chat presence) is not proof a push buzzed the operator’s phone. Never claim “delivered to phone” / “you got a push.” Tag phone-arrival claims **UNVERIFIABLE** always — the operator checks the device.
4. Still enforce: one item per body; no buy/sell; dedupe; quiet-hours gate; below-bar path when applicable.
5. Approval-gated steps: **UNVERIFIABLE** until the operator confirms card clear — never log complete on a success string alone.

## What to return
- Sent: only if VALIDATE #1 (and #2/#3 as applicable) are **CONFIRMED** or honestly tagged; include evidence tags.
- Held: only if hold-file line re-read **CONFIRMED**; tag it.
- Not sent: “quiet — below bar / duplicate / nothing to report” (no false delivery claim).
- Never return “sent/filed/done” on ACK-ONLY or UNVERIFIABLE without saying so.

## What requires the operator’s approval
- Any follow-up that **acts** on the ping (send email/SMS, buy/sell, tweet, connect a service, create an agent, edit `rules.md` / skills / watch bars, ship product).
- The operator replies with `act`, `noise`, or `later` in the assistant chat. Update the ledger line and `learning/signal.md` only on an **explicit** reply.
- **Silence stays `unknown`.** Only an explicit `noise` from the operator counts against a watch’s signal. Never raise a watch bar based on non-response.
- **Test pings** (`watch: test` or marked TEST): still post to chat and ledger, but do **not** count in `learning/signal.md` tallies. Test pings may deliver during quiet hours **only** under the operator-requested path-check exemption above (explicit operator ask). Always evaluate the quiet-hours gate; log `quiet-hours=exempt:operator-test`. Do not treat “test/not-tallied” alone as a quiet-hours bypass.
- **Below-bar digest `act`:** if the operator replies `act` on a below-bar digest line in assistant chat, loosen that topic in `learning/signal.md` (explicit act only).
