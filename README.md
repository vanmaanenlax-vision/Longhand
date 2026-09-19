# Longhand

**A governed agent operating system — by VMV.**

My agent had a rule that was supposed to keep it from waking me at night. It never ran —
not once, for nine days — and every signal said it was working. This is the system I
built so that can't happen silently again. [Read the evidence.](EVIDENCE.md)

A file-first memory store, skill contracts, and a weekly self-audit for a chief-of-staff
agent. Built and run for weeks on a $30 plan. **New here? Start with [QUICKSTART.md](QUICKSTART.md)
— fifteen minutes to a running routine.**

Longhand means written out in full — nothing abbreviated, nothing compressed into
shorthand only the writer can read. That is the whole argument. Your agent's memory lives
in plain files you can open, diff, and audit, instead of inside a vendor's black box you
have to take on faith.

This is not a prompt. It is an operating system for one agent: a memory store you can
read, a set of laws the agent cites instead of restating, routines that log their own
birth, and an audit that catches the agent drifting from its own configuration. It was
built by one founder to take over the noise from his phone, and it has been running his
email triage, timeline monitoring, calendar, and watch items continuously since early
September 2026.

Install it, point it at your own life, and you get the architecture. The judgment is yours
to build — this README tells you how.

**Install the ready-made bot:** <TEMPLATE LINK — add after the Share-as-Template dry-run>
Or build it from the files in this repo.

---

## The one idea

**Files win. Bot memory is a cache.**

Every agent platform offers some form of built-in memory. All of them are opaque: you
cannot diff them, you cannot audit them, you cannot tell whether what the agent believes
today is what you told it last week. When it drifts, you find out by being wrong.

So the source of truth lives in plain markdown files the agent reads and writes, and the
platform's own memory is treated as a convenience that may be stale at any moment. If the
files and the agent disagree, the files are right and the agent gets corrected.

Everything else in this template follows from that one commitment.

---

## What you get

```
brain/
  index.md              entry point — what everything is and where it lives
  rules.md              the laws, stated once
  decisions.md          append-only. every consequential change, dated, with why
  facts/                durable state: rosters, watch lists, confirmed senders
  log/                  daily activity, routine outcomes
  ledger/               structured records the agent appends to, one JSON object per line
  learning/             lessons, open questions, standing patterns, calibration notes
  snapshots/            point-in-time copies for diffing
```

**Skill contracts.** Each capability is defined by a contract with six fields: *when* it
fires, *inputs* it needs, *steps* it takes, how it *validates* its own output, what it
*returns*, and **what needs approval**. That last field is the one most setups skip, and
it is the one that makes the rest safe.

**Prompts cite, they do not restate.** A routine's prompt says "follow the ping contract."
It does not paraphrase the ping contract. Restating a rule in five places means five
places to drift. This is the single highest-leverage anti-drift move in the template.

**A roster with hashes.** `facts/routine-roster.md` records every routine, its enabled
state, and a hash of its prompt. A weekly audit diffs the roster against what is actually
running. When they disagree, something changed without being recorded — which is exactly
the failure that is otherwise invisible.

---

## The laws

These are the rules the agent cites. Adapt the specifics; keep the shape.

**Every routine's birth gets a decisions row.** If it exists and is not in the log, it
does not exist. This is what makes the roster diff meaningful.

**Roster updates happen in the same action as the change.** Not "later," not "at the next
audit." An agent that disables a routine and updates the roster tomorrow has a window
where its own audit will lie to it.

**Silence is unknown, not clean.** A quiet channel means the agent did not report, which
is a different fact from nothing happening. Never let absence of output read as absence of
events.

**Notifications go to two places.** The agent's native chat and one channel you actually
watch. If one path breaks you find out, because the other one didn't.

**Quiet hours are real, with named exceptions.** Nothing between 9pm and 7am except a
short, explicit list — family, security, same-day deadlines. Everything else queues and
flushes in the morning. An assistant that wakes you at 2am for a newsletter gets turned
off within a week, and then it does nothing at all.

**Nothing external goes out without a human word.** No email sends, no deploys, no
purchases. The agent drafts and proposes; you approve. This is not timidity — it is what
makes it safe to let the rest run unsupervised.

**Substantiated change updates every linked piece in one pass. Rumor stays watch-only.**
When a date moves and it is confirmed first-party, the calendar entry, the reminder, and
the roster all move together. When it is a rumor, nothing moves.

