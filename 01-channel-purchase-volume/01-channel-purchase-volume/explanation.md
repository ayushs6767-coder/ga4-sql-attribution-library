## Channel Purchase Volume — GA4 BigQuery

### Business Problem
GA4's standard reports are sampled above 500K sessions.
This query bypasses the UI and pulls raw, unsampled event data
directly from BigQuery export tables.

### Key Technical Decision
Used _TABLE_SUFFIX instead of event_date for partition pruning.
This reduces bytes scanned from full table to January partitions only.
On a client account with 3 years of data, this is the difference
between a $0 query and a $4 query — at scale, that compounds.

### What This Finds
The exact purchase count per acquisition channel for any date range,
unsampled, directly from raw GA4 event logs.
