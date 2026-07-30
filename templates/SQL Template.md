# SQL Template

> **Project:** Loan Knowledge Base
>
> **Module:** SQL Cookbook
>
> **Document:** SQL Template
>
> **Version:** 2.0

---

# Overview

This template provides a standardized structure for writing SQL queries within the Loan Management System.

Its goals are to:

- Improve query readability.
- Promote consistent coding standards.
- Simplify maintenance.
- Improve performance.
- Support Business Intelligence reporting.
- Assist AI-powered SQL generation.
- Encourage reusable SQL patterns.

The template follows ANSI SQL whenever possible and is compatible with PostgreSQL. Minor syntax adjustments may be required for MySQL, SQL Server, Oracle, or other relational database systems.

---

# SQL Metadata

| Field | Description |
|---------|-------------|
| Query ID | Unique query identifier |
| Query Name | Descriptive query title |
| Category | Reporting, Analytics, ETL, Dashboard, etc. |
| Author | Query author |
| Version | Query version |
| Database | PostgreSQL |
| Last Updated | Latest revision |
| Related Tables | Tables used by the query |

---

# Query Information

## Query ID

```text
SQL-001
```

---

## Query Name

```text
Customer Loan Summary
```

---

## Business Objective

Describe the purpose of the query.

Example:

> Generate a report showing the number of approved loans and total approved loan amount for each customer.

---

## Business Question

Example:

> Which customers have received the highest total approved loan amount?

---

## Source Tables

| Table | Purpose |
|---------|----------|
| users | Customer information |
| application | Loan applications |
| loans | Approved loans |

---

## Relationships

```text
users
   │
   │ user_id
   ▼
application
   │
   │ application_id
   ▼
loans
```

---

# SQL Template

````sql
/*
=========================================================
Query Name  : Customer Loan Summary
Query ID    : SQL-001
Purpose     : Customer loan portfolio report
Author      : Your Name
Version     : 1.0
=========================================================
*/

SELECT
    u.id,
    u.full_name,
    COUNT(l.id) AS total_loans,
    SUM(l.approved_amount) AS total_approved_amount
FROM users u
JOIN application a
    ON u.id = a.user_id
JOIN loans l
    ON a.id = l.application_id
GROUP BY
    u.id,
    u.full_name
ORDER BY total_approved_amount DESC;
