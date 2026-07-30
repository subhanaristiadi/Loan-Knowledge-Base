# Advanced SQL Queries

> **Project:** Loan Knowledge Base
>
> **Module:** SQL Cookbook
>
> **Document:** Advanced Queries
>
> **Version:** 2.0

---

# Overview

This document contains advanced SQL queries commonly used in loan management systems for reporting, business intelligence, operational monitoring, and analytics.

The examples assume a PostgreSQL-compatible database but can be adapted to MySQL, SQL Server, or other relational database systems.

---

# Topics Covered

- Multi-table JOIN
- Common Table Expressions (CTE)
- Window Functions
- Ranking
- Running Totals
- Cohort Analysis
- Loan Aging
- Delinquency Analysis
- Customer Segmentation
- Payment Performance
- Time Series Analysis

---

# 1. Customer Loan Summary

Retrieve customer information along with total approved loans.

```sql
SELECT
    u.id,
    u.full_name,
    COUNT(l.id) AS total_loans,
    SUM(l.approved_amount) AS total_amount
FROM users u
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id
GROUP BY
    u.id,
    u.full_name
ORDER BY total_amount DESC;
```

---

# 2. Top 10 Customers by Loan Amount

```sql
SELECT
    u.full_name,
    SUM(l.approved_amount) AS total_loan
FROM users u
JOIN application a
ON u.id = a.user_id
JOIN loans l
ON a.id = l.application_id
GROUP BY u.full_name
ORDER BY total_loan DESC
LIMIT 10;
```

---

# 3. Monthly Loan Disbursement

```sql
SELECT
    DATE_TRUNC('month', start_date) AS month,
    COUNT(*) AS loans,
    SUM(approved_amount) AS amount
FROM loans
GROUP BY month
ORDER BY month;
```

---

# 4. Loan Distribution by Province

```sql
SELECT
    p.province_name,
    COUNT(l.id) AS loans,
    SUM(l.approved_amount) AS total_amount
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
ORDER BY total_amount DESC;
```

---

# 5. Average Loan by Education

```sql
SELECT
    e.education_name,
    ROUND(AVG(l.approved_amount),2) AS avg_loan
FROM educations e
JOIN users u
ON e.id=u.education_id
JOIN application a
ON u.id=a.user_id
JOIN loans l
ON a.id=l.application_id
GROUP BY e.education_name
ORDER BY avg_loan DESC;
```

---

# 6. Running Loan Total

```sql
SELECT
    start_date,
    approved_amount,
    SUM(approved_amount)
        OVER (
            ORDER BY start_date
        ) AS cumulative_amount
FROM loans;
```

---

# 7. Running Payment Total

```sql
SELECT
    payment_date,
    amount,
    SUM(amount)
        OVER(
            ORDER BY payment_date
        ) AS cumulative_payment
FROM payments;
```

---

# 8. Loan Ranking

```sql
SELECT
    id,
    approved_amount,
    RANK()
    OVER(
        ORDER BY approved_amount DESC
    ) AS ranking
FROM loans;
```

---

# 9. Dense Ranking

```sql
SELECT
    id,
    approved_amount,
    DENSE_RANK()
    OVER(
        ORDER BY approved_amount DESC
    ) AS ranking
FROM loans;
```

---

# 10. Customer Loan Ranking

```sql
SELECT
    u.full_name,
    SUM(l.approved_amount) total_loan,
    RANK()
    OVER(
        ORDER BY SUM(l.approved_amount) DESC
    ) rank_customer
FROM users u
JOIN application a
ON u.id=a.user_id
JOIN loans l
ON a.id=l.application_id
GROUP BY u.full_name;
```

---

# 11. Previous Loan Comparison

```sql
SELECT
    id,
    approved_amount,
    LAG(approved_amount)
    OVER(
        ORDER BY start_date
    ) AS previous_loan
FROM loans;
```

---

# 12. Next Loan Comparison

```sql
SELECT
    id,
    approved_amount,
    LEAD(approved_amount)
    OVER(
        ORDER BY start_date
    ) AS next_loan
FROM loans;
```

---

# 13. Monthly Growth Rate

```sql
WITH monthly AS (

SELECT
DATE_TRUNC('month', start_date) month,
SUM(approved_amount) total

FROM loans

GROUP BY month

)

SELECT
month,
total,

LAG(total)
OVER(
ORDER BY month
) previous,

ROUND(
(total-LAG(total)
OVER(ORDER BY month))
/
NULLIF(
LAG(total)
OVER(ORDER BY month),
0
)
*100,
2
) growth_percent

FROM monthly;
```

---

# 14. Active Loan Portfolio

```sql
SELECT
COUNT(*) total_active,
SUM(approved_amount) outstanding
FROM loans l
JOIN loan_status ls
ON l.loan_status_id=ls.id
WHERE ls.status_name='Active';
```

---

# 15. Overdue Payments

```sql
SELECT
p.id,
u.full_name,
p.payment_date,
p.amount
FROM payments p
JOIN loans l
ON p.loan_id=l.id
JOIN application a
ON l.application_id=a.id
JOIN users u
ON a.user_id=u.id
JOIN payment_status ps
ON p.payment_status_id=ps.id
WHERE ps.status_name='Overdue';
```

---

