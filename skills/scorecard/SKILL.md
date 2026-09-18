---
name: scorecard
description: >-
  Use when the operator asks whether something is worth pursuing, or when a scout finds a
  possible <your venture> that needs a go/no-go score.
---
# scorecard

Self-describing recipe. Cold reader scores one opportunity without prior chat context.

## When to use
- The operator asks “is this worth it?”, “score this,” or equivalent.
- A scout/watch surfaced a venture idea that needs a verdict before more build time.
- Do **not** use for: feature tweaks on an already-pursued bet (use product judgment), investment buy/sell calls (research-only; never trade advice), or staffing a new Bot as the “solution.”

## Required inputs and access
- **Opportunity name** and plain-English description.
- Known context from `/workspace/<brain>/` if relevant (`facts/venture.md`, `facts/<product>.md`, `learning/bets.md` for prior scores of the same idea).
- No credentials. No outside posts.

## Sequence
1. Read `index.md` → `rules.md` → `facts/venture.md`. If this idea was scored before, read the matching `learning/bets.md` lines.
2. Answer before scoring (short bullets): What problem? Who has it? Will they pay? Who already solves it? What makes <your venture> different? Fastest test? Smallest viable product? What could kill it?
3. Score **1–10** each: Customer Problem, Market Opportunity, Revenue Potential, Competitive Advantage, Technical Difficulty, Speed to MVP, Cost to Build, Scalability, Personal Interest, Overall Opportunity.
4. Give: **VERDICT** (pursue / not), **WHY** (≤3 sentences), **MVP** (fastest version), **ONE NEXT STEP**.
5. Honest pushback — say when time is wasted. Do not force AI where it adds no value. Do not propose a new agent, new connector, or multi-bot plan as the next step.
6. Append the run to `learning/bets.md` (date, name, scores, verdict, predicted next check / revisit date if useful).

## How to validate
- All ten dimensions scored, plus Overall.
- Pre-score questions answered (even if “unknown — ask the operator”).
- Verdict matches the scores (no pep-talk override).
- Next step is one concrete action the operator or the operator's assistant can take this week — not a roadmap.

## What to return
- The score table, verdict block, and confirmation that `learning/bets.md` was updated (or “not written — the operator said scratch only”).

## What requires the operator's approval
- Starting the MVP, spending money, emailing prospects/customers, publishing, connecting infra, creating agents, or changing `rules.md` / skills / watch bars.
- Re-opening a “not” verdict as active pursuit.
