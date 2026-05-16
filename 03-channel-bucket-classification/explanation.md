## Channel Bucket Classification — GA4 BigQuery

### Business Problem
Raw GA4 data returns dozens of source/medium combinations.
Marketers don't need 9 rows — they need four buckets:
Paid, Organic, Direct, Other.

This query uses CASE WHEN to classify every purchase event
into a business-meaningful channel before aggregating.

### Key Finding (January 2021, GA4 Sample Dataset)
| Channel | Purchases |
|---|---|
| Other | 560 |
| Organic | 337 |
| Direct | 269 |
| Paid | 38 |

Other is the largest bucket — indicating significant attribution
gaps in GA4's source/medium tracking. Referral, email, and
affiliate traffic are not classified by this model and require
a more granular CASE WHEN expansion.

### Technical Notes
- CASE WHEN evaluated top to bottom — order of conditions matters
- medium = 'cpc' checked before source = '(direct)' intentionally
- GROUP BY channel references the alias directly — valid in BigQuery
- Dimensions (channel) listed before metrics (total_purchases) in SELECT

### Concepts Demonstrated
CASE WHEN · conditional classification · alias reference in GROUP BY
