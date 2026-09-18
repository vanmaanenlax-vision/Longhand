# Watch-feed senders (EXAMPLE TEMPLATE)

Ship empty or with fake rows only. Never copy a live sender list into a public template.

Prompts should **cite this file** as the source of truth — do not hardcode From addresses in routine text.

## Format
| From | Maps to watch | Status |
|---|---|---|
| `user@domain` | `<watch name>` | Confirmed / Pending / Exclude |

## Example (fake — replace or delete)
| From | Maps to watch | Status |
|---|---|---|
| `example@newsletter.example` | `<watch A>` | Confirmed |

## Rules
- Confirmed senders: treat as watch-feed items (not promo purge).
- Pending: not live until moved to Confirmed after a real delivery.
- Exclude: stay on the promo / skip-archive path.
