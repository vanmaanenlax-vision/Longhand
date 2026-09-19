# EXAMPLE — the full gmail-weekday-watch, filled in for a FICTIONAL operator

**This operator does not exist.** "Sam" runs an imaginary bakery. Every sender, label,
and topic here is invented so you can see the SHAPE of real substitutions without
copying anyone's actual data. Do not use these values — replace with your own.

| Placeholder | Sam's value (fictional) | What it actually is |
|---|---|---|
| `<brain>` | `brain` | folder name → paths become `/workspace/brain/...` |
| `<your venture>` | Sam's Sourdough | the operator's business |
| `<your product>` | the online order form | the live product |
| `<your-product-automation-sender>` | `orders@samssourdough.example` | the automated mail from the product |
| `<label:product>` | `Orders` | Gmail label for product automation |
| `<label:purge>` | `Purge Q4` | Gmail label for the delete-later pile |
| `<label:bills>` | `Bills` | bills and invoices |
| `<label:vehicle>` | `Van` | the delivery van's loan/insurance mail |
| `<label:health>` | `Health` | medical/insurance mail |
| `<label:work>` | `Bakery` | the business |
| `<label:local>` | `Local` | town, school, community |
| `<watch A>` | `Flour Weekly` | a supplier newsletter Sam actually reads |
| `<watch B>` | `Market Report` | a farmers-market bulletin |
| `<your promo senders — …>` | `Wholesale Depot, Coupon Barn, Streamflix, LinkedIn` | senders Sam never acts on |
| `<your-channel>` | `#sam-alerts` | the one Slack channel Sam watches (or delete Slack refs) |
| `<a ticker you follow>` | `(none)` — block deleted | Sam has no investments to watch |

So, filled in, the product-automation line becomes:

> Any mail from `orders@samssourdough.example` (order confirmations, form submissions):
> apply label `Orders`, remove INBOX, stay quiet unless the body is a real person, a
> bill, or a deadline.

And the INBOX ZERO label list becomes:

> Labels: `Orders`; `Purge Q4`; `Van`; `Bills`; `Health`; `Bakery`; `Local`.

Notice what Sam did with things that don't apply: **deleted the block**, didn't fill it
with a guess. No ticker, no product-automation block beyond orders. A routine is allowed
to be shorter than the template.
