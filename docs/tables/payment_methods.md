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

The **Payment Methods** table stores the master list of payment methods available for loan repayments.

It serves as a reference table that standardizes payment channels across the Loan Management System, ensuring consistent payment processing and reporting.

Each payment method is identified by a unique identifier.

---

# Business Purpose

The Payment Methods table maintains standardized payment method information.

Business objectives include:

- Standardizing payment methods
- Supporting loan repayment processing
- Supporting payment reporting
- Preventing inconsistent payment method values
- Supporting business analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payment_methods |
| Module | Master Data |
| Type | Master Table |
| Primary Key | payment_method_id |
| Parent Table | None |
| Child Tables | payments |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| payment_method_id | INTEGER | No | ✓ | | Unique payment method identifier |
| payment_method | STRING | No | | | Payment method name |

---

# Column Descriptions

## payment_method_id

**Description**

Unique identifier for each payment method.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## payment_method

**Description**

Name of the payment method available for loan repayment.

Example values:

- Biller Services
- E-Wallet
- Inter-Bank Transfer
- Intra-Bank Transfer

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized payment method names

---

# Primary Key

| Column | Description |
|---------|-------------|
| payment_method_id | Unique payment method identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| payments | One-to-Many | One payment method can be referenced by many payment transactions |

---

# Entity Relationship

```text
payment_methods
        │
        │ payment_method_id
        ▼
payments
```

---

# Business Rules

- Every payment method must have a unique identifier.
- Payment method names should be standardized.
- Payment transactions should reference a valid payment method.
- Payment methods should not be deleted if they are referenced by payment transactions.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Method ID | payment_method_id cannot be NULL |
| Required Method Name | payment_method cannot be NULL |
| Unique Method ID | payment_method_id must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | payment_method_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payment_methods | payment_method_id | Primary key lookup |
| idx_payment_method_name | payment_method | Payment method search |

---

# Common SQL Queries

## View All Payment Methods

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Methods`;
```

---

## Count Payment Methods

```sql
SELECT
    COUNT(*) AS total_payment_methods
FROM `crediu-504100.Crediu.Payment Methods`;
```

---

## Search Payment Method

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Methods`
WHERE payment_method = 'E-Wallet';
```

---

# Reporting Usage

This table is frequently used in:

- Payment Dashboard
- Payment Method Distribution
- Loan Repayment Analysis
- Executive Dashboard

---

# KPIs Supported

- Total Payment Methods
- Payment Method Usage
- Payment Channel Distribution
- Digital Payment Adoption

---

# ETL Considerations

- Preserve payment method identifiers.
- Prevent duplicate payment methods.
- Standardize payment method names.
- Validate payment method references before loading payment transactions.

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

The **Payment Methods** table provides standardized payment method information used throughout the Loan Management System.

It enables AI systems to:

- Generate BigQuery SQL involving payment methods.
- Analyze payment channel usage.
- Produce payment distribution reports.
- Join payment method information with payment transactions.
- Support repayment analytics.

---

# Related Documentation

- Payments Table
- Loans Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Payment Methods** table is a master reference table containing standardized loan repayment methods. It ensures consistent payment channel classification, supports reporting and analytics, and provides a common reference for AI-assisted SQL generation.
