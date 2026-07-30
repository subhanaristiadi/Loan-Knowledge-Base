# Loans Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `loans`
>
> **Version:** 2.0

---

# Overview

The **Loans** table stores all approved loan contracts within the Loan Management System.

A loan record is created only after a customer's application has been successfully approved. It contains the official loan information used throughout the repayment period, including the approved amount, loan term, interest rate, current status, and repayment schedule.

The Loans table is one of the core transactional tables in the database and serves as the foundation for payment processing, portfolio management, financial reporting, and business intelligence.

---

# Business Purpose

The Loans table manages approved loans and their lifecycle.

Business objectives include:

- Recording approved loans
- Tracking loan balances
- Managing repayment schedules
- Supporting payment processing
- Monitoring loan performance
- Providing portfolio analytics
- Supporting financial reporting

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | loans |
| Module | Loan Management |
| Type | Transaction Table |
| Primary Key | id |
| Parent Table | application |
| Child Table | payments |
| Estimated Volume | High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Loan identifier |
| application_id | BIGINT | No | | ✓ | Approved application |
| loan_status_id | BIGINT | No | | ✓ | Current loan status |
| approved_amount | DECIMAL(15,2) | No | | | Approved loan amount |
| interest_rate | DECIMAL(5,2) | No | | | Annual interest rate (%) |
| loan_term | INTEGER | No | | | Loan duration (months) |
| approval_date | DATE | No | | | Approval date |
| maturity_date | DATE | No | | | Loan maturity date |

---

# Column Descriptions

## id

**Description**

Unique identifier for each loan.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## application_id

**Description**

References the approved loan application.

**References**

```text
application.id
```

**Business Rules**

- Must reference an approved application.
- One approved application should normally create one loan.
- Required field.

---

## loan_status_id

**Description**

Current lifecycle status of the loan.

**References**

```text
loan_status.id
```

Typical values:

- Active
- Paid Off
- Defaulted
- Closed
- Written Off

---

## approved_amount

**Description**

Final loan amount approved after underwriting.

**Business Rules**

- Greater than zero
- Cannot exceed business limits
- May differ from requested amount

---

## interest_rate

**Description**

Annual interest rate applied to the loan.

Example:

```text
12.50
```

Business Rules:

- Positive value
- Defined by lending policy
- Stored as percentage

---

## loan_term

**Description**

Repayment duration in months.

Examples:

- 6
- 12
- 24
- 36
- 60

---

## approval_date

**Description**

Official approval date.

Business Rules:

- Required
- Cannot be after maturity date

---

## maturity_date

**Description**

Scheduled final repayment date.

Business Rules:

- Must be later than approval date
- Calculated using loan term

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique loan identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| application_id | application.id |
| loan_status_id | loan_status.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-One (typically) | Loan originates from an approved application |
| loan_status | Many-to-One | Loan lifecycle status |
| payments | One-to-Many | Loan repayment transactions |

---

# Entity Relationship

```text
application
      │
      │ application_id
      ▼
loans
      │
      ├────────────► loan_status
      │
      └────────────► payments
```

---

# Business Rules

- Every loan must originate from an approved application.
- Every loan must have one valid status.
- Approved amount must be positive.
- Loan term must be greater than zero.
- Maturity date must occur after approval date.
- Loan status must exist in the Loan Status table.
- Every payment must reference an existing loan.

---

# Loan Lifecycle

```text
Application Approved

↓

Loan Created

↓

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
| Approved Application | application_id must reference an approved application |
| Positive Amount | approved_amount > 0 |
| Positive Interest | interest_rate >= 0 |
| Valid Loan Term | loan_term > 0 |
| Valid Dates | maturity_date > approval_date |
| Valid Status | loan_status_id must exist |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | application_id |
| FOREIGN KEY | loan_status_id |
| NOT NULL | Required columns |
| CHECK | Positive amount |
| CHECK | Positive loan term |

Example:

```sql
CHECK (approved_amount > 0)

CHECK (loan_term > 0)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_loans | id | Primary key lookup |
| idx_loans_application | application_id | Application lookup |
| idx_loans_status | loan_status_id | Portfolio reporting |
| idx_loans_approval | approval_date | Time-series reporting |
| idx_loans_maturity | maturity_date | Loan monitoring |

---

# Sample Records

| id | application_id | loan_status_id | approved_amount | interest_rate | loan_term | approval_date | maturity_date |
|---:|---------------:|---------------:|----------------:|--------------:|----------:|---------------|---------------|
| 1 | 102 | 1 | 15000.00 | 12.50 | 24 | 2026-01-15 | 2028-01-15 |
| 2 | 110 | 1 | 8000.00 | 10.00 | 12 | 2026-02-01 | 2027-02-01 |
| 3 | 115 | 2 | 25000.00 | 11.75 | 36 | 2025-03-20 | 2028-03-20 |

---

# Common SQL Queries

## View All Loans

```sql
SELECT *
FROM loans;
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

## Loan Portfolio Value

```sql
SELECT
    SUM(approved_amount) AS total_portfolio
FROM loans;
```

---

## Loans by Status

```sql
SELECT
    ls.status_name,
    COUNT(*) AS total_loans,
    SUM(l.approved_amount) AS portfolio_value
FROM loans l
JOIN loan_status ls
    ON l.loan_status_id = ls.id
GROUP BY ls.status_name
ORDER BY portfolio_value DESC;
```

---

## Monthly Loan Approvals

```sql
SELECT
    DATE_TRUNC('month', approval_date) AS month,
    COUNT(*) AS approved_loans,
    SUM(approved_amount) AS total_amount
FROM loans
GROUP BY month
ORDER BY month;
```

---

## Average Loan Amount

```sql
SELECT
    ROUND(AVG(approved_amount),2) AS average_loan_amount
FROM loans;
```

---

# Reporting Usage

This table is commonly used in:

- Loan Portfolio Dashboard
- Executive Dashboard
- Financial Performance Dashboard
- Loan Monitoring Report
- Credit Risk Dashboard
- Collection Dashboard
- Regulatory Reporting

---

# KPIs Supported

- Total Loans
- Active Loans
- Loan Portfolio Value
- Average Loan Amount
- Outstanding Balance
- Paid-Off Loans
- Default Rate
- Portfolio Growth
- Monthly Loan Disbursement

---

# ETL Considerations

- Load approved applications before loans.
- Validate foreign keys.
- Ensure approved amounts are positive.
- Calculate maturity dates consistently.
- Preserve approval history.
- Standardize interest rate precision.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Financial loan information |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | 10 Years |
| Archive Policy | Annual Archive |
| Deletion Policy | Regulatory Compliance |

---

# Dependencies

### Depends On

- application
- loan_status

### Referenced By

- payments

---

# AI & RAG Notes

The **Loans** table is the central financial entity in the Loan Management System and is essential for AI-assisted analytics. It enables AI systems to:

- Calculate loan portfolio metrics.
- Generate repayment and exposure reports.
- Analyze lending performance.
- Produce SQL for financial reporting.
- Explain relationships between applications, loans, statuses, and payments.
- Support forecasting, risk analysis, and executive dashboards.

---

# Related Documentation

- Application Table
- Loan Status Table
- Payments Table
- Database Schema
- Relationship Matrix
- Loan Lifecycle
- Business Rules
- Executive Dashboard

---

# Summary

The **Loans** table stores all approved loan contracts and serves as the core transactional entity for loan management. It connects approved applications with repayment activities, tracks the complete loan lifecycle, supports portfolio management, financial reporting, and business intelligence, and provides the foundation for AI-assisted analysis and decision-making within the Loan Management System.
