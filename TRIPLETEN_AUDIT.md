# TripleTen Submission Audit

Audit date: October 5, 2026

## Rubric compliance

| Requirement | Status | Verification |
|---|---|---|
| Import the supplied Excel workbook | Pass | Original workbook is included unchanged in `data/`. |
| `Transaction_Date` formatted as a date | Pass | Tableau recognizes the field as a date. |
| Relate `customers` and `transactions` on `Customer_ID` | Pass | Relationship is present and documented in `screenshots/data_model.png`. |
| Page named `Customer Cohort` | Pass | Tableau worksheet uses the exact required name. |
| Cohorts based on subscription-start month | Pass | `First Purchase Date` uses the first transaction where `Transaction Type = "Subscription"`. |
| Cohort retention matrix | Pass | Month cohort rows, months-since-first-purchase columns, and distinct active customers are present. |
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
| 2024/2025 cohort filter | Pass | Both years are selected and the interactive filter is displayed on the worksheet. |
| Break-even identified | Pass | 2024 reaches break-even in month 4; 2025 reaches break-even in month 6. |
| README answers all three business questions | Pass | Cohort timing, forecast amount/seasonality, and both CAC payback periods are documented. |
| Required data and screenshot filenames | Pass | All required files are present with exact names. |
| Tableau workbook in repository | Pending publish | Workbook is complete in Tableau Public Desktop; the packaged/public workbook must be added after publishing. |
| Public GitHub repository with exact name | Pending publish | Must be created as `fitness-subscription-analytics`. |
| TripleTen submission | Pending confirmation | Submit only after the public repository URL is verified. |

## Verified figures

- Customers: 9,300
- Transactions: 64,979
- Subscription transactions: 51,982
- Historical subscription revenue: $2,006,148
- Independent 12-month forecast check: approximately $2.05 million
- 2024 total CAC: $501,536.80; break-even month 4
- 2025 total CAC: $1,162,459.11; break-even month 6
- Subscription retention: 100.00% at month 0, 84.99% at month 1, 71.56% at month 2, and 42.01% at month 3

## Pre-submission gate

The analytical work and local repository contents now match the live TripleTen rubric. The remaining steps are external actions: publish the Tableau workbook, add the resulting workbook file/link to the public GitHub repository, verify the public repository contents, and submit that repository URL to TripleTen.
