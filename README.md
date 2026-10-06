# Fitness Subscription Analytics

This Tableau Public project analyzes customer retention, subscription revenue, and the relationship between customer acquisition cost (CAC) and lifetime value (LTV) for a fitness subscription business.

## Live Tableau report

[View FitnessHub Subscription Analytics on Tableau Public](https://public.tableau.com/app/profile/jonathan.colon/viz/FitnessHub_Subscription_Analytics/CustomerCohort)

## Project objectives

- Identify when customer retention declines most sharply after acquisition.
- Forecast subscription revenue for the next 12 months.
- Compare cumulative LTV with total CAC for the 2024 and 2025 acquisition cohorts.
- Determine when each cohort reaches break-even.

## Data model

The workbook uses two related Excel tables:

- `customers`: one row per customer, including acquisition channel, subscription plan, country, and CAC.
- `transactions`: one row per transaction, including transaction date, type, product, and revenue.

The tables are related on `Customer_ID`. `Transaction_Date` is stored as a date. The source contains 9,300 customers and 64,979 transactions, with dates from January 1, 2024 through January 31, 2026.

## Tableau calculations

```tableau
// First Purchase Date
{ FIXED [Customer ID (transactions)] :
    MIN(IF [Transaction Type] = "Subscription" THEN [Transaction Date] END)
}

// Cohort Month
DATETRUNC("month", [First Purchase Date])

// Months Since First Purchase
DATEDIFF("month", [First Purchase Date], [Transaction Date])

// Active Customers
COUNTD([Customer ID (transactions)])

// Retention Rate (computed across months within each cohort row)
[Active Customers] / WINDOW_MAX([Active Customers])

// Cohort Year
YEAR([First Purchase Date])

// Customer CAC — prevents transaction-level duplication
{ FIXED [Customer ID] : MIN([CAC]) }

// Total CAC by acquisition cohort
{ FIXED [Cohort Year] : SUM([Customer CAC]) }
```

Cumulative LTV is represented by a running sum of revenue across `Months Since First Purchase`, partitioned by `Cohort Year`.

## Findings

### Customer cohorts

- Retention is 100% in the acquisition month, approximately 85% in month 1, 78% in month 2, and 50% in month 3 across the monthly cohorts.
- The largest early retention decline occurs by month 3, when approximately half of the original customers remain active.
- The median observed customer lifetime is approximately two months.

### Revenue forecast

- Historical subscription revenue totals **$2,006,148**.
- The Tableau forecast uses all available observations, a 12-month horizon, annual seasonality of 12 months, and a 95% prediction interval.
- An independently reproduced Holt-Winters model estimates approximately **$2.05 million** in subscription revenue for the next 12 months. Tableau's displayed forecast is the authoritative workbook result.
- Revenue exhibits annual seasonality and strong underlying growth, with the highest expected revenue late in the forecast year.

### CAC versus LTV

| Cohort | Customers | Total CAC | Break-even month |
|---|---:|---:|---:|
| 2024 | 2,816 | $501,536.80 | 4 |
| 2025 | 6,484 | $1,162,459.11 | 6 |

- The 2024 cohort reaches break-even faster, in month 4.
- The 2025 cohort requires more acquisition investment and reaches break-even in month 6.
- Both cohorts ultimately generate cumulative revenue above total CAC, but the longer 2025 payback period should be monitored when setting acquisition budgets.

## Files

- `FitnessHub_Subscription_Analytics.twbx` — packaged Tableau workbook (added after publishing from Tableau Public).
- `data/Fitness_Subscriptions_Dataset.xlsx` — original project dataset.
- `screenshots/cohort_analysis.png` — screenshot taken directly from the completed Tableau monthly cohort retention worksheet.
- `screenshots/revenue_forecast.png` — historical subscription revenue and 12-month forecast.
- `screenshots/cac_vs_ltv.png` — screenshot taken directly from Tableau with cumulative revenue and CAC synchronized to the same axis scale.
- `screenshots/data_model.png` — Tableau relationship between customers and transactions.

## Business recommendations

1. Prioritize onboarding and engagement interventions before month 3, where the largest retention loss occurs.
2. Track 2025 acquisition channels closely because their cohort takes two months longer to recover CAC than the 2024 cohort.
3. Use the 95% forecast interval for budgeting rather than relying only on the point forecast.
4. Refresh this analysis monthly and compare actual revenue with forecast to detect changes in growth or seasonality.
