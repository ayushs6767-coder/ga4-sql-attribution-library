## Source + Medium Purchase Breakdown — GA4 BigQuery

### Business Problem
GA4's default acquisition report groups traffic by source only.
This collapses paid and organic Google traffic into one "google" row —
hiding the performance difference between them.

This query splits source and medium together, exposing the true
channel breakdown behind every purchase event.

### Key Finding (January 2021, GA4 Sample Dataset)
- google / organic: 310 purchases
- (direct) / (none): 269 purchases
- shop.googlemerchandisestore.com / referral: 165 purchases

Google organic outperformed every paid channel.
A marketer reading only the source report would never see this split.

### Technical Notes
- GROUP BY on two columns simultaneously: source and medium
- _TABLE_SUFFIX partition pruning: 38.56 MB scanned vs full table scan
- COUNT(*) counts rows — each row in events_* is one event
- Explicit column names in GROUP BY preferred over positional (1, 2)
  for production readability

### Concepts Demonstrated
GROUP BY · COUNT(*) · _TABLE_SUFFIX partition pruning · multi-column aggregation
