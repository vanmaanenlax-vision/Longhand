# gmail-weekday-watch — MINIMAL (start here)

This is the starter version. Two placeholders. No watch-feeds, no product filing, no
promo brand list — those are in the full `job.md` and you graduate to it once this one
is running and you've reacted to a week of pings.

---

Check the operator's inbox. You and the operator are partners. The operator does not
manage or look at email — you do. Goal: keep junk out of the way, surface only what
needs the operator, and end every run with zero unread in the inbox.

Read `/workspace/<brain>/index.md` then `rules.md` first.

Look at unread inbox since the last run (and anything still in Inbox).

PING (via the ping skill) when mail:
- is a real person writing to the operator,
- is a bill, an invoice, or a payment notice,
- has a deadline or will go stale if ignored,
- is a security alert that is NOT from the operator's own known sign-ins.

STAY QUIET on: promotions, newsletters, social notifications, receipts for things
already known, and automated mail with no action in it.

INBOX ZERO — every remaining INBOX message leaves the inbox before the run ends:
1. Pinged → apply a keeper label, remove INBOX and UNREAD.
2. Keeper (bill / receipt / reference / a person) → apply a keeper label, remove INBOX
   and UNREAD, stay quiet unless already pinged this run.
3. Not needed → apply the `Purge` label, remove INBOX and UNREAD. Never trash directly.
Success check: when this run finishes, `is:unread in:inbox` is empty.

Never send, reply, or unsubscribe unless the operator asked in this chat.

Log one line to `/workspace/<brain>/log/routines.md`:
`- YYYY-MM-DD HH:MM CT | gmail-weekday-watch | <outcome> | pinged|quiet`

---

**Placeholders in this file: `<brain>` only.** The labels are named literally
("keeper", "Purge") — create those two labels in Gmail before the first run, or rename
them here to labels you already have.
