# sisyphus-test-targets

Deterministic test datasets and their validation contracts for the Sisyphus test-recovery pipeline.

## Repository layout

```
sisyphus-test-targets/
├── README.md
├── targets/          # Raw input datasets (JSON arrays)
├── schemas/          # JSON Schema files describing each dataset
└── expectations/     # Pre-computed aggregate results used for QC
```

## Datasets

### `testvr_web_recovery_array_v1`

| File | Purpose |
|------|---------|
| `targets/testvr_web_recovery_array_v1.json` | Six integer-based transaction records |
| `schemas/testvr_web_recovery_array_v1.schema.json` | JSON Schema (draft 2020-12) for the target array |
| `expectations/testvr_web_recovery_array_v1.expected.json` | Expected aggregates: record count, quantity total, extended value, and per-category totals |

All monetary values are stored in **cents** (integers) to eliminate floating-point ambiguity.

### Validation contract

A conforming consumer must:

1. **Recover** the target file independently (not copy the expectation file).
2. **Parse** the JSON array and validate each record against the schema.
3. **Calculate** the following aggregates:
   - `record_count` — total number of records
   - `quantity_total` — sum of all `quantity` fields
   - `extended_value_cents` — sum of `quantity × unit_price_cents` for every record
   - `category_totals_cents` — sum of `extended_value_cents` grouped by `category`
4. **QC** the results against `expectations/testvr_web_recovery_array_v1.expected.json` and report any discrepancy as a failure.
