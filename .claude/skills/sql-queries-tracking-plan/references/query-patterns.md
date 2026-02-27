# Firebase Analytics SQL Patterns for Metabase

All patterns query `analytics_prod.native_event` (flat table, no UNNEST).
- Date filter: `{{event_date}}` (Metabase variable)
- Session grouping: `unique_session_id` (not `user_pseudo_id`)

---

## Pattern A — Weekly Event Volume

Use for: tracking event volume over time, averaged per session.

```sql
WITH weekly_data AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    COUNT(DISTINCT unique_session_id) AS nb_sessions,
    COUNTIF(event_name = 'EventName') AS nb_events
  FROM analytics_prod.native_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1
)
SELECT
  semaine,
  nb_sessions,
  nb_events,
  SAFE_DIVIDE(nb_events, nb_sessions) AS ratio_moyen
FROM weekly_data
ORDER BY semaine
```

---

## Pattern B — Multi-Event Session Analysis (Funnel)

Use for: measuring how many sessions include multiple sequential events.

```sql
WITH sessions AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    unique_session_id,
    COUNTIF(event_name = 'EventA') AS has_event_a,
    COUNTIF(event_name = 'EventB') AS has_event_b
  FROM analytics_prod.native_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1, 2
)
SELECT
  semaine,
  COUNT(*) AS nb_sessions_total,
  COUNTIF(has_event_a > 0) AS sessions_avec_event_a,
  COUNTIF(has_event_a > 0 AND has_event_b > 0) AS sessions_conversion,
  SAFE_DIVIDE(
    COUNTIF(has_event_a > 0 AND has_event_b > 0),
    COUNTIF(has_event_a > 0)
  ) AS taux_conversion
FROM sessions
GROUP BY 1
ORDER BY semaine
```

---

## Pattern C — Ratio Between Event Types

Use for: "offers viewed from artist pages divided by artist page visits."

```sql
WITH weekly AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    COUNTIF(event_name = 'EventNumerator') AS nb_numerateur,
    COUNTIF(event_name = 'EventDenominator') AS nb_denominateur
  FROM analytics_prod.native_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1
)
SELECT
  semaine,
  nb_numerateur,
  nb_denominateur,
  SAFE_DIVIDE(nb_numerateur, nb_denominateur) AS ratio
FROM weekly
ORDER BY semaine
```

---

## Pattern D — Normalized Ratio Against Total Interactions

Use for: relative proportion when comparing multiple interaction types.

```sql
WITH weekly AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    COUNTIF(event_name = 'EventA') AS nb_event_a,
    COUNTIF(event_name = 'EventB') AS nb_event_b,
    COUNTIF(event_name IN ('EventA', 'EventB')) AS nb_total
  FROM analytics_prod.native_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1
)
SELECT
  semaine,
  SAFE_DIVIDE(nb_event_a, nb_total) AS part_event_a,
  SAFE_DIVIDE(nb_event_b, nb_total) AS part_event_b
FROM weekly
ORDER BY semaine
```

---

## Pattern E — Parameter Distribution Breakdown

Use for: revealing composition of event origins or categorical attributes.

```sql
SELECT
  DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
  from AS source,
  COUNT(*) AS nb_occurrences,
  SAFE_DIVIDE(COUNT(*), SUM(COUNT(*)) OVER (PARTITION BY DATE_TRUNC(event_date, WEEK(MONDAY)))) AS part
FROM analytics_prod.native_event
WHERE event_name = 'EventName'
  AND event_date = {{event_date}}
  AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
GROUP BY 1, 2
ORDER BY semaine, nb_occurrences DESC
```

---

## Pattern F — Video Analytics

Use for: video completion rates and combined video + event metrics.

```sql
WITH video_stats AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    COUNT(DISTINCT unique_session_id) AS sessions_video,
    AVG(SAFE_DIVIDE(seen_duration, video_length)) AS taux_completion_moyen
  FROM int_firebase_prod.native_video_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1
),
offer_stats AS (
  SELECT
    DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
    COUNTIF(event_name = 'ConsultOffer') AS nb_consult
  FROM analytics_prod.native_event
  WHERE event_date = {{event_date}}
    AND DATE_TRUNC(event_date, WEEK(MONDAY)) < DATE_TRUNC(CURRENT_DATE(), WEEK(MONDAY))
  GROUP BY 1
)
SELECT
  v.semaine,
  v.sessions_video,
  v.taux_completion_moyen,
  o.nb_consult
FROM video_stats v
LEFT JOIN offer_stats o USING (semaine)
ORDER BY semaine
```
