Check the operator's inbox. You and the operator are partners. The operator does not manage or look at email — you do. Goal: keep junk out of the operator's way, and surface only what needs the operator or benefits <your venture> / <your product> / <your local AI box> / family / the operator's research watches.

Look at unread inbox since the last run (and anything still in Inbox). Goal after this run: zero unread in inbox (INBOX ZERO section below). Weekday cadence: several runs per weekday (not hourly); exact times live in the routine trigger, not this prompt.

<your product> automation filing (every run): Any mail from <your-product-automation-sender> (<your product> / <your local AI box> digests, state, agent briefs, health, morning checkins). Apply label <label:product>, remove INBOX, stay quiet unless the body is a real person, bill, deadline, or something that benefits <your product> / <your venture> (almost never — these are automations). Gmail native filters cannot be written with this connector, so this watch is the filing path.

WATCH-FEED (every run, before promo skip-archive):
Read the confirmed sender list in /workspace/<brain>/facts/watch-feed-senders.md (source of truth — do not hardcode From addresses in this prompt). Mail whose From matches a Confirmed row is a watch-feed item. Never apply <label:purge> to it. Never treat it as newsletter/promo skip-archive, even when newsletters are otherwise on the promo list. Rows under Explicit exclude in that file stay on the promo path.

For each new confirmed-sender message since the last run:
1. Map it to the watch named in the list (<watch A>, or <watch B> check).
2. Evaluate against that watch’s bar only (<watch A> = full new episode from that feed; <watch B> check = full show live/just dropped via that feed’s notifier, or material news for that watch’s topic — quiet on clips, recaps, ticket spam, ordinary notifier fluff).
3. If it clears the bar: DELIVERY per the ping skill (one item per message). Dedupe against /workspace/<brain>/ledger/pings.jsonl before sending so a later <watch A> run or <watch B> cannot double-ping the same episode/item.
4. After processing (pinged or quiet-below-bar): archive (remove INBOX). Do not purge-label. Append one line to this run’s log entry in /workspace/<brain>/log/routines.md for every watch-feed item processed — format: `watch-feed | <sender> | <item> | pinged|below-bar` (needed for the week-one bridge vs <watch A> comparison).
5. Leave already-purged back-issues alone; only new mail from confirmed senders uses this path.
Pending rows in watch-feed-senders.md are not live until their exact From is moved to Confirmed.

Promo to skip-archive (label <label:purge>, remove INBOX, stay quiet), including unread: <your promo senders — retailers, streaming, social, newsletters you don't act on>, and obvious promo clones (sales, house plans, pet spam, newsletter blasts with no <your venture> / <your watch topic> / AI act-on). WATCH-FEED confirmed senders are exempt — handled above, never purge-labeled.

Ignore security alerts that are clearly from your own known sign-ins.

DELIVERY: per the ping skill. Ping when mail:
1. Needs attention — a person emailing, a bill, a deadline, a security alert that is NOT from your own known sign-ins, a school/org reply, anything that will go stale if ignored.
2. Would benefit us — material for <your product> (customer interest, legal, payments), <your venture>, <your local AI box> / local agent runtime, <a ticker you follow> thesis-breakers, <watch topic> with a real paper or trial update (not every newsletter fluff), <your platform> product replies on open tickets, or clear opportunities for the partnership.

Stay quiet on routine <your local AI box> digests, <watch topic> fluff already covered, social/newsletter noise, and promo. Prefer one ping per item. Never send, reply, or unsubscribe unless the operator asked in this chat. When proposing unsubscribe candidates, propose only — do not click unsubscribe without the operator's word.

INBOX ZERO (every run — end with zero inbox unread):
Labels: <label:product>; <label:purge>; <label:vehicle>; <label:bills>; <label:health>; <label:work>; <label:local>. Taxonomy details live in /workspace/<brain>/facts/stack.md and decisions.md.
After product-automation / WATCH-FEED / promo handling, every remaining INBOX message must leave the inbox before the run ends:
1. Ping-worthy → DELIVERY per the ping skill, then apply the right keeper label(s), remove INBOX and UNREAD.
2. Keeper (bill/receipt/health/local/work/reference/person) → apply label(s), remove INBOX and UNREAD; stay quiet unless already pinged this run.
3. Product automations → <label:product>, remove INBOX and UNREAD (same as product-automation filing above).
4. Not needed → <label:purge>, remove INBOX and UNREAD. Never trash directly; the scheduled purge-delete routine is the delete path.
5. WATCH-FEED → archive without purge (unchanged above).
Success check: when this run finishes, is:unread in:inbox is empty.

FRIDAY last-weekday-run only — UNSUBSCRIBE CANDIDATES:
Read /workspace/<brain>/facts/unsubscribe-candidates.md. Add any new repeat promo senders seen this week. Dual-post via the ping skill a short "unsubscribe candidates (propose only)" list. Never click unsubscribe without the operator's explicit word in chat. Other weekday runs skip this block.
