# BigQuery Firebase Analytics Export Schema

## Table Structure

Firebase exports events in daily-sharded tables using the naming convention `projet.dataset.events_YYYYMMDD`.

**Critical rule:** Always use `_TABLE_SUFFIX` to filter dates on wildcard tables — this is the only way to enable partition pruning.

## Core Columns

| Column | Type | Description |
|--------|------|-------------|
| `event_timestamp` | INTEGER | Microseconds since epoch |
| `event_name` | STRING | Event identifier |
| `user_pseudo_id` | STRING | Device-based identifier |
| `event_params` | ARRAY<STRUCT> | Event parameters (key-value pairs) |
| `user_properties` | ARRAY<STRUCT> | User-level properties |
| `device` | STRUCT | Device info (platform, model, etc.) |
| `geo` | STRUCT | Geographic data |

## Parameter Extraction Strategy

Event parameters are stored as arrays of structs with varying value types. The optimal approach uses a single `UNNEST` operation combined with `MAX(IF())` pivoting to extract multiple parameters efficiently.

**Preferred pattern:**
```sql
SELECT
  event_name,
  MAX(IF(ep.key = 'param_name', ep.value.string_value, NULL)) AS param_name
FROM `projet.dataset.events_*`,
UNNEST(event_params) AS ep
WHERE _TABLE_SUFFIX BETWEEN '20240101' AND '20240131'
GROUP BY event_name
```

## Performance Best Practices

**Costly antipatterns to avoid:**
- Omitting `_TABLE_SUFFIX` filters → scans all historical tables
- Multiple `UNNEST` operations on identical arrays → duplicate processing
- `COUNT(DISTINCT)` on large datasets → use `APPROX_COUNT_DISTINCT` instead
- Unfiltered JOINs → require complete table scans

## Partition Optimization

For wildcard tables, filter using:
```sql
WHERE _TABLE_SUFFIX BETWEEN '20240101' AND '20240131'
```

**Do NOT** use `event_date` filtering with wildcard syntax — it doesn't trigger partition pruning.