**Pre-decide platform features before they activate.** When your vendor announces
something — a new memory system, voice, a marketplace — write down what you will do about
it *before* it lands. Features that arrive undecided get adopted by accident.

---

## Calibration: the part that actually makes it useful

An agent that surfaces everything is a worse inbox. The template ships a three-word
feedback loop: reply **act**, **noise**, or **later** to anything it sends you.

Those replies accumulate. The agent learns which topics clear the bar, which get filed to
a digest, and which should never have been raised. A below-bar digest batches the rejects
once a day so you can catch a miscalibration without reading each one live.

Budget two weeks of honest reactions. The system is only as good as this loop, and it is
the one part nobody else can do for you.

---

## The scaffolding

The packager ships instructions, skills, and routine triggers. It does not reliably carry
the files — and the files are the point. Build them first. It takes five minutes and
everything else assumes they exist.

```
mkdir -p brain/{facts,log,ledger,learning,snapshots}
touch brain/{index.md,rules.md,decisions.md}
touch brain/facts/routine-roster.md
touch brain/learning/{lessons.md,questions.md}
touch brain/ledger/pings.jsonl
```

**`brain/index.md`** — the entry point. The agent reads this first, every time.

```markdown
# Index

This directory is the source of truth. If you and these files disagree, the files
are right and you are stale. Re-read before acting on anything you "remember."

- rules.md          The laws. Cite them; never restate them.
- decisions.md      Append-only. Every consequential change, dated, with why.
- facts/            Durable state. Rosters, watch lists, confirmed senders.
- log/              Daily activity and routine outcomes.
- ledger/           Structured records, one JSON object per line.
- learning/         Lessons, open questions, standing patterns.
- snapshots/        Point-in-time copies, for diffing.
```

**`brain/rules.md`** — your laws, in your words. This is the starting set; edit it.

```markdown
# Rules

1. Files win. Platform memory is a cache and may be stale.
2. Every routine's birth gets a decisions.md row. If it is not logged, it does not exist.
3. Roster updates happen in the SAME action as the change. Never "later."
4. Silence is unknown, not clean. Absence of output is not absence of events.
5. Notifications go to two places: native chat and one channel the operator watches.
6. Quiet hours 9pm-7am. Exceptions: family, security, same-day deadlines. Nothing else.
7. Nothing external sends without an explicit human word. Draft and propose; never send.
8. Substantiated change updates every linked piece in one pass. Rumor stays watch-only.
9. Pre-decide platform features before they activate.
10. When unsure whether something clears the bar, file it below-bar and let the digest
    surface it. Do not interrupt on a guess.
11. One decision per decisions.md row. Bundling two changes in one row hides the one
    you never justified.
12. When a later row narrows an earlier rule, mark the earlier one
    superseded-by <date>. Two active rows saying different things is a coin flip.
13. Never suppress a drift finding to make an audit pass. Fix it, or let it fail
    loudly until it is fixed.
14. Absent verification never renders as passed verification. An audit that cannot
    check something says so. A stale copy that matches itself is a false pass, and a
    false pass is worse than an honest failure.
```

**`brain/decisions.md`** — append-only. Never edit a past row; add a correcting one.

```markdown
# Decisions

| Date | Change | Why | Reversible? |
|---|---|---|---|
| 2026-01-15 | Enabled weekday email watch, 4x/day | Inbox triage is the first real job | Yes - disable in settings |
```

**`brain/facts/routine-roster.md`** — what the weekly audit diffs against.

```markdown
# Routine roster

| Routine | Enabled | Schedule | Prompt hash | Decisions row |
|---|---|---|---|---|
| weekday-email-watch | yes | 8:00,12:00,16:00,20:00 | a3f1c9 | 2026-01-15 |
```

A routine running but absent here, or present here but not running, is drift. That is the
finding the audit exists to produce.

**`brain/ledger/pings.jsonl`** — one object per line, appended, never rewritten.

```json
{"ts":"2026-01-15T08:04:00Z","topic":"email","subject":"vendor contract renewal","bar":"act","reaction":null}
```

Leave `reaction` null until the operator replies act, noise, or later. Those reactions are
the calibration data; without them the agent never learns your bar.

**Skill contract template** — every capability gets one of these, in the skill itself.

