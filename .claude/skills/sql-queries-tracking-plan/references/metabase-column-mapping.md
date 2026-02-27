# Metabase Tables and Columns Guide

## Key Tables

### `analytics_prod.native_event` — Primary table
Flat table containing all Firebase events. **Pas de UNNEST nécessaire : les paramètres sont déjà des colonnes.**

**Standard columns:**
| Column | Firebase Parameter | Description |
|--------|-------------------|-------------|
| `event_name` | event_name | Event identifier |
| `event_date` | event_date | Date of the event |
| `event_timestamp` | event_timestamp | Timestamp in microseconds |
| `unique_session_id` | unique_session_id | Session grouping key (use this, NOT user_pseudo_id) |
| `user_id` | user_id | Authenticated user ID |
| `platform` | platform | iOS / Android |
| `offer_id` | offerId | Offer identifier |
| `category_name` | categoryName | Offer category |
| `reaction_type` | reactionType | User reaction |
| `module_name` | moduleName | Home module name |
| `module_id` | moduleId | Home module ID |
| `module_type` | moduleType | Type of module |
| `search_id` | searchId | Search session ID |
| `from` | from | Navigation source |
| `venue_id` | venueId | Venue identifier |
| `booking_id` | bookingId | Booking identifier |

**Missing parameters (not available as columns):**
- `artistId`
- `artistName`
- `videoId`
- `state`

### `int_firebase_prod.native_video_event` — Video analytics table
Specialized table for video analytics with pre-calculated columns:
- `seen_duration` — Duration viewed
- `video_length` — Total video length
- `completion_rate` — Percentage viewed

## Critical Guidelines

- Always use flat tables — unnesting is unnecessary
- Apply date filters using the Metabase variable `{{event_date}}` (not start/end date parameters)
- Use `unique_session_id` for session grouping, NOT `user_pseudo_id`

## Use Cases

| Use Case | Table |
|----------|-------|
| Standard event analysis (conversions, funnels) | `analytics_prod.native_event` |
| Video performance analysis | `int_firebase_prod.native_video_event` |

## SQL Examples

**Basic event count:**
```sql
SELECT
  DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
  COUNT(*) AS nb_events
FROM analytics_prod.native_event
WHERE event_name = 'ConsultOffer'
  AND event_date = {{event_date}}
GROUP BY 1
ORDER BY 1
```

**Multi-event session analysis:**
```sql
SELECT
  DATE_TRUNC(event_date, WEEK(MONDAY)) AS semaine,
  COUNT(DISTINCT unique_session_id) AS nb_sessions,
  COUNTIF(event_name = 'ConsultOffer') AS nb_consult,
  COUNTIF(event_name = 'BookingConfirmation') AS nb_booking
FROM analytics_prod.native_event
WHERE event_date = {{event_date}}
GROUP BY 1
```
