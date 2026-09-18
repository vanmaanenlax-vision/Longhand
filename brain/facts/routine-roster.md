# Expected routine roster (EXAMPLE TEMPLATE)

Authority file for Sunday memory-audit drift detection. The operator owns changes. Update this file in the **same action** as any routine create / enable / disable / pause / prompt change.

## Format
| folder | name | expected | prompt_hash | schedule/trigger | notes |
|---|---|---|---|---|---|
| `slug` | display name | enabled / paused | `<hash or MANUALLY-SYNCED>` | cron or event | short note |

## Example (fake — replace or delete)
| folder | name | expected | prompt_hash | schedule/trigger | notes |
|---|---|---|---|---|---|
| `example-watch` | Example watch | enabled | `EXAMPLEONLY` | `0 9 * * 1-5` | EXAMPLE ONLY — not a real routine |