```markdown
## Contract: <name>
WHEN:     the exact condition that fires this
INPUTS:   what it needs, and where it reads each one from
STEPS:    numbered, in order, no improvisation
VALIDATE: how it checks its own output before returning
RETURN:   the exact shape it hands back
APPROVAL: what it must NOT do without an explicit human word
```

The APPROVAL line is the one people skip. It is the one that makes the rest safe to run
unattended.

---

## Setting it up

**First hour.** Build the scaffolding above, then edit `rules.md` until the laws are yours
rather than mine. Then one routine only: a weekday email watch. Nothing else. Let it run for two
days and react to everything it sends.

**First week.** Add routines one at a time, each with a decisions row. Turn on quiet hours
before you add anything that fires more than twice a day. Do not enable a real-time
listener until you understand your plan's usage budget — a channel listener that wakes on
every message, including the agent's own posts, will consume a weekly allowance in days.
This is the most common way a setup like this fails.

**First month.** Turn on the weekly audit. Let it find its first drift. That moment — the
audit catching something you did and forgot to record — is when the method starts paying
for itself.

---

## Honest limits

**This is single-operator.** One person gives it work, one person sees its output, one
person approves. It has no concept of a team.

**It runs on a budget you can exhaust.** Every routine costs. The roster is not just an
audit artifact, it is a cost ledger. Adding a tenth routine is a real decision.

**Your platform can break the files underneath you.** During this template's own
development, the local mirror of routine definitions silently stopped being written for
newly created routines — the control plane had them, the disk did not — which left three
routines live but unverifiable. An audit can only check what is written down. When the
platform stops writing, the correct response is a failing audit, not a suppression flag —
and watch for the subtler version: files that still exist but stopped updating will hash
cleanly against themselves and report green. Check freshness, not just presence.

**Verification is on you.** The agent reports what it did. Those reports are claims, and
claims need checking against something the agent does not control — the calendar entry
itself, the raw file lines, the actual channel. During this template's own development, a
self-report checked out on substance but misdescribed sequence. That is the normal case,
not the alarming one, and it is why the audit exists.

**Verify the write path, not the artifact.** This is the failure that will cost you most,
because it looks like success. An empty hold ledger reads as a quiet night when it may
mean nothing was ever evaluated. A local file that hashes clean may be a copy comparing
itself to itself. A calendar entry that looks right may have been set by the action you
are about to credit to something else. In each case the artifact is fine and the process
behind it was never running. Before you accept an artifact as evidence, make the agent
show you the code path that would have written to it — and if no path exists, you have
found a side door, not a clean result.

The general form of the fix is worth stating plainly, because it is the most useful idea
in this whole template: **list every boundary where your agent's belief can diverge from
reality, and put a reconciliation on each one.** An agent only knows what a tool call
returned. Everywhere that return value can be true while the world disagrees is a place
where the log will drift from what actually happened, silently, for as long as nobody
looks. In this system there turned out to be three: what reached the operator versus what
the ledger recorded, the local copy of a configuration versus the live one, and an action
the agent fired versus an approval queue the agent cannot see. Each one had gone
undetected for days. Each needed the same treatment.

Find yours before they find you. The question to ask of any action your agent reports as
done: *what would it look like if this had silently failed?* If the answer is "exactly the
same," you have found a boundary that needs a reconciliation.

The concrete technique for the first of them: **reconcile the channel against the
ledger.** Every message that reached you should have a matching ledger row, and every row
should have a matching message. An entry in one without the other is a side door or a
silent drop. Double-entry bookkeeping, applied to your own notifications.

**A filed rule is not a live rule.** An agent that says it has learned a pattern has, at
that moment, only written a sentence. The only proof is a case nobody pointed at, handled
correctly, unprompted. Test yours.

**It does not replace your judgment.** It removes the cost of noticing. What to do about
what it notices is still your job, and the setups that forget this become a second inbox.

---

## What was removed

This template ships with all personal content stripped: contacts, senders, family
references, financial and health items, addresses, product internals, and every watch item
specific to its author. The routines are included as **patterns with example topics**, not
as working watches, and the two data files a routine reads — the confirmed-sender list and
the unsubscribe-candidates list — ship empty, with one clearly-fake example row each. You
will replace the topics and the example rows with your own; the contracts, laws, and audit
structure are the part worth keeping.

If you find anything personal that survived the scrub, say so and it will be removed.

---

*Longhand is free to use, modify, and republish. Built by VMV. If it saves you an hour a
week, that is the whole return being asked for.*
