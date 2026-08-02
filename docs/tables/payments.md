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

The **Payments** table stores loan repayment transactions for every loan in the Loan Management System.

Each record represents a scheduled or completed installment payment and contains information about payment amounts, due dates, payment status, and payment methods.

The table serves as the primary source for repayment tracking, collection monitoring, and financial reporting.

---

# Business Purpose

The Payments table records loan repayment information.

Business objectives include:

- Recording loan installment payments
- Tracking payment schedules
- Monitoring overdue payments
- Recording payment methods
- Supporting collection activities
- Supporting financial reporting and analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payments |
| Module | Payment |
| Type | Transaction Table |
| Primary Key | payment_id |
| Parent Table | loans |
| Child Tables | None |
| Estimated Volume | Very High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| payment_id | BIGINT | No | ✓ | | Unique payment identifier |
| loan_id | STRING | No | | ✓ | References the associated loan |
| payment_number | INTEGER | No | | | Installment sequence number |
| payment_status_code | INTEGER | No | | ✓ | References the payment status |
| payment_timestamp | TIMESTAMP | Yes | | | Date and time the payment was made |
| due_timestamp | TIMESTAMP | No | | | Scheduled payment due date |
| principal_amount | NUMERIC | No | | | Principal portion of the installment |
| interest_amount | NUMERIC | No | | | Interest portion of the installment |
| late_fee | NUMERIC | No | | | Late payment fee |
| due_amount | NUMERIC | No | | | Total amount due |
| paid_amount | NUMERIC | No | | | Amount actually paid |
| payment_method_id | INTEGER | Yes | | ✓ | References the payment method |

---

# Column Descriptions

## payment_id

**Description**

Unique identifier for each payment transaction.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## loan_id

**Description**

References the loan associated with the payment.

**References**

```
loans.loan_id
```

---

## payment_number

**Description**

Sequential installment number for the loan.

---

## payment_status_code

**Description**

References the current payment status.

**References**

```
payment_status.payment_status_code
```

---

## payment_timestamp

**Description**

Date and time when the payment was completed.

---

## due_timestamp

**Description**

Scheduled due date and time for the payment.

---

## principal_amount

**Description**

Principal amount due for the installment.

---

## interest_amount

**Description**

Interest amount charged for the installment.

---

## late_fee

**Description**

Late payment penalty charged when applicable.

---

## due_amount

**Description**

Total amount that should be paid for the installment.

---

## paid_amount

**Description**

Actual amount received from the customer.

---

## payment_method_id

**Description**

References the payment method used for the transaction.

**References**

```
payment_methods.payment_method_id
```

---

# Primary Key

| Column | Description |
|---------|-------------|
| payment_id | Unique payment identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| loan_id | loans.loan_id |
| payment_status_code | payment_status.payment_status_code |
| payment_method_id | payment_methods.payment_method_id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| loans | Many-to-One | Many payments belong to one loan |
| payment_status | Many-to-One | Many payments share one payment status |
| payment_methods | Many-to-One | Many payments may use the same payment method |

---

# Entity Relationship

```text
loans
   │
   │ loan_id
   ▼
payments
   ├────────────► payment_status
   └────────────► payment_methods
```

---

# Business Rules

- Every payment must belong to one loan.
- Payment numbers should be sequential within a loan.
- Due amount should equal principal amount, interest amount, and applicable late fees.
- Paid amount cannot be negative.
- Payment methods should reference valid master data.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Loan | loan_id cannot be NULL |
| Required Payment Number | payment_number cannot be NULL |
| Required Due Date | due_timestamp cannot be NULL |
| Positive Principal | principal_amount >= 0 |
| Positive Interest | interest_amount >= 0 |
| Positive Due Amount | due_amount >= 0 |
| Positive Paid Amount | paid_amount >= 0 |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | payment_id |
| FOREIGN KEY | loan_id |
| FOREIGN KEY | payment_status_code |
| FOREIGN KEY | payment_method_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payments | payment_id | Primary key lookup |
| idx_payments_loan | loan_id | Loan lookup |
| idx_payments_status | payment_status_code | Status reporting |
| idx_payments_due | due_timestamp | Due date analysis |
| idx_payments_method | payment_method_id | Payment method analysis |

---

# Common SQL Queries

## View All Payments

```sql
SELECT *
FROM `crediu-504100.Crediu.Payments`;
```

---

## Total Paid Amount

```sql
SELECT
    SUM(paid_amount) AS total_paid
FROM `crediu-504100.Crediu.Payments`;
```

---

## Outstanding Amount

```sql
SELECT
    SUM(due_amount - paid_amount) AS outstanding_amount
FROM `crediu-504100.Crediu.Payments`;
```

---

## Payments by Method

```sql
SELECT
    payment_method_id,
    COUNT(*) AS total_payments
FROM `crediu-504100.Crediu.Payments`
GROUP BY payment_method_id;
```

---

## Payments by Status

```sql
SELECT
    payment_status_code,
    COUNT(*) AS total_payments
FROM `crediu-504100.Crediu.Payments`
GROUP BY payment_status_code;
```

---

# Reporting Usage

This table is frequently used in:

- Payment Dashboard
- Collection Report
- Outstanding Balance Report
- Payment Performance Dashboard
- Executive Dashboard

---

# KPIs Supported

- Total Payments
- Total Amount Paid
- Outstanding Amount
- Collection Rate
- Late Fee Collected
- Payment Method Distribution

---

# ETL Considerations

- Preserve payment identifiers.
- Validate loan references.
- Validate payment status references.
- Validate payment method references.
- Preserve payment timestamps.
- Prevent duplicate payment records.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer repayment information |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | 7 Years |
| Archive Policy | Annual |
| Deletion Policy | Regulatory Compliance |

---

# Dependencies

### Depends On

- loans
- payment_status
- payment_methods

### Referenced By

- None

---

# AI & RAG Notes

The **Payments** table contains detailed loan repayment transactions.

It enables AI systems to:

- Generate BigQuery SQL involving payment transactions.
- Analyze repayment performance.
- Calculate outstanding balances.
- Monitor collection activities.
- Analyze payment methods and payment status.
- Produce financial and operational reports.

---

# Related Documentation

- Loans Table
- Payment Status Table
- Payment Methods Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Payments** table stores all loan repayment transactions, including installment schedules, payment amounts, payment status, payment methods, and due dates. It serves as the primary transaction table for repayment tracking, financial reporting, collection analysis, and AI-assisted SQL generation.
