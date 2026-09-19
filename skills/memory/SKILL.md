---
name: memory
description: >-
  Use when reading or writing durable knowledge in /workspace/<brain>/, or
  at the start of any substantive turn.
---
# memory

Self-describing recipe. Files win; built-in Bot memory is a cache and may be stale.

## When to use
- **Read** at the start of any substantive turn (not banter).
- **Write** when the operator states a durable fact, a decision is made, a rule changes, an opportunity is scored, a watch bar changes, the operator corrects something, the operator replies `act`/`noise`/`later` to a ping, a routine finishes (run log), or an open question appears.
- Do **not** write chatter or anything that expires inside a week.

## Required inputs and access
- Store root: `/workspace/<brain>/` (shared by Bots on this account).
- No credentials, tokens, cookies, or API keys ever written here.

## Sequence — READ
1. Read `index.md`, then `rules.md`.
2. Read only the topic file(s) that apply — never the whole store.

## Sequence — WRITE
1. Subject picks the file (one place only):
   - Facts → `facts/SUBJECT.md` (`venture`, `product`, `stack`, `investing`, `people`, `watches`)
   - Decisions → `decisions.md` (append-only)
   - What happened → `log/YYYY-MM.md`
   - Routine runs → `log/routines.md` (append-only; format `- YYYY-MM-DD HH:MM CT | routine-name | outcome | pinged or quiet`)
   - Pings → `ledger/pings.jsonl` (+ reaction updates)
   - Ping tallies → `learning/signal.md`
   - Corrections → `learning/lessons.md`
   - Scorecard runs → `learning/bets.md`
   - Open questions → `learning/questions.md` (never invent a fact to close a TBD)
   - Dated dumps → `snapshots/` (routine-owned)
2. One dated line, append or edit in place. Keep every fact. Mark old lines `superseded YYYY-MM-DD`; never delete to “clean up.”
3. Same lesson three times → propose a skill (do not silently invent one).

## How to validate
- Wrote to the correct file only.
- No credentials.
- TBDs stay in `learning/questions.md` until the operator answers.
- `rules.md`, skills, and watch bars untouched unless the operator explicitly ordered the edit.

## What to return
- Read: the relevant excerpts / gates that apply to the current task.
- Write: which path(s) changed and the new line(s).

## What requires the operator’s approval
- Any edit to `rules.md`, any skill, or any watch bar (propose → the operator decides).
- Creating a new skill, a new agent, or connecting infra.
- Anything that ships, emails, texts family, tweets, buys/sells, or goes to production.
