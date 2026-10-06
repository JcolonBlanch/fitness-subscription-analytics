# TripleTen Submission Audit

Audit date: October 6, 2026

## Rubric compliance

| Requirement | Status | Verification |
|---|---|---|
| Import the supplied Excel workbook | Pass | Original workbook is included unchanged in `data/`. |
| `Transaction_Date` formatted as a date | Pass | Tableau recognizes the field as a date. |
| Relate `customers` and `transactions` on `Customer_ID` | Pass | Relationship is present and documented in `screenshots/data_model.png`. |
| Page named `Customer Cohort` | Pass | Tableau worksheet uses the exact required name. |
| Cohorts based on subscription-start month | Pass | `First Purchase Date` uses the first transaction where `Transaction Type = "Subscription"`. |
| Cohort retention matrix | Pass | Tableau contains 24 discrete monthly cohort rows, 25 months-since-first-purchase columns, and visible percentage labels based only on `Retention Rate`. |
| Conditional color scale | Pass | Explicit `Retention Rate` calculation drives the heatmap color scale. |
| Page named `Revenue Forecast` | Pass | Tableau worksheet uses the exact required name. |
| Monthly subscription revenue | Pass | Revenue is filtered to `Subscription` and displayed by continuous month. |
| Forecast length: 12 months | Pass | Tableau forecast is configured for the next 12 months. |
| Seasonality: 12 | Pass | Monthly forecast uses annual (12-month) seasonality. |
| Confidence interval: 95% | Pass | Prediction intervals are enabled at 95%. |
| Ignore last: 0 | Pass | Forecast options explicitly include the full final period. |
| Page named `CAC vs LTV` | Pass | Tableau worksheet uses the required name. |
| Cumulative LTV line chart | Pass | Revenue uses a running-total table calculation over months since first purchase. |
| Total CAC measure | Pass | Customer-level CAC is deduplicated, then summed by cohort year with an LOD calculation. |
| CAC constant lines | Pass | Total CAC is plotted as horizontal cohort-specific lines on the dual-axis chart. |
| CAC and cumulative revenue use the same scale | Pass | The Tableau packaged workbook stores the secondary-axis encoding with `synchronized="true"`. |
| 2024/2025 cohort filter | Pass | Both years are selected and the interactive filter is displayed on the worksheet. |
| Break-even identified | Pass | 2024 reaches break-even in month 4; 2025 reaches break-even in month 6. |
| README answers all three business questions | Pass | Cohort timing, forecast amount/seasonality, and both CAC payback periods are documented. |
| Required data and screenshot filenames | Pass | All required files are present with exact names, and every screenshot was captured directly from the corresponding final Tableau worksheet. |
| Tableau workbook in repository | Pass | Published workbook is included as `FitnessHub_Subscription_Analytics.twbx`; the live Tableau Public report is linked in `README.md`. |
| Public GitHub repository with exact name | Pass | Public repository is available at `https://github.com/JcolonBlanch/fitness-subscription-analytics`. |
| TripleTen submission | Pass | Repository URL was submitted successfully; TripleTen shows `Project has been submitted` and `Review in progress`. |

## Verified figures

- Customers: 9,300
- Transactions: 64,979
- Subscription transactions: 51,982
- Historical subscription revenue: $2,006,148
- Independent 12-month forecast check: approximately $2.05 million
- 2024 total CAC: $501,536.80; break-even month 4
- 2025 total CAC: $1,162,459.11; break-even month 6
- Subscription retention: 100% at month 0, approximately 85% at month 1, 78% at month 2, and 50% at month 3 across monthly cohorts

## Final submission status

All analytical, file-structure, publication, repository, and submission requirements have been completed and verified against the live TripleTen rubric.
