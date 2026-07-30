# Window Functions

> **Project:** Loan Knowledge Base
>
> **Module:** SQL Cookbook
>
> **Document:** Window Functions
>
> **Version:** 2.0

---

# Overview

Window functions perform calculations across a set of rows related to the current row **without collapsing the result set**.

Unlike `GROUP BY`, window functions preserve every row while providing additional analytical values.

They are essential for:

- Business Intelligence
- Financial reporting
- Trend analysis
- Time-series analysis
- Ranking
- Running totals
- Comparative analysis
- Executive dashboards

---

# Window Function Syntax

```sql
FUNCTION_NAME(expression)
OVER (
    PARTITION BY column
    ORDER BY column
)
```

A window function has two major components:

- **PARTITION BY** → Divides rows into groups.
- **ORDER BY** → Defines calculation order within each group.

---

# Window Function Categories

| Category | Functions |
|----------|-----------|
| Ranking | `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()` |
| Navigation | `LAG()`, `LEAD()`, `FIRST_VALUE()`, `LAST_VALUE()` |
| Aggregate | `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()` |
| Distribution | `PERCENT_RANK()`, `CUME_DIST()` |

---

# 1. Row Number

Assign a sequential number to every loan.

```sql
SELECT
    id,
    approved_amount,
    ROW_NUMBER() OVER (
        ORDER BY approved_amount DESC
    ) AS row_num
FROM loans;
```

---

# 2. Rank Loans

```sql
SELECT
    id,
    approved_amount,
    RANK() OVER (
        ORDER BY approved_amount DESC
    ) AS loan_rank
FROM loans;
```

---

# 3. Dense Rank

```sql
SELECT
    id,
    approved_amount,
    DENSE_RANK() OVER (
        ORDER BY approved_amount DESC
    ) AS dense_rank
FROM loans;
```

---

# 4. Rank Customers by Total Loan

```sql
SELECT
    u.full_name,
    SUM(l.approved_amount) AS total_loan,
    RANK() OVER (
        ORDER BY SUM(l.approved_amount) DESC
    ) AS customer_rank
FROM users u
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id
GROUP BY u.full_name;
```

---

# 5. Running Loan Total

```sql
SELECT
    start_date,
    approved_amount,
    SUM(approved_amount)
        OVER (
            ORDER BY start_date
        ) AS running_total
FROM loans;
```

---

# 6. Running Payment Total

```sql
SELECT
    payment_date,
    amount,
    SUM(amount)
        OVER (
            ORDER BY payment_date
        ) AS cumulative_payment
FROM payments;
```

---

# 7. Average Loan by Province

```sql
SELECT
    p.province_name,
    l.approved_amount,
    AVG(l.approved_amount)
        OVER (
            PARTITION BY p.province_name
        ) AS province_average
FROM provinces p
JOIN cities c
    ON p.id = c.province_id
JOIN users u
    ON c.id = u.city_id
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id;
```

---

# 8. Previous Loan Amount

```sql
SELECT
    id,
    approved_amount,
    LAG(approved_amount)
        OVER (
            ORDER BY start_date
        ) AS previous_loan
FROM loans;
```

---

# 9. Next Loan Amount

```sql
SELECT
    id,
    approved_amount,
    LEAD(approved_amount)
        OVER (
            ORDER BY start_date
        ) AS next_loan
FROM loans;
```

---

# 10. Monthly Growth

```sql
WITH monthly AS (

SELECT
DATE_TRUNC('month', start_date) AS month,
SUM(approved_amount) AS total_amount
FROM loans
GROUP BY month

)

SELECT

month,

total_amount,

LAG(total_amount)
OVER (
ORDER BY month
) previous_month,

ROUND(

(
total_amount -

LAG(total_amount)
OVER (
ORDER BY month
)

)

/

NULLIF(

LAG(total_amount)
OVER (
ORDER BY month
),

0

)

*100,

2

)

AS growth_percent

FROM monthly;
```

---

# 11. Payment Difference

Compare each payment with the previous payment.

```sql
SELECT
    payment_date,
    amount,
    amount -
    LAG(amount)
    OVER (
        ORDER BY payment_date
    ) AS difference
FROM payments;
```

---

# 12. First Loan Amount

```sql
SELECT
    id,
    approved_amount,
    FIRST_VALUE(approved_amount)
    OVER (
        ORDER BY start_date
    ) AS first_loan
FROM loans;
```

---

# 13. Last Loan Amount

```sql
SELECT
    id,
    approved_amount,
    LAST_VALUE(approved_amount)
    OVER (

        ORDER BY start_date

        ROWS BETWEEN
        UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING

    ) AS last_loan
FROM loans;
```

---

# 14. Percent Rank

```sql
SELECT
    id,
    approved_amount,
    PERCENT_RANK()
    OVER (
        ORDER BY approved_amount
    ) AS percent_rank
FROM loans;
```

