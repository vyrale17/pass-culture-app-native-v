---
name: sql-queries-tracking-plan
description: Generate optimized SQL queries for Metabase from Pass Culture Firebase Analytics tracking plans.
---

# SQL Queries from Tracking Plan

This skill guides generating optimized SQL queries for Metabase from Pass Culture Firebase Analytics tracking plans. It's triggered by requests to query Firebase/BigQuery data, analyze tracking events, or build analytics dashboards.

## Core Collaboration Rules
- **No guessing** — Consult references or ask clarifying questions rather than assume column/event names
- **Interactive approach** — Ask targeted questions when needs are ambiguous before generating queries
- **Expert coaching** — Challenge metrics themselves and signal interpretation limitations

## Production Standards
Five mandatory practices anchor all queries:

1. Always query `analytics_prod.native_event` (flat table, no UNNEST)
2. Use `{{event_date}}` as the single Metabase date filter variable
3. Reference `unique_session_id` for session grouping (not `user_pseudo_id`)
4. Apply `COUNTIF` for multi-event session analysis within one scan
5. Use `DATE_TRUNC(event_date, WEEK(MONDAY))` for weekly aggregations, excluding incomplete weeks

## Implementation Workflow

**Step 1:** Verify available columns in `references/metabase-column-mapping.md`

**Step 2:** Identify event names and metric type (count, ratio, funnel, distribution, time series)

**Step 3:** Select pattern from `references/query-patterns.md` (6 validated templates covering volume, funnels, ratios, breakdowns, and video analysis)

**Step 4:** Generate annotated query using CTEs with French column names where appropriate

## Reference Files

- `references/metabase-column-mapping.md` — Column and table mappings for Metabase
- `references/query-patterns.md` — Six production-validated query patterns with examples
- `references/bigquery-schema.md` — Raw Firebase schema for unavailable parameters
