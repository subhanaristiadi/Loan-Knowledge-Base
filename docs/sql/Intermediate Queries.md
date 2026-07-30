# Intermediate SQL Queries

> **Project:** Loan Knowledge Base
>
> **Module:** SQL Cookbook
>
> **Document:** Intermediate Queries
>
> **Version:** 2.0

---

# Overview

This document contains intermediate-level SQL queries for the Loan Management database.

These examples build upon the fundamentals introduced in **Basic SQL Queries** and introduce more practical reporting techniques commonly used by:

- Data Analysts
- Business Intelligence Developers
- Reporting Teams
- Backend Developers
- AI-powered SQL Assistants

The examples include more complex joins, aggregations, filtering, conditional logic, and analytical calculations.

---

# Topics Covered

- Multi-table JOINs
- Aggregate Functions
- CASE Expressions
- GROUP BY
- HAVING
- Date Functions
- Conditional Aggregation
- Subqueries
- Derived Tables
- Business Reporting

---

# 1. Customer Loan Summary

Retrieve each customer with the number of approved loans and total approved amount.

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

# 2. Total Applications by Province

```sql
SELECT
    p.province_name,
    COUNT(a.id) AS total_applications
FROM provinces p
JOIN cities c
    ON p.id = c.province_id
JOIN users u
    ON c.id = u.city_id
JOIN application a
    ON u.id = a.user_id
GROUP BY p.province_name
ORDER BY total_applications DESC;
```

---

# 3. Loan Amount by Education Level

```sql
SELECT
    e.education_name,
    COUNT(l.id) AS total_loans,
    SUM(l.approved_amount) AS total_amount,
    ROUND(AVG(l.approved_amount), 2) AS average_amount
FROM educations e
JOIN users u
    ON e.id = u.education_id
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id
GROUP BY e.education_name
ORDER BY total_amount DESC;
```

---

# 4. Monthly Loan Applications

```sql
SELECT
    DATE_TRUNC('month', application_date) AS month,
    COUNT(*) AS total_applications
FROM application
GROUP BY month
ORDER BY month;
```

---

# 5. Monthly Loan Disbursement

```sql
SELECT
    DATE_TRUNC('month', start_date) AS month,
    COUNT(*) AS total_loans,
    SUM(approved_amount) AS total_disbursed
FROM loans
GROUP BY month
ORDER BY month;
```

---

# 6. Payment Summary by Method

```sql
SELECT
    pm.method_name,
    COUNT(*) AS total_transactions,
    SUM(p.amount) AS total_amount,
    AVG(p.amount) AS average_payment
FROM payments p
JOIN payment_methods pm
    ON p.payment_method_id = pm.id
GROUP BY pm.method_name
ORDER BY total_amount DESC;
```

---

# 7. Payment Summary by Status

```sql
SELECT
    ps.status_name,
    COUNT(*) AS total_transactions,
    SUM(p.amount) AS total_amount
FROM payments p
JOIN payment_status ps
    ON p.payment_status_id = ps.id
GROUP BY ps.status_name
ORDER BY total_amount DESC;
```

---

# 8. Loan Portfolio by Status

```sql
SELECT
    ls.status_name,
    COUNT(*) AS total_loans,
    SUM(approved_amount) AS portfolio_value
FROM loans l
JOIN loan_status ls
    ON l.loan_status_id = ls.id
GROUP BY ls.status_name
ORDER BY portfolio_value DESC;
```

---

# 9. Customers with Large Loans

Find customers whose total approved loans exceed 50,000.

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
HAVING SUM(l.approved_amount) > 50000
ORDER BY total_loan DESC;
```

---

# 10. Loan Purpose Distribution

```sql
SELECT
    r.reason_name,
    COUNT(*) AS applications,
    SUM(a.requested_amount) AS requested_amount
FROM reason r
JOIN application a
    ON r.id = a.reason_id
GROUP BY r.reason_name
ORDER BY requested_amount DESC;
```

---

# 11. Customer Classification

```sql
SELECT
    full_name,
    CASE
        WHEN created_at >= CURRENT_DATE - INTERVAL '30 days'
            THEN 'New Customer'
        ELSE 'Existing Customer'
    END AS customer_type
FROM users;
```

---

# 12. Loan Size Classification

```sql
SELECT
    id,
    approved_amount,
    CASE
        WHEN approved_amount < 5000 THEN 'Small'
        WHEN approved_amount < 20000 THEN 'Medium'
        ELSE 'Large'
    END AS loan_category
FROM loans;
```

---

# 13. Outstanding Balance

Estimate outstanding balance by subtracting total payments from approved loan amount.

```sql
SELECT
    l.id,
    l.approved_amount,
    COALESCE(SUM(p.amount), 0) AS total_paid,
    l.approved_amount - COALESCE(SUM(p.amount), 0)
        AS outstanding_balance
FROM loans l
LEFT JOIN payments p
    ON l.id = p.loan_id
