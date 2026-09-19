# gmail-weekday-watch

Three files here. Only ONE is a routine prompt.

| File | What it is | Paste it? | Hash it? |
|---|---|---|---|
| `minimal.md` | **Start here.** The starter routine. Pure prompt, nothing else. One placeholder: `<brain>`. | Yes — this is the routine | Yes — `sha256sum minimal.md \| cut -c1-16` is the roster hash |
| `job.md` | The full routine — watch-feeds, product filing, promo list, many placeholders. Graduate to this after a week on minimal. | Yes, once you've filled it | Yes |
| `EXAMPLE-filled.md` | `job.md` filled in for a **fictional** operator, so you can see the shape of real substitutions. Teaching only. | **No** | **No** |

**Why minimal.md has no header or notes inside it:** the file you hash must be exactly
the file you paste. Any prose inside the prompt file makes the roster hash lie about
what's running — the audit would pass a hash that doesn't match the live routine. So
routine files are pure prompts, and everything explanatory lives here.

**Labels:** minimal.md names two Gmail labels literally — `keeper` and `Purge`. If you
already have labels that mean "keep this" and "delete later," rename those two words in
minimal.md to match your existing labels — don't create duplicates. If you have none,
create `keeper` and `Purge`, either in the Gmail UI (left sidebar → + next to Labels)
or by asking the agent: "create Gmail labels keeper and Purge."

**Angle-bracket convention, everywhere in this repo:** `<brain>` and any token listed
as a placeholder in the file's README you replace before running. Tokens like
`<routine name>` in a *format* line describe what the agent writes at runtime — you
leave those alone. minimal.md avoids the second kind entirely so there's nothing to
second-guess.
