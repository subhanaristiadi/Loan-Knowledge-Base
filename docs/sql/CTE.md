# Common Table Expressions (CTE)

> **Project:** Loan Knowledge Base
>
> **Module:** SQL Cookbook
>
> **Document:** Common Table Expressions (CTE)
>
> **Version:** 2.0

---

# Overview

A **Common Table Expression (CTE)** is a temporary named result set that exists only for the duration of a single SQL statement.

CTEs improve:

- Readability
- Maintainability
- Query organization
- Complex calculations
- Multi-step analysis

Instead of writing deeply nested subqueries, complex logic can be divided into smaller, easier-to-understand blocks.

---

# CTE Syntax

```sql
WITH cte_name AS (

    SELECT ...

)

SELECT *
FROM cte_name;
```

Multiple CTEs can be chained together.

```sql
WITH

first_cte AS (

    ...

),

second_cte AS (

    ...

)

SELECT *
FROM second_cte;
```

---

# Benefits of Using CTEs

- Improves query readability.
- Breaks complex logic into manageable steps.
- Reduces repeated calculations.
- Simplifies debugging.
- Makes SQL easier to maintain.
- Works well with window functions.
- Ideal for BI reporting and analytics.

---

# 1. Total Loan Amount per Customer

```sql
WITH customer_loans AS (

SELECT

a.user_id,

SUM(l.approved_amount) AS total_amount

FROM application a

JOIN loans l
ON a.id = l.application_id

GROUP BY a.user_id

)

SELECT

u.full_name,

c.total_amount

FROM customer_loans c

JOIN users u
ON c.user_id = u.id

ORDER BY total_amount DESC;
```

---

# 2. Monthly Loan Summary

```sql
WITH monthly_loans AS (

SELECT

DATE_TRUNC('month', start_date) AS month,

COUNT(*) AS total_loans,

SUM(approved_amount) AS total_amount

FROM loans

GROUP BY month

)

SELECT *

FROM monthly_loans

ORDER BY month;
```

---

# 3. Active Loan Portfolio

```sql
WITH active_loans AS (

SELECT

id,

approved_amount

FROM loans l

JOIN loan_status ls
ON l.loan_status_id = ls.id

WHERE ls.status_name = 'Active'

)

SELECT

COUNT(*) AS active_loans,

SUM(approved_amount) AS outstanding_balance

FROM active_loans;
```

---

# 4. Repeat Borrowers

```sql
WITH borrower_summary AS (

SELECT

a.user_id,

COUNT(l.id) AS total_loans

FROM application a

JOIN loans l
ON a.id = l.application_id

GROUP BY a.user_id

)

SELECT

u.full_name,

b.total_loans

FROM borrower_summary b

JOIN users u
ON b.user_id = u.id

WHERE total_loans > 1

ORDER BY total_loans DESC;
```

---

# 5. Monthly Growth Analysis

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
OVER(
ORDER BY month
) AS previous_month,

