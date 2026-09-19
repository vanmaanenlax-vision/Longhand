# Watch-feed senders

Source of truth for which senders are watch-feed items (never promo-archived). Routines
read this file; never hardcode addresses in a prompt.

**Ship empty or with fake rows only. Never copy a live sender list into a public template.**

Rows are **Pending** until you move the exact From address to **Confirmed** yourself.
Nothing here is live until it says Confirmed.

| From | Watch | Status |
|---|---|---|
| example@newsletter.example | <watch A> | Pending |

## Explicit exclude
(senders that look like watch-feeds but stay on the promo path)
