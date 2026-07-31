# Payment Status Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `payment_status`
>
> **Version:** 2.0

---

# Overview

The **Payment Status** table is a master reference table that defines the valid statuses for loan payment transactions.

Instead of storing payment status values directly in the **Payments** table, the system references this table to ensure standardized status management, improve data quality, and simplify reporting.

This table is essential for monitoring repayment progress, collection activities, and payment performance.

---

# Business Purpose

The Payment Status table standardizes the status of payment transactions throughout the Loan Management System.

Business objectives include:

- Standardizing payment status values
- Preventing inconsistent payment records
- Supporting repayment monitoring
- Improving collection reporting
- Enabling payment analytics
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payment_status |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Table | payments |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Payment status identifier |
| status_name | VARCHAR(50) | No | | | Payment status name |

---

# Column Descriptions

## id

**Description**

Unique identifier for each payment status.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## status_name

**Description**

Defines the business status of a payment transaction.

Typical values:

- Pending
- Paid
- Late
- Failed
- Cancelled

**Business Rules**

- Required
- Must be unique
- Use standardized naming
- Maintain consistent terminology across the system

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique payment status identifier |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| payments | One-to-Many | One payment status may be used by many payment records |

---

# Entity Relationship

```text
payment_status
        │
        │ id
        ▼
payments
```

---

# Business Rules

- Every payment must have one valid payment status.
- Payment statuses must be selected from this table.
- Status names should not be duplicated.
- Payment status changes should follow the organization's collection policies.
- Master data should only be updated by authorized administrators.

---

# Typical Payment Lifecycle

```text
Pending

↓

Paid

OR

Late

↓

Failed

OR

Cancelled
```

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Status | status_name cannot be NULL |
| Unique Status | Duplicate status names are not allowed |
| Standard Naming | Use approved payment status values |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| UNIQUE | status_name |
| NOT NULL | status_name |

Example:

```sql
UNIQUE (status_name)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payment_status | id | Primary key lookup |
| idx_payment_status_name | status_name | Status lookup |

---

# Sample Records

| id | status_name |
|---:|-------------|
| 1 | Pending |
| 2 | Paid |
| 3 | Late |
| 4 | Failed |
| 5 | Cancelled |

---

# Common SQL Queries

## View All Payment Statuses

```sql
SELECT *
FROM payment_status;
```

---

## Number of Payments by Status

```sql
SELECT
    ps.status_name,
    COUNT(p.id) AS total_payments
FROM payment_status ps
LEFT JOIN payments p
    ON ps.id = p.payment_status_id
GROUP BY ps.status_name
ORDER BY total_payments DESC;
```

---

## Total Amount Paid by Status

```sql
SELECT
    ps.status_name,
    SUM(p.payment_amount) AS total_amount
FROM payments p
JOIN payment_status ps
    ON p.payment_status_id = ps.id
GROUP BY ps.status_name
ORDER BY total_amount DESC;
```

---

## Overdue Payments

```sql
SELECT
    p.*
FROM payments p
JOIN payment_status ps
    ON p.payment_status_id = ps.id
WHERE ps.status_name = 'Late';
```

---

# Reporting Usage

This table is commonly used in:

- Payment Dashboard
- Collection Dashboard
- Executive Dashboard
- Payment Monitoring Report
- Delinquency Analysis
- Collection Performance Report

---

# KPIs Supported

- Successful Payment Rate
- Late Payment Rate
- Failed Payment Rate
- Collection Rate
- Total Payments
- Outstanding Payments
- Monthly Payment Performance

---

# ETL Considerations

- Load payment status master data before payment transactions.
- Validate payment status references.
- Prevent duplicate status values.
- Standardize naming conventions.
- Preserve historical status consistency.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Internal | Reference master data |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | Permanent |
| Archive Policy | Not Applicable |
| Deletion Policy | Administrative update only |

---

# Dependencies

### Depends On

None

### Referenced By

- payments

---

# AI & RAG Notes

The **Payment Status** table provides standardized payment state definitions that enable AI systems to:

- Analyze repayment performance.
- Generate payment status reports.
- Produce SQL queries involving payment monitoring.
- Support collection analytics.
- Recommend joins with the Payments table.
- Improve dashboard consistency through standardized status values.

---

# Related Documentation

- Payments Table
- Payment Methods Table
- Loan Status Table
- Database Schema
- Relationship Matrix
- Collection Dashboard
- Business Rules

---

# Summary

The **Payment Status** table is a master reference table that defines the valid lifecycle states for payment transactions within the Loan Management System. By centralizing payment status definitions, it ensures consistent repayment tracking, reliable reporting, accurate analytics, and strong referential integrity across operational systems, business intelligence solutions, and AI-powered applications.