ROUND(

(
total_amount -

LAG(total_amount)
OVER(
ORDER BY month
)

)

/

NULLIF(

LAG(total_amount)
OVER(
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

# 6. Payment Collection Summary

```sql
WITH paid_transactions AS (

SELECT

amount

FROM payments p

JOIN payment_status ps
ON p.payment_status_id = ps.id

WHERE ps.status_name = 'Paid'

)

SELECT

COUNT(*) AS paid_transactions,

SUM(amount) AS collected_amount,

AVG(amount) AS average_payment

FROM paid_transactions;
```

---

# 7. Loan Purpose Ranking

```sql
WITH purpose_summary AS (

SELECT

r.reason_name,

COUNT(*) AS total_applications,

SUM(a.requested_amount) AS requested_amount

FROM reason r

JOIN application a
ON r.id = a.reason_id

GROUP BY r.reason_name

)

SELECT *

FROM purpose_summary

ORDER BY requested_amount DESC;
```

---

# 8. Province Loan Analysis

```sql
WITH province_summary AS (

SELECT

p.province_name,

COUNT(l.id) AS loans,

SUM(l.approved_amount) AS amount

FROM provinces p

JOIN cities c
ON p.id = c.province_id

JOIN users u
ON c.id = u.city_id

JOIN application a
ON u.id = a.user_id

JOIN loans l
ON a.id = l.application_id

GROUP BY p.province_name

)

SELECT *

FROM province_summary

ORDER BY amount DESC;
```

---

# 9. Customer Payment Summary

```sql
WITH payment_summary AS (

SELECT

a.user_id,

SUM(p.amount) AS total_paid,

COUNT(*) AS total_payments

FROM payments p

JOIN loans l
ON p.loan_id = l.id

JOIN application a
ON l.application_id = a.id

GROUP BY a.user_id

)

SELECT

u.full_name,

ps.total_paid,

ps.total_payments

FROM payment_summary ps

JOIN users u
ON ps.user_id = u.id

ORDER BY total_paid DESC;
```

---

# 10. Loan Aging Report

```sql
WITH aging AS (

SELECT

id,

approved_amount,

CURRENT_DATE - start_date AS age_days

FROM loans

)

SELECT *

FROM aging

ORDER BY age_days DESC;
```

---

# 11. Top Customers by Outstanding Balance

```sql
WITH outstanding AS (

SELECT

a.user_id,

SUM(l.approved_amount) -

COALESCE(SUM(p.amount),0) AS outstanding_balance

FROM application a

JOIN loans l
ON a.id = l.application_id

LEFT JOIN payments p
ON l.id = p.loan_id

GROUP BY a.user_id

)

SELECT

u.full_name,

o.outstanding_balance

FROM outstanding o

JOIN users u
ON o.user_id = u.id

ORDER BY outstanding_balance DESC;
```

---

# 12. Loan Status Distribution

```sql
WITH status_summary AS (

SELECT

ls.status_name,

COUNT(*) AS total_loans

FROM loan_status ls

JOIN loans l
ON ls.id = l.loan_status_id

GROUP BY ls.status_name

)

SELECT *

FROM status_summary

ORDER BY total_loans DESC;
```

---

# Multiple CTE Example

Complex reports often require multiple CTEs.

```sql
WITH

monthly_loans AS (

SELECT

DATE_TRUNC('month', start_date) AS month,

SUM(approved_amount) AS total_disbursed

FROM loans

GROUP BY month

),

monthly_payments AS (

SELECT

DATE_TRUNC('month', payment_date) AS month,

SUM(amount) AS total_collected

FROM payments

GROUP BY month

)

SELECT

l.month,

l.total_disbursed,

p.total_collected,

l.total_disbursed - COALESCE(p.total_collected,0)

AS net_outstanding

FROM monthly_loans l

LEFT JOIN monthly_payments p

ON l.month = p.month

ORDER BY l.month;
```

---

# Recursive CTE

Recursive CTEs are useful for hierarchical data.

General syntax:

```sql
WITH RECURSIVE cte_name AS (

-- Anchor query

SELECT ...

UNION ALL

-- Recursive query

SELECT ...

FROM cte_name

)

SELECT *

FROM cte_name;
```

Although the Loan Management schema does not include hierarchical tables by default, recursive CTEs may be useful if future versions introduce organizational structures, referral trees, or branch hierarchies.

---

# Best Practices

When using CTEs:

- Give each CTE a descriptive name.
- Keep each CTE focused on a single task.
- Avoid creating unnecessarily deep CTE chains.
- Use CTEs instead of repeating identical subqueries.
- Combine CTEs with window functions for advanced analytics.
- Test each CTE independently during development.
- Use comments to describe complex business logic.

---

# Common Use Cases

CTEs are particularly useful for:

- Executive dashboards
- KPI calculations
- Financial reporting
- Customer segmentation
- Portfolio analysis
- Cohort analysis
- Loan aging
- Collection performance
- Time-series analysis
- Multi-step transformations

---

# AI & RAG Notes

CTEs provide highly structured SQL that is easier for AI assistants to interpret and generate. They:

- Improve explainability.
- Reduce query complexity.
- Support incremental reasoning.
- Produce reusable analytical building blocks.
- Help Retrieval-Augmented Generation (RAG) systems generate more maintainable SQL.

---

# Related Documentation

- Basic SQL Queries
- Advanced SQL Queries
- Window Functions
- SQL Prompt
- Database Schema
- Relationship Matrix
- KPI Catalog

---

# Summary

This document introduces Common Table Expressions (CTEs) for organizing complex SQL into readable, reusable components. The examples demonstrate how CTEs simplify reporting, financial analysis, customer analytics, portfolio monitoring, and dashboard development while improving maintainability and supporting AI-assisted SQL generation.
