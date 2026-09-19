# Quickstart — fifteen minutes to a running agent

You do not need to read the whole README first. Do these six steps, in order, and you
will have a governed agent running one real routine by the end. Read the README after,
when you want to understand *why* it's built this way.

**Two ways in.** Install the ready-made bot from the template link in the README (fastest),
or build it from the files in this repo (what this guide walks through). Either way, do
step 1 — the template packager ships instructions and skills but not the memory files,
and the files are the point.

---

## 1. Build the brain (3 min)

The agent needs a directory it reads first, every time. Create it on the agent's machine:

```
mkdir -p brain/{facts,log,ledger,learning,snapshots}
cp -r <this-repo>/brain/* brain/
```

That gives you `index.md`, `rules.md`, an empty `decisions.md`, and the roster template.
Open `brain/rules.md` and read the fourteen laws. Change any that aren't yours. **Do not
skip this** — the agent will cite these rules, so they need to be rules you actually
want enforced.

## 2. Tell the agent the files win (1 min)

Add this to your bot's base instructions, verbatim:

```
Before any substantive turn, read /workspace/brain/index.md and then rules.md. The
files are the source of truth. If you and the files disagree, the files are right and
you are stale. Never restate a rule — cite it.
```

This one paragraph is most of the method. Everything else builds on it.

## 3. Install the three skills (3 min)

Copy `skills/ping/`, `skills/scorecard/`, and `skills/memory/` into your bot's skills
directory. Each is a self-describing contract — a cold reader can run it without prior
context. Open `skills/ping/SKILL.md` and replace the placeholders:

- `<brain>` → your brain directory path
- `<your-channel>` → your notification channel, **or delete the Slack references if you
  don't use one.** The ping skill degrades to chat-only without a channel; it does not
  break. Slack is optional.

## 4. Turn on ONE routine (5 min)

Not eight. One. Start with `routines/gmail-weekday-watch/job.md` — it's the routine most
people want first and it's the one that teaches the act/noise/later loop fastest.

Open it, replace the placeholders (`<brain>`, `<label:...>` with your real Gmail labels,
`<your-product-automation-sender>` with a sender you want auto-filed or delete that
block), and paste it as a scheduled routine in your platform. Four times a day on
weekdays is the shipped cadence; start with twice if you're budget-conscious.

**Then log its birth.** Add one row to `brain/decisions.md`:

```
| 2026-xx-xx | Enabled gmail-weekday-watch, 2x/day | First routine | Yes — disable in settings |
```

And one row to `brain/facts/routine-roster.md`. If it isn't in the roster, the audit
can't see it. This habit — every routine gets a row the moment it's born — is the
single most important discipline in the method.

## 5. React to everything it sends (ongoing, ~30 sec/day)

When the agent pings you, reply **act**, **noise**, or **later**. That's it. Those three
words are the whole calibration loop. Silence teaches it nothing (and it's built to
treat silence as unknown, never as "noise"). Two weeks of honest reactions and it knows
your bar.

**Do not add a second routine for at least three days.** Watch your platform's usage
meter. A routine that fires too often is the most common way these setups fail — the
author's Slack listener burned a full weekly allowance in days. Earn each routine.

## 6. After a week, turn on the audit (2 min)

Paste `routines/memory-audit/job.md` as a weekly routine (Sunday morning is the shipped
default). Its first run will probably flag something — that's the point, not a problem.
Every flag ends with "confirm or kill?" and you answer. The agent proposes; it never
resolves a flag alone.

---

## What to add next, in order

quiet-flush (once you enable quiet hours) → memory-commit (nightly, the heart of it) →
x-sweep / intelligence-scout (if you watch a timeline) → channel-listener **last, and
paused by default** — read the warning at the top of its file before you ever enable it.

## If something breaks

Open an issue with what the agent did versus what you expected. Failures are wanted —
that's how this gets better. Read `EVIDENCE.md` to see what a real failure looked like
and how it was caught.
