# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a delivery quote
in USD. Zones are `local` and `regional`; weights must be positive.

| Service    | Base (local) | Base (regional) | Per-kg | Express surcharge |
|------------|-------------|-----------------|--------|-------------------|
| `standard` | $5.00       | $8.00           | $1.50  | —                 |
| `express`  | $5.00       | $8.00           | $1.50  | +$7.00 flat       |

Passing an unrecognised zone or service raises `ValueError`.

### CLI

```
python -m warehouse.cli <weight_kg> <zone> [--service {standard,express}]
```

Examples:

```bash
# Standard quote – 3 kg, local zone
python -m warehouse.cli 3 local
# $9.50

# Express quote – 3 kg, regional zone
python -m warehouse.cli 3 regional --service express
# $22.50
```