---

# 15. Cumulative Distribution

```sql
SELECT
    id,
    approved_amount,
    CUME_DIST()
    OVER (
        ORDER BY approved_amount
    ) AS cumulative_distribution
FROM loans;
```

---

# 16. Divide Loans into Quartiles

```sql
SELECT
    id,
    approved_amount,
    NTILE(4)
    OVER (
        ORDER BY approved_amount
    ) AS quartile
FROM loans;
```

---

# 17. Running Average

```sql
SELECT
    payment_date,
    amount,
    AVG(amount)
    OVER (
        ORDER BY payment_date
    ) AS running_average
FROM payments;
```

---

# 18. Monthly Running Portfolio

```sql
WITH monthly AS (

SELECT

DATE_TRUNC('month', start_date) AS month,

SUM(approved_amount) AS amount

FROM loans

GROUP BY month

)

SELECT

month,

amount,

SUM(amount)
OVER(
ORDER BY month
) AS cumulative_portfolio

FROM monthly;
```

---

# 19. Loan Count per Customer

```sql
SELECT
    u.full_name,
    l.id,
    COUNT(*)
    OVER (
        PARTITION BY u.id
    ) AS total_customer_loans
FROM users u
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id;
```

---

# 20. Highest Loan per Province

```sql
SELECT *

FROM (

SELECT

p.province_name,

l.approved_amount,

ROW_NUMBER()

OVER(

PARTITION BY p.province_name

ORDER BY approved_amount DESC

)

AS rn

FROM provinces p

JOIN cities c
ON p.id=c.province_id

JOIN users u
ON c.id=u.city_id

JOIN application a
ON u.id=a.user_id

JOIN loans l
ON a.id=l.application_id

) x

WHERE rn=1;
```

---

# Common Window Functions

| Function | Purpose |
|----------|---------|
| `ROW_NUMBER()` | Sequential numbering |
| `RANK()` | Ranking with gaps |
| `DENSE_RANK()` | Ranking without gaps |
| `LAG()` | Previous row |
| `LEAD()` | Next row |
| `FIRST_VALUE()` | First value in window |
| `LAST_VALUE()` | Last value in window |
| `SUM() OVER()` | Running total |
| `AVG() OVER()` | Running average |
| `COUNT() OVER()` | Running count |
| `NTILE()` | Divide into buckets |
| `PERCENT_RANK()` | Relative rank |
| `CUME_DIST()` | Cumulative distribution |

---

# PARTITION BY vs GROUP BY

| GROUP BY | PARTITION BY |
|-----------|--------------|
| Returns one row per group | Preserves every row |
| Collapses results | Keeps original rows |
| Used for aggregation | Used for analytical calculations |
| Cannot access individual rows after grouping | Allows row-level comparisons |

Example:

`GROUP BY`

```sql
SELECT
loan_status_id,
COUNT(*)
FROM loans
GROUP BY loan_status_id;
```

`PARTITION BY`

```sql
SELECT
id,
loan_status_id,
COUNT(*)
OVER (
PARTITION BY loan_status_id
)
AS loans_in_status
FROM loans;
```

---

# Best Practices

When using window functions:

- Always specify an `ORDER BY` clause when row order matters.
- Use `PARTITION BY` only when calculations should restart for each group.
- Prefer window functions over self-joins for running totals and rankings.
- Combine window functions with CTEs for complex analytical queries.
- Explicitly define window frames for functions such as `LAST_VALUE()` to avoid unexpected results.
- Test queries with realistic datasets to verify ranking and cumulative calculations.

---

# Common Business Use Cases

Window functions are widely used for:

- Customer ranking
- Portfolio analysis
- Executive dashboards
- Payment trend analysis
- Running financial balances
- Loan growth tracking
- Monthly KPI reporting
- Collection performance monitoring
- Cohort and retention analysis
- Top-N reporting by region or customer segment

---

# AI & RAG Notes

Window functions are among the most requested SQL features in analytics. Including these examples enables AI assistants to:

- Generate advanced analytical SQL.
- Recommend efficient alternatives to self-joins.
- Explain ranking and cumulative calculations.
- Produce production-ready reporting queries.
- Support Retrieval-Augmented Generation (RAG) with reusable analytical patterns.

---

# Related Documentation

- Basic SQL Queries
- Intermediate SQL Queries
- Advanced SQL Queries
- Common Table Expressions (CTE)
- Database Schema
- KPI Catalog
- Business Questions

---

# Summary

This document introduces SQL Window Functions for analytical reporting in the Loan Management system. Covering ranking, navigation, cumulative calculations, running averages, distributions, and partitioned analytics, these examples provide essential building blocks for business intelligence, financial reporting, and AI-assisted SQL generation.
