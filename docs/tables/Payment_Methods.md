# Payment Methods Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `payment_methods`
>
> **Version:** 2.0

---

# Overview

The **Payment Methods** table stores the available payment methods that customers can use to repay their loans.

It serves as a master reference table that standardizes payment method information across the loan management system.

Each payment method defines how loan repayments are collected or transferred.

---

# Business Purpose

The Payment Methods table maintains the list of supported repayment methods.

Business objectives include:

- Standardizing payment methods
- Supporting repayment processing
- Reducing data inconsistency
- Supporting reporting and analytics
- Managing available payment channels

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payment_methods |
| Module | Payment |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Tables | payments |
| Estimated Volume | Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Payment method ID |
| payment_method_name | VARCHAR(100) | No | | | Payment method name |
| description | TEXT | Yes | | | Description of the payment method |
| is_active | BOOLEAN | No | | | Indicates whether the payment method is active |
| created_at | TIMESTAMP | No | | | Record creation timestamp |
| updated_at | TIMESTAMP | Yes | | | Last update timestamp |

---

# Column Descriptions

## id

**Description**

Unique identifier for each payment method.

**Business Rules**

- Auto-generated
- Cannot be duplicated
- Immutable after creation

---

## payment_method_name

**Description**

The name of the payment method available to customers.

Examples include:

- Bank Transfer
- Virtual Account
- Auto Debit
- E-Wallet
- Cash
- QRIS

**Business Rules**

- Required
- Must be unique
- Cannot be empty

---

## description

**Description**

Additional information describing the payment method.

**Business Rules**

- Optional
- Used for internal documentation

---

## is_active

**Description**

Indicates whether the payment method is currently available.

Typical values:

- TRUE
- FALSE

---

## created_at

**Description**

Timestamp when the payment method was created.

**Business Rules**

- Automatically generated
- Required

---

## updated_at

**Description**

Timestamp of the most recent update.

**Business Rules**

- Updated whenever the record changes

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique payment method identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| payments | One-to-Many | One payment method can be used by many payment records |

---

# Entity Relationship

```text
payment_methods
        │
        │ id
        ▼
payments
```

---

# Business Rules

- Payment method names must be unique.
- Only active payment methods may be used for new payments.
- Historical payment records must retain their original payment method.
- Payment methods should not be deleted if already referenced by payment transactions.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Unique Name | payment_method_name must be unique |
| Required Name | payment_method_name cannot be NULL |
| Active Flag | is_active must contain TRUE or FALSE |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| UNIQUE | payment_method_name |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payment_methods | id | Primary key lookup |
| idx_payment_method_name | payment_method_name | Search payment methods |
| idx_payment_method_active | is_active | Active payment methods |

---

# Sample Records

| id | payment_method_name | is_active |
|----|----------------------|-----------|
| 1 | Bank Transfer | TRUE |
| 2 | Virtual Account | TRUE |
| 3 | Auto Debit | TRUE |
| 4 | QRIS | TRUE |
| 5 | Cash | FALSE |

---

# Common SQL Queries

## View All Payment Methods

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Methods`;
```

---

## Active Payment Methods

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Methods`
WHERE is_active = TRUE;
```

---

## Count Active Payment Methods

```sql
SELECT
    COUNT(*) AS total_active_methods
FROM `crediu-504100.Crediu.Payment Methods`
WHERE is_active = TRUE;
```

---

# Reporting Usage

This table is frequently used in:

- Payment Dashboard
- Payment Method Distribution
- Loan Repayment Report
- Payment Analytics
- Executive Dashboard

---

# KPIs Supported

- Active Payment Methods
- Payment Method Usage
- Payment Channel Distribution
- Repayment Method Adoption

---

# ETL Considerations

- Preserve payment method IDs.
- Prevent duplicate payment method names.
- Maintain active status correctly.
- Update timestamps on modification.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Internal | Master reference data |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | Permanent |
| Archive Policy | Not Applicable |
| Deletion Policy | Soft Delete Recommended |

---

# Dependencies

### Depends On

- None

### Referenced By

- payments

---

# AI & RAG Notes

The **Payment Methods** table is a master reference table used to identify how loan repayments are made.

It enables AI systems to:

- Explain available payment methods.
- Generate BigQuery SQL involving repayment channels.
- Analyze payment method usage.
- Produce repayment reports.
- Support payment-related analytics.

---

# Related Documentation

- Payments Table
- Loans Table
- Users Table
- Database Schema
- Relationship Matrix
- Business Rules

---

# Summary

The **Payment Methods** table stores the master list of supported loan repayment methods. It standardizes payment channels across the system, supports repayment processing, reporting, and analytics, and serves as the reference table for all payment transactions.
