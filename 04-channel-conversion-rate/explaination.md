## Channel Conversion Rate — GA4 BigQuery

### Business Problem
Purchase volume alone is misleading. A channel driving 500 purchases
from 100,000 sessions is less efficient than one driving 38 purchases
from 5,000 sessions. Conversion rate normalises for volume and reveals
true channel efficiency.

### Key Finding (January 2021, GA4 Sample Dataset)
| Channel | Sessions | Purchases | Conversion Rate |
|---|---|---|---|
| Other | 43,436 | 560 | 1.29% |
| Direct | 27,222 | 269 | 0.99% |
| Organic | 40,676 | 337 | 0.83% |
| Paid | 5,215 | 38 | 0.73% |

Paid search has the lowest conversion rate despite being the only
channel with direct cost. The Other bucket — containing referral,
email, and affiliate traffic — converts at 1.29%, nearly 2x Paid.
A budget optimisation based on purchase count alone would miss this
entirely.

### Technical Notes
- CTEs separate aggregation logic into named, readable steps
- No GROUP BY in final SELECT — data already aggregated in CTEs
- Division uses 100.0 not 100 to force decimal output in BigQuery
- JOIN on channel matches pre-aggregated rows — one row per channel
  per CTE, so no fan-out risk

### Concepts Demonstrated
CTEs · multi-step aggregation · JOIN on aggregated data ·
integer vs decimal division · conversion rate calculation