GROUP BY
    l.id,
    l.approved_amount
ORDER BY outstanding_balance DESC;
```

---

# 14. Latest Payment per Loan

```sql
SELECT
    loan_id,
    MAX(payment_date) AS latest_payment
FROM payments
GROUP BY loan_id;
```

---

# 15. Customers Without Loans

```sql
SELECT
    u.id,
    u.full_name
FROM users u
LEFT JOIN application a
    ON u.id = a.user_id
LEFT JOIN loans l
    ON a.id = l.application_id
WHERE l.id IS NULL;
```

---

# 16. Average Payment by Loan

```sql
SELECT
    loan_id,
    ROUND(AVG(amount), 2) AS average_payment
FROM payments
GROUP BY loan_id
ORDER BY average_payment DESC;
```

---

# 17. Largest Loan in Each Province

```sql
SELECT
    p.province_name,
    MAX(l.approved_amount) AS largest_loan
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
ORDER BY largest_loan DESC;
```

---

# 18. Daily Payment Summary

```sql
SELECT
    payment_date,
    COUNT(*) AS total_transactions,
    SUM(amount) AS total_collected
FROM payments
GROUP BY payment_date
ORDER BY payment_date;
```

---

# 19. Applications by Month and Status

```sql
SELECT
    DATE_TRUNC('month', application_date) AS month,
    status,
    COUNT(*) AS total
FROM application
GROUP BY
    month,
    status
ORDER BY
    month,
    status;
```

---

# 20. Province Loan Ranking

```sql
SELECT
    p.province_name,
    SUM(l.approved_amount) AS total_portfolio
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
ORDER BY total_portfolio DESC;
```

---

# 21. Average Processing Time

Calculate the average number of days from application submission to approval.

```sql
SELECT
    ROUND(
        AVG(
            ah.changed_at::date -
            a.application_date
        ),
        2
    ) AS average_days
FROM application a
JOIN application_history ah
    ON a.id = ah.application_id
WHERE ah.current_status = 'Approved';
```

---

# 22. Top Payment Days

```sql
SELECT
    payment_date,
    SUM(amount) AS collected
FROM payments
GROUP BY payment_date
ORDER BY collected DESC
LIMIT 10;
```

---

# 23. Monthly Collection Report

```sql
SELECT
    DATE_TRUNC('month', payment_date) AS month,
    SUM(amount) AS collected_amount
FROM payments
GROUP BY month
ORDER BY month;
```

---

# 24. Customers by Education and Province

```sql
SELECT
    e.education_name,
    p.province_name,
    COUNT(*) AS customers
FROM users u
JOIN educations e
    ON u.education_id = e.id
JOIN cities c
    ON u.city_id = c.id
JOIN provinces p
    ON c.province_id = p.id
GROUP BY
    e.education_name,
    p.province_name
ORDER BY customers DESC;
```

---

# 25. Loan Portfolio KPI

```sql
SELECT
    COUNT(*) AS total_loans,
    SUM(approved_amount) AS portfolio_value,
    AVG(approved_amount) AS average_loan,
    MIN(approved_amount) AS minimum_loan,
    MAX(approved_amount) AS maximum_loan
FROM loans;
```

---

# Intermediate SQL Techniques

These examples introduce several important SQL concepts:

| Technique | Purpose |
|-----------|---------|
| Multi-table JOIN | Combine related entities |
| LEFT JOIN | Include unmatched records |
| CASE | Categorize data |
| HAVING | Filter grouped results |
| Aggregate Functions | Produce summaries |
| DATE_TRUNC | Monthly reporting |
| COALESCE | Handle NULL values |
| Subqueries & Derived Tables | Build layered queries |

---

# Best Practices

When writing intermediate SQL:

- Use meaningful table aliases.
- Filter rows before aggregation whenever possible.
- Replace `NULL` values with `COALESCE()` when appropriate.
- Avoid duplicate calculations.
- Group only necessary columns.
- Format SQL consistently.
- Test queries on small datasets before running on production data.

---

# AI & RAG Notes

These intermediate examples bridge the gap between basic retrieval and advanced analytics. They demonstrate common reporting patterns that AI assistants can reuse for:

- Operational reports
- KPI calculations
- Portfolio summaries
- Customer analytics
- Payment monitoring
- Business Intelligence dashboards

They also provide high-quality examples for Retrieval-Augmented Generation (RAG) systems to generate accurate and maintainable SQL.

---

# Related Documentation

- Basic SQL Queries
- Advanced SQL Queries
- Common Table Expressions (CTE)
- Window Functions
- Database Schema
- KPI Catalog
- Business Questions

---

# Summary

This document presents intermediate SQL queries commonly used in loan management systems. By combining joins, aggregations, conditional logic, date functions, and business-oriented reporting techniques, these examples provide a solid foundation for analytical reporting and prepare users for more advanced SQL concepts such as CTEs and window functions.
