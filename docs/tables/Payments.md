# Payments Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `payments`
>
> **Version:** 2.0

---

# Overview

The **Payments** table stores every repayment transaction made against approved loans.

Each payment record represents a financial transaction associated with a loan and contains information such as the payment amount, payment date, payment method, and payment status.

This table is the primary source for repayment tracking, collection analysis, cash flow reporting, and loan performance monitoring.

---

# Business Purpose

The Payments table records all loan repayment transactions.

Business objectives include:

- Recording loan repayments
- Tracking outstanding balances
- Monitoring collection performance
- Supporting financial reporting
- Measuring repayment behavior
- Enabling payment analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payments |
| Module | Payment Management |
| Type | Transaction Table |
| Primary Key | id |
| Parent Table | loans |
| Child Tables | None |
| Estimated Volume | Very High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Payment identifier |
| loan_id | BIGINT | No | | ✓ | Loan reference |
| payment_method_id | BIGINT | No | | ✓ | Payment method |
| payment_status_id | BIGINT | No | | ✓ | Payment status |
| payment_amount | DECIMAL(15,2) | No | | | Amount paid |
| payment_date | DATE | No | | | Payment date |

---

# Column Descriptions

## id

**Description**

Unique identifier for each payment transaction.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## loan_id

**Description**

References the loan receiving the payment.

**References**

```text
loans.id
```

**Business Rules**

- Loan must exist.
- Required field.
- Foreign key enforced.

---

## payment_method_id

**Description**

References the payment method used.

**References**

```text
payment_methods.id
```

Example values:

- Bank Transfer
- Cash
- Credit Card
- Debit Card
- Mobile Banking

---

## payment_status_id

**Description**

References the payment status.

**References**

```text
payment_status.id
```

Typical values:

- Pending
- Paid
- Late
- Failed
- Cancelled

---

## payment_amount

**Description**

Amount received for the payment.

**Business Rules**

- Greater than zero.
- Required.
- Currency follows organizational standards.

---

## payment_date

**Description**

Date the payment was received.

**Business Rules**

- Required.
- Cannot be in the future.
- Should not occur before the loan approval date.

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique payment identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| loan_id | loans.id |
| payment_method_id | payment_methods.id |
| payment_status_id | payment_status.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| loans | Many-to-One | Payment belongs to one loan |
| payment_methods | Many-to-One | Payment uses one payment method |
| payment_status | Many-to-One | Payment has one payment status |

---

# Entity Relationship

```text
loans
   │
   │ loan_id
   ▼
payments
   │
   ├────────────► payment_methods
   │
   └────────────► payment_status
```

---

# Business Rules

- Every payment belongs to one loan.
- Payment amount must be greater than zero.
- Every payment must have a payment method.
- Every payment must have a payment status.
- Payment cannot exist without an associated loan.
- Payment history should never be deleted.
- Multiple payments may exist for a single loan.

---

# Payment Lifecycle

```text
Loan Created

↓

Scheduled Payment

↓

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
| Valid Loan | loan_id must exist |
| Valid Method | payment_method_id must exist |
| Valid Status | payment_status_id must exist |
| Positive Amount | payment_amount > 0 |
| Valid Date | payment_date cannot be in the future |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | loan_id |
| FOREIGN KEY | payment_method_id |
| FOREIGN KEY | payment_status_id |
| NOT NULL | Required columns |
| CHECK | Positive payment amount |

Example:

```sql
CHECK (payment_amount > 0)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payments | id | Primary key lookup |
| idx_payments_loan | loan_id | Loan lookup |
| idx_payments_status | payment_status_id | Payment reporting |
| idx_payments_method | payment_method_id | Method analysis |
| idx_payments_date | payment_date | Time-series reporting |

---

# Sample Records

| id | loan_id | payment_method_id | payment_status_id | payment_amount | payment_date |
|---:|--------:|------------------:|------------------:|---------------:|--------------|
| 1 | 101 | 1 | 2 | 850.00 | 2026-01-30 |
| 2 | 101 | 2 | 2 | 850.00 | 2026-02-28 |
| 3 | 102 | 1 | 3 | 600.00 | 2026-03-31 |

---

# Common SQL Queries

## View All Payments

```sql
SELECT *
FROM payments;
```

---

## Total Payments Received

```sql
SELECT
    SUM(payment_amount) AS total_received
FROM payments;
```

---

## Payments by Status

```sql
SELECT
    ps.status_name,
    COUNT(*) AS total_payments,
    SUM(p.payment_amount) AS total_amount
FROM payments p
JOIN payment_status ps
    ON p.payment_status_id = ps.id
GROUP BY ps.status_name;
```

---

## Payments by Method

```sql
SELECT
    pm.method_name,
    COUNT(*) AS total_transactions,
    SUM(p.payment_amount) AS total_amount
FROM payments p
JOIN payment_methods pm
    ON p.payment_method_id = pm.id
GROUP BY pm.method_name
ORDER BY total_amount DESC;
```

---

## Monthly Collections

```sql
SELECT
    DATE_TRUNC('month', payment_date) AS month,
    SUM(payment_amount) AS collection_amount
FROM payments
GROUP BY month
ORDER BY month;
```

---

## Loan Payment History

```sql
SELECT
    p.payment_date,
    p.payment_amount,
    ps.status_name
FROM payments p
JOIN payment_status ps
    ON p.payment_status_id = ps.id
WHERE p.loan_id = 101
ORDER BY p.payment_date;
```

---

# Reporting Usage

This table is commonly used in:

- Payment Dashboard
- Collection Dashboard
- Cash Flow Dashboard
- Executive Dashboard
- Loan Repayment Report
- Collection Performance Report
- Delinquency Report

---

# KPIs Supported

- Total Collections
- Collection Rate
- Monthly Collections
- Average Payment Amount
- Payment Success Rate
- Late Payment Rate
- Outstanding Balance
- Collection Performance
- Repayment Trend

---

# ETL Considerations

- Load loans before payment transactions.
- Validate all foreign key references.
- Prevent duplicate payment records.
- Standardize payment dates.
- Preserve transaction history.
- Reject negative payment amounts.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Financial transaction data |

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

- loans
- payment_methods
- payment_status

### Referenced By

None

---

# AI & RAG Notes

The **Payments** table is the primary source of repayment and collection information within the Loan Management System. It enables AI systems to:

- Calculate collection rates.
- Analyze repayment behavior.
- Generate cash flow reports.
- Produce SQL for payment analysis.
- Support delinquency monitoring.
- Build executive dashboards and financial performance reports.

---

# Related Documentation

- Loans Table
- Payment Status Table
- Payment Methods Table
- Database Schema
- Relationship Matrix
- Collection Dashboard
- Business Rules

---

# Summary

The **Payments** table records every repayment transaction associated with approved loans. As the primary source of financial transaction data, it supports repayment tracking, collection monitoring, cash flow analysis, portfolio management, regulatory reporting, and AI-assisted analytics while ensuring accurate relationships with loans, payment methods, and payment statuses.
