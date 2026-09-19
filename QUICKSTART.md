# Quickstart — a running routine in about fifteen minutes

This guide is written for **Grok Bot**, where Longhand was built. Every step names the
real screen or command. If you're on another platform, the two things that differ are
called out where they happen: where base instructions live, and how skills install.

**What "fifteen minutes" honestly gets you:** a complete brain, three skills installed,
and one real routine running against your inbox. Not the full eight-routine setup —
that's a week of adding one at a time. The first fifteen minutes gets the loop turning.

**You need:** a Grok Bot agent with its own computer, Gmail connected to it, and about
fifteen minutes.

**One convention:** angle-bracket tokens like `<brain>` are things *you* replace before
running. Each file's README says which ones. Routine prompt files contain nothing else,
so if you see an angle-bracket token in a prompt file, it's yours to fill.

---

## 1. Get the files onto the agent's computer (2 min)

In the agent's chat:

```
Clone https://github.com/vanmaanenlax-vision/Longhand into /workspace/longhand
```

Everything below refers to `/workspace/longhand/...` (the repo) and `/workspace/brain`
(the memory store you're about to build). Those are the real paths on a Grok Bot
computer. On another platform, use wherever your agent's persistent working directory
is and substitute throughout.

## 2. Build the brain (1 min)

```
cp -r /workspace/longhand/brain /workspace/brain
```

That's the whole step. The repo ships a **complete** scaffolding — `index.md`,
`rules.md`, `decisions.md`, the roster, every ledger/learning/log file the skills read,
and five `facts/` stubs (stack, people, venture, product, watch-feed-senders), each with
one clearly-fictional example row. Nothing needs to be created by hand.

Open `/workspace/brain/rules.md` and read the fourteen laws. You don't have to change
anything yet — you'll edit them as you learn what you actually want enforced. Just know
they're there, because the agent is about to start citing them.

**About `<brain>`:** every routine and skill in the repo says `/workspace/<brain>/...`.
Replace `<brain>` with the folder name — `brain` — so paths become `/workspace/brain/...`.
Not a full path, just the name.

## 3. Put the one rule where the agent reads it (2 min)

Grok Bot has no field called "instructions." Base instructions live in the agent's
**Description**. Path: open the agent's chat → click the agent's name in the header (or
Cmd+Shift+I) → gear → the agent's Settings → **Description**.

Paste this at the top of the Description, verbatim:

```
Before any substantive turn, read /workspace/brain/index.md and then rules.md. The
files are the source of truth. If you and the files disagree, the files are right and
you are stale. Never restate a rule — cite it.
```

This one paragraph is most of the method. Everything else builds on it. *(Other
platforms: this goes in the system prompt or custom-instructions field — whatever your
agent reads before every turn.)*

## 4. Install the three skills (3 min)

Grok Bot does **not** load skills from a folder. They install through the agent's own
tooling. In the agent's chat:

```
Install three skills from the repo using update_state (target: skill, action: write),
one each from these files — use the name, description, and body from each SKILL.md:
  /workspace/longhand/skills/ping/SKILL.md
  /workspace/longhand/skills/scorecard/SKILL.md
  /workspace/longhand/skills/memory/SKILL.md
Before writing, replace the only two placeholders the skills contain:
  <brain> -> "brain" (in all three)
  <your-channel> -> [the Slack channel I watch, OR: "I don't use Slack; delete the
  Slack references"] (ping skill only)
There are no other placeholders in the skills. Confirm none remain before writing.
```

When it's done, the three show up as skill pills in chat and under the agent's
Settings. **Slack is optional.** Without a channel, the ping skill delivers to chat only;
it does not break. *(Other platforms: install the three SKILL.md files however your
platform adds skills.)*

**If you already have skills with similar names** (e.g. from an earlier setup), install
these under the names `ping`, `scorecard`, `memory` and retire the old ones — two
overlapping ping skills will fight. To retire on Grok Bot, tell the agent:
ask it to list installed skills with their ids (there is no list action on `update_state` — the id is the skill pill / folder slug), then `update_state target skill, action delete, id <old-skill-id>` for each old one.

## 5. Stage ONE routine — the minimal one (4 min)

Not the full eight. Not even the full gmail watch. Start with
`/workspace/longhand/routines/gmail-weekday-watch/minimal.md`. It is a **pure prompt
with one placeholder** (`<brain>`) and needs no personal data to run: it pings real
people, bills, and deadlines, archives the rest, and ends every run at inbox zero.
Read the `README.md` next to it first — it explains the three files in that folder and
which one you actually paste.

Open `minimal.md`. Replace `<brain>` with `brain`. It names two Gmail labels literally —
`keeper` and `Purge`. **If you already have labels that mean "keep this" and "delete
later," rename those two words in the file to match — don't create duplicates.** If
you have no such labels, create `keeper` and `Purge` now, either in Gmail (left
sidebar → + next to Labels) or by telling the agent: "create Gmail labels keeper and
Purge." That's the only setup.

Then, in the agent's chat:

```
Create a routine named gmail-weekday-watch from /workspace/longhand/routines/
gmail-weekday-watch/minimal.md, schedule 0 9,15 * * 1-5 (weekdays 9am and 3pm), and
create it PAUSED. Do not run it yet.
```

Twice a day is the right starting cadence. The full version runs four times; earn that.

## 6. Log its birth, then turn it on (2 min)

**Before you enable it**, record that it exists. This is the single most important habit
in the method — if a routine isn't in the roster, the audit can't see it.

Add one row to `/workspace/brain/decisions.md`:

```
| 2026-xx-xx | Created gmail-weekday-watch (minimal), 2x/day weekdays, paused | first routine | yes — delete routine |
```

Add one row to `/workspace/brain/facts/routine-roster.md`. The prompt hash is:

```
sha256sum /workspace/longhand/routines/gmail-weekday-watch/minimal.md | cut -c1-16
```

This works because `minimal.md` is a pure prompt — the file you hash is exactly the
file you pasted, so the roster hash matches what's running. (If you ever edit the
routine's text in the platform, re-hash the file you edited from, not the original.)

Now enable the routine. Log a second decisions row: `enabled gmail-weekday-watch`. One
decision per row — creating and enabling are two decisions.

## 7. React to everything it sends (30 sec/day, ongoing)

When it pings you, reply **act**, **noise**, or **later**. That's the entire calibration
loop. Silence teaches it nothing — it's built to treat silence as unknown, never as
"noise." Two weeks of honest reactions and it knows your bar.

**Do not add a second routine for at least three days.** Watch your platform's usage
meter. A routine that fires too often is the most common way these setups fail — the
author's Slack listener burned a full weekly allowance in days. Earn each routine.

## 8. After a week, turn on the audit (2 min)

Stage `/workspace/longhand/routines/memory-audit/job.md` as a weekly routine (Sunday
morning is the shipped default), same replace-`<brain>` step, same birth rows. Its first
run will probably flag something — that's the point. Every flag ends with "confirm or
kill?" and you answer. It proposes; it never resolves a flag alone.

---

## Graduating from minimal

Once minimal has run a week and you've reacted to its pings, open the full
`gmail-weekday-watch/job.md`. It adds watch-feed senders, product-automation filing,
and a promo list — and it has many more placeholders. Read `EXAMPLE-filled.md` first:
it's the full routine filled in for a **fictional** operator so you can see the shape of
real substitutions. Anything that doesn't apply to you, **delete the block** — don't fill
it with a guess. A routine is allowed to be shorter than the template.

## What to add next, in order

quiet-flush (once you set quiet hours) → memory-commit (nightly; the heart of it) →
x-sweep / intelligence-scout (if you watch a timeline) → channel-listener **last, and
paused by default** — read the warning at the top of its file before you ever enable it.

## If something breaks

Open an issue with what the agent did versus what you expected. Failures are wanted —
that's how this gets better. Read `EVIDENCE.md` to see what a real failure looked like
and how it was caught.