# 16. Payment Collection Rate

```sql
SELECT

ROUND(

SUM(
CASE
WHEN ps.status_name='Paid'
THEN amount
ELSE 0
END
)

/

SUM(amount)

*100

,2)

AS collection_rate

FROM payments p

JOIN payment_status ps
ON p.payment_status_id=ps.id;
```

---

# 17. Loan Aging Report

```sql
SELECT

id,

CURRENT_DATE-start_date

AS age_days,

approved_amount

FROM loans

ORDER BY age_days DESC;
```

---

# 18. Loan Purpose Analysis

```sql
SELECT

r.reason_name,

COUNT(*) applications,

SUM(requested_amount) requested

FROM reason r

JOIN application a
ON r.id=a.reason_id

GROUP BY r.reason_name

ORDER BY requested DESC;
```

---

# 19. Customer Segmentation

```sql
SELECT

CASE

WHEN approved_amount<5000
THEN 'Small'

WHEN approved_amount<20000
THEN 'Medium'

ELSE 'Large'

END segment,

COUNT(*) loans

FROM loans

GROUP BY segment;
```

---

# 20. Repeat Borrowers

```sql
SELECT

u.full_name,

COUNT(l.id) total_loans

FROM users u

JOIN application a
ON u.id=a.user_id

JOIN loans l
ON a.id=l.application_id

GROUP BY u.full_name

HAVING COUNT(l.id)>1

ORDER BY total_loans DESC;
```

---

# 21. Approval Rate

```sql
SELECT

ROUND(

SUM(
CASE
WHEN status='Approved'
THEN 1
ELSE 0
END
)::numeric

/

COUNT(*)

*100

,2)

AS approval_rate

FROM application;
```

---

# 22. Average Time to Approval

```sql
SELECT

AVG(

ah.changed_at::date
-
a.application_date

)

AS avg_days

FROM application a

JOIN application_history ah
ON a.id=ah.application_id

WHERE ah.current_status='Approved';
```

---

# 23. Daily Payment Trend

```sql
SELECT

payment_date,

SUM(amount) total_payment

FROM payments

GROUP BY payment_date

ORDER BY payment_date;
```

---

# 24. Monthly Payment Trend

```sql
SELECT

DATE_TRUNC(
'month',
payment_date
)

AS month,

SUM(amount)

AS payment

FROM payments

GROUP BY month

ORDER BY month;
```

---

# 25. Cohort Analysis

```sql
WITH first_loan AS (

SELECT

user_id,

MIN(application_date)

AS first_date

FROM application

GROUP BY user_id

)

SELECT

DATE_TRUNC('month',first_date)

AS cohort,

COUNT(*)

customers

FROM first_loan

GROUP BY cohort

ORDER BY cohort;
```

---

# 26. Loan Status Distribution

```sql
SELECT

ls.status_name,

COUNT(*) loans

FROM loan_status ls

JOIN loans l
ON ls.id=l.loan_status_id

GROUP BY ls.status_name

ORDER BY loans DESC;
```

---

# 27. Payment Method Usage

```sql
SELECT

pm.method_name,

COUNT(*) total_transactions,

SUM(amount) total_amount

FROM payment_methods pm

JOIN payments p
ON pm.id=p.payment_method_id

GROUP BY pm.method_name

ORDER BY total_amount DESC;
```

---

# 28. Monthly Revenue from Interest (Estimated)

```sql
SELECT

DATE_TRUNC('month',start_date)

AS month,

SUM(
approved_amount
*
interest_rate
/
100
)

estimated_interest

FROM loans

GROUP BY month

ORDER BY month;
```

---

# 29. Highest Single Payment

```sql
SELECT *

FROM payments

ORDER BY amount DESC

LIMIT 1;
```

---

# 30. Customer Lifetime Value (Loan Value)

```sql
SELECT

u.full_name,

SUM(l.approved_amount)

lifetime_value

FROM users u

JOIN application a
ON u.id=a.user_id

JOIN loans l
ON a.id=l.application_id

GROUP BY u.full_name

ORDER BY lifetime_value DESC;
```

---

# Best Practices

When writing advanced SQL:

- Filter data as early as possible.
- Create indexes on frequently joined columns.
- Avoid unnecessary `SELECT *`.
- Use CTEs to simplify complex queries.
- Use window functions instead of self-joins when possible.
- Validate execution plans for large datasets.
- Aggregate only required columns.

---

# AI & RAG Notes

These SQL examples provide high-quality retrieval context for AI assistants by demonstrating:

- Business-oriented query patterns.
- Proper JOIN strategies.
- Analytical SQL techniques.
- Window function usage.
- Reporting best practices.
- Real-world dashboard queries.

They are suitable as reference examples for SQL generation, code completion, and analytics assistance in Retrieval-Augmented Generation (RAG) systems.

---

# Related Documentation

- SQL Basics
- SQL Cookbook
- Database Schema
- Table Documentation
- KPIs
- Dashboard Ideas
- Business Questions

---

# Summary

This document presents a collection of advanced SQL queries used in loan management systems. The examples cover operational reporting, customer analytics, portfolio monitoring, payment analysis, cohort analysis, rankings, window functions, and business intelligence use cases, serving as practical references for analysts, developers, and AI-assisted SQL generation.
