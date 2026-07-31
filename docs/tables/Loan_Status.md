# Loan Status Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `loan_status`
>
> **Version:** 2.0

---

# Overview

The **Loan Status** table is a master reference table that defines the possible statuses of a loan throughout its lifecycle.

Rather than storing status names directly in the **Loans** table, the system references this table to maintain consistency, improve data quality, and simplify reporting.

The table acts as a lookup table for all valid loan statuses.

---

# Business Purpose

The Loan Status table standardizes loan status values across the Loan Management System.

Business objectives include:

- Standardizing loan statuses
- Preventing inconsistent status values
- Supporting loan lifecycle management
- Improving reporting consistency
- Simplifying dashboard development
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | loan_status |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Table | loans |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Loan status identifier |
| status_name | VARCHAR(50) | No | | | Loan status name |

---

# Column Descriptions

## id

**Description**

Unique identifier for each loan status.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## status_name

**Description**

The business name of the loan status.

Example values:

- Active
- Paid Off
- Defaulted
- Closed
- Written Off

**Business Rules**

- Required
- Must be unique
- Use standardized terminology
- Case-sensitive naming should follow organizational standards

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique loan status identifier |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| loans | One-to-Many | One loan status may be assigned to many loans |

---

# Entity Relationship

```text
loan_status
      │
      │ id
      ▼
loans
```

---

# Business Rules

- Every loan must have exactly one status.
- Status values must come from this table.
- Loan status changes should follow approved business workflows.
- Status records should rarely change.
- Status names should never be duplicated.

---

# Typical Loan Lifecycle

```text
Active

↓

Paid Off

OR

Defaulted

↓

Closed

OR

Written Off
```

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Status | status_name cannot be NULL |
| Unique Status | No duplicate status names |
| Standard Naming | Use approved status values |

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
| pk_loan_status | id | Primary key lookup |
| idx_loan_status_name | status_name | Status lookup |

---

# Sample Records

| id | status_name |
|---:|-------------|
| 1 | Active |
| 2 | Paid Off |
| 3 | Defaulted |
| 4 | Closed |
| 5 | Written Off |

---

# Common SQL Queries

## View All Loan Statuses

```sql
SELECT *
FROM loan_status;
```

---

## Number of Loans by Status

```sql
SELECT
    ls.status_name,
    COUNT(l.id) AS total_loans
FROM loan_status ls
LEFT JOIN loans l
    ON ls.id = l.loan_status_id
GROUP BY ls.status_name
ORDER BY total_loans DESC;
```

---

## Active Loans

```sql
SELECT
    l.*
FROM loans l
JOIN loan_status ls
    ON l.loan_status_id = ls.id
WHERE ls.status_name = 'Active';
```

---

## Loan Portfolio by Status

```sql
SELECT
    ls.status_name,
    SUM(l.approved_amount) AS portfolio_value
FROM loans l
JOIN loan_status ls
    ON l.loan_status_id = ls.id
GROUP BY ls.status_name
ORDER BY portfolio_value DESC;
```

---

# Reporting Usage

This table is commonly used in:

- Loan Portfolio Dashboard
- Executive Dashboard
- Collection Dashboard
- Credit Risk Dashboard
- Loan Performance Report
- Portfolio Monitoring Report

---

# KPIs Supported

- Active Loans
- Closed Loans
- Default Rate
- Paid-Off Rate
- Loan Portfolio by Status
- Outstanding Loan Balance
- Collection Performance

---

# ETL Considerations

- Load loan status master data before loading loans.
- Prevent duplicate status values.
- Validate foreign key references.
- Use controlled vocabulary for status names.
- Preserve historical consistency.

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

- loans

---

# AI & RAG Notes

The **Loan Status** table provides standardized lifecycle states that enable AI systems to:

- Explain loan progression.
- Generate portfolio reports by status.
- Produce status-based SQL queries.
- Analyze loan performance.
- Recommend appropriate joins with the Loans table.
- Support business intelligence dashboards and operational reporting.

---

# Related Documentation

- Loans Table
- Payment Status Table
- Database Schema
- Relationship Matrix
- Loan Lifecycle
- Business Rules
- Executive Dashboard

---

# Summary

The **Loan Status** table is a master reference table that defines the valid lifecycle states for loans within the Loan Management System. By centralizing loan status definitions, it ensures consistent reporting, reliable analytics, strong referential integrity, and simplified maintenance across operational systems, business intelligence solutions, and AI-powered applications.
