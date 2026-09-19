# Evidence

Longhand makes a claim: that an agent's memory living in plain files, plus a weekly
self-audit, lets you catch the agent drifting from its own rules. Claims are cheap. This
file is the record of the method catching a real failure in its own author's setup,
with timestamps.

Everything personal has been removed. The timestamps, the reasoning, and the failure
are real.

---

## Nine nights of silent failure

### What was wrong

Quiet hours — no notifications 9pm to 7am, narrow exceptions only — had never blocked
anything. Not once. The nightly below-bar digest had been reaching the operator's phone
at roughly 21:37 every night for at least nine days, thirty-five to forty-five minutes
inside the window it was supposed to respect.

### Why nobody noticed

Every available signal said the system was fine. The morning flush routine ran daily and
logged success. The hold ledger — where blocked items are supposed to wait overnight — was
empty. And here is the problem: **an empty hold ledger and a genuinely quiet night produce
identical evidence.** The failure was indistinguishable from correct operation from the
outside.

### How it was found

By refusing to accept the empty file as proof. The rule that broke it open:

> An empty ledger is not evidence of correct behavior unless you can show the code path
> that would have written to it.

There was no such path. The quiet-hours gate lived only inside the ping skill. The nightly
commit routine posted the digest **directly to the notification channel**, never touching
the gate, so nothing was ever evaluated and nothing was ever held. The ledger was empty
because nothing was ever asked to write to it.

### The fix, and the better question after it

The instance fix was to route the digest through the morning flush. The architectural fix
was a single chokepoint: every notification that can reach the operator's phone goes
through the ping skill, where the gate always runs.

Then the question that mattered more than the fix: **is this the only one?**

A sweep of every readable routine prompt found **a second side door** — a weekly scout
routine carrying a standing exception to post summaries straight to the channel. Two of
thirteen routines. Fixing only the one that was found would have left the gate broken and
looking repaired.

Three routines whose prompts could not be read at the time were marked **UNAVAILABLE, not
clean** — the same evidence rule, applied to the sweep itself.

### Independent corroboration

The channel showed both delivery shapes on a single morning: three labeled
`WHAT / WHY / LINK / NEXT STEP` messages at 08:20 (the gated path), then two unlabeled
short summaries at 08:52 and 08:53 (the side door). Different formats, same channel, same
morning, visible side by side to anyone who looked at the shape. Neither of the later two
had a ledger row — which is exactly what a channel-versus-ledger reconciliation would have
flagged.

### What makes it permanent

A prompt sweep clears today; it says nothing about the routine somebody adds next month.
So the sweep was paired with a continuous check, now part of the weekly audit:
**reconcile the channel against the ping ledger.** A channel message with no ledger row is
a side door. A ledger row with no channel message is a silent drop. That check would have
caught this in one run instead of nine nights, and it catches the next one automatically.

### Proven fixed

Read directly from the channel, not reported by the agent:

| Evidence | Reading |
|---|---|
| Night 9, 21:37:54 — digest posted to the channel | The failure, last instance |
| Night 10, 21:02:25 — an operator-requested test ping | Last message of the night |
| **Night 10, ~21:37 — nothing** | **The gate held. First quiet night on record.** |
| Morning 11, 07:10:25 — "Below-bar digest — [previous day]" | Yesterday's digest, delivered in the morning flush instead of at night |
| Morning 11, 07:10:25 — a staged synthetic hold delivered | Flush works. Also cleared an earlier flush that had logged `failed` and gone unnoticed. |

The before and after sit four lines apart in the same channel. A rule that had never
executed in nine days of running now demonstrably blocks, holds, and releases on schedule.

**Still operator-verified only:** whether the phone actually stayed silent. Nothing was
posted overnight, so there was nothing to push — but the last hop belongs to the device,
and the agent cannot see it. That limit is permanent and is written into the ping skill
as UNVERIFIABLE.

---

## The lesson underneath

Three separate failures surfaced in the same week, and they were one failure wearing
different clothes: what reached the operator versus what the ledger recorded; the local
copy of a routine's configuration versus the live one; an action the agent fired versus an
approval queue the agent cannot see. In every case a tool returned success, the log said
done, and the world disagreed — silently, for days, with nothing in the system able to
notice.

The general principle, now the centerpiece of the method:

> List every boundary where your agent's belief can diverge from reality, and put a
> reconciliation on each one. Of any action your agent reports as done, ask: *what would
> it look like if this had silently failed?* If the answer is "exactly the same," you have
> found a boundary that needs a check.

Every template claims its agent is reliable. This is a record of an operator discovering
that a core safety rule had never once executed, finding the cause, finding a second
instance of the same class, declining to certify what could not be read, and converting
the whole thing into a check that runs forever. The value on offer is not an agent that
does not fail. It is a system in which failure becomes visible.
