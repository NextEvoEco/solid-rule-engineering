# Example · Separate subtotal calculation from receipt formatting

This example uses Python. The quote flow only needs a numeric subtotal.
Checkout needs that same amount and a formatted receipt. A reporting export
also computes a sum, but it sums settled amounts for a different business purpose.

## Before

```python
def subtotal(prices, *, receipt=False):
    total = sum(prices)
    if receipt:
        return total, f"Receipt subtotal: {total} cents"
    return total


def quote(prices):
    return subtotal(prices)


def checkout(prices):
    return subtotal(prices, receipt=True)


def settled_total(payments):
    return sum(payment["settled_cents"] for payment in payments)
```

The locations below are block-relative line numbers. The inspection covers the
entire example, including every caller. There is no public API outside the
two entry points and reporting export in this example.

| Target | Rule | Status | Evidence and decision |
| --- | --- | --- | --- |
| `subtotal` | SRP-F01 | fail | Lines 2–5 calculate a numeric subtotal and also create customer-facing text. Lines 9 and 13 show that these outcomes have separate consumers. |
| `subtotal` | SRP-F02 | fail | Line 2 changes if subtotal policy changes. Line 4 changes if receipt wording changes. Neither change requires the other. |
| `subtotal` | SRP-F03 | pass | Line 2 uses the input prices and the Python built-in `sum` to calculate the amount. The function uses no external I/O, state, or collaborators for formatting. |
| `subtotal` | SRP-F04 | fail | Lines 9 and 13 select different contracts. Checkout opts into presentation and gets a tuple. The quote gets a number. |
| `subtotal` | SRP-F05 | pass | Searching the example for `sum(` and the total-related symbols finds line 17. Settled payments and quoted prices follow separate policies. Keep the functions separate. |

## After

```python
def subtotal(prices):
    return sum(prices)


def format_subtotal_receipt(total):
    return f"Receipt subtotal: {total} cents"


def quote(prices):
    return subtotal(prices)


def checkout(prices):
    total = subtotal(prices)
    return total, format_subtotal_receipt(total)


def settled_total(payments):
    return sum(payment["settled_cents"] for payment in payments)
```

Checkout coordinates the two operations to return its existing pair. Both
entry points consume the same numeric subtotal. The only changed signature
belongs to the internal helper, and both of its callers are shown.

Example technical checks. Run these assertions with the refactored definitions
in the same Python process.

```python
assert quote([125, 75]) == 200
assert checkout([125, 75]) == (200, "Receipt subtotal: 200 cents")
assert quote([]) == 0
assert checkout([]) == (0, "Receipt subtotal: 0 cents")
assert settled_total([{"settled_cents": 50}]) == 50
```

## Re-evaluation

Mode is refactor. The rules are from pack 0.1.0. Inspect the second code block
for final source locations and use the checks above to verify the caller
contracts. Each cell records the decision and its evidence.

| Target | SRP-F01 | SRP-F02 | SRP-F03 | SRP-F04 | SRP-F05 |
| --- | --- | --- | --- | --- | --- |
| `subtotal` | pass · Lines 1–2 calculate the amount. | pass · Only subtotal policy changes line 2. | pass · Line 2 uses prices and `sum`. | pass · Lines 10 and 14 consume the same numeric result. | pass · Lines 2 and 19 match `sum(`, but the input contracts and change drivers differ. |
| `format_subtotal_receipt` | pass · Lines 5–6 render receipt text. | pass · Receipt wording drives changes at line 6. | pass · Line 6 needs only the amount. | pass · Line 15 consumes the text as receipt output. | pass · Searching for `receipt` and the format string identifies one rendering implementation at line 6. |
| `quote` | pass · Lines 9–10 return the quote amount. | pass · Line 10 delegates subtotal policy. | pass · Line 10 uses the subtotal to form the quote. | pass · The quote assertions exercise the numeric entry-point contract. | pass · Searching for `subtotal(` finds distinct uses at lines 10 and 14. Calculation is already shared. |
| `checkout` | pass · Lines 13–15 produce the checkout result. | pass · The amount and receipt policies are delegated. Only assembly of the checkout result belongs here. | pass · Both delegates supply parts of that result at lines 14–15. | pass · The checkout assertions exercise the amount-and-receipt entry-point contract. | pass · Searching for `subtotal(` and `receipt` identifies the shared calculation and a single presentation call. No shared checkout assembly is warranted. |

The analysis gate is supported by the caller and candidate inventory. The
implementation gate follows from the final responsibility boundaries and
preserved entry-point contracts. The technical gate requires the assertions
to pass. The rule gate follows from the final review of all affected functions.
