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

The **Payment Status** table stores the master list of payment statuses used throughout the Loan Management System.

It serves as a reference table that standardizes the status of every loan payment, ensuring consistent repayment tracking, reporting, and collection activities.

Each payment status is identified by a unique status code.

---

# Business Purpose

The Payment Status table maintains standardized payment status information.

Business objectives include:

- Standardizing payment statuses
- Supporting repayment tracking
- Supporting collection processes
- Supporting payment reporting
- Preventing inconsistent status values
- Supporting business analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | payment_status |
| Module | Master Data |
| Type | Master Table |
| Primary Key | payment_status_code |
| Parent Table | None |
| Child Tables | payments |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| payment_status_code | INTEGER | No | ✓ | | Unique payment status identifier |
| payment | STRING | No | | | Payment status name |

---

# Column Descriptions

## payment_status_code

**Description**

Unique identifier for each payment status.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## payment

**Description**

Descriptive name of the payment status.

Example values:

- grace
- ontime
- notpaid
- late

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized payment status names

---

# Primary Key

| Column | Description |
|---------|-------------|
| payment_status_code | Unique payment status identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| payments | One-to-Many | One payment status can be referenced by many payment records |

---

# Entity Relationship

```text
payment_status
       │
       │ payment_status_code
       ▼
payments
```

---

# Business Rules

- Every payment status must have a unique identifier.
- Payment status names should be standardized.
- Every payment should reference a valid payment status.
- Payment status records should not be deleted if they are referenced by payment transactions.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Status Code | payment_status_code cannot be NULL |
| Required Status Name | payment cannot be NULL |
| Unique Status Code | payment_status_code must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | payment_status_code |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_payment_status | payment_status_code | Primary key lookup |
| idx_payment_status_name | payment | Payment status search |

---

# Common SQL Queries

## View All Payment Statuses

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Status`;
```

---

## Count Payment Statuses

```sql
SELECT
    COUNT(*) AS total_payment_statuses
FROM `crediu-504100.Crediu.Payment Status`;
```

---

## Find a Payment Status

```sql
SELECT *
FROM `crediu-504100.Crediu.Payment Status`
WHERE payment = 'ontime';
```

---

# Reporting Usage

This table is frequently used in:

- Payment Dashboard
- Collection Dashboard
- Payment Status Distribution
- Collection Performance Report
- Executive Dashboard

---

# KPIs Supported

- On-Time Payment Rate
- Late Payment Rate
- Unpaid Payment Rate
- Grace Period Payment Rate
- Payment Status Distribution

---

# ETL Considerations

- Preserve payment status codes.
- Prevent duplicate status codes.
- Standardize payment status names.
- Validate payment status references before loading payment data.

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

The **Payment Status** table provides standardized payment status information used throughout the Loan Management System.

It enables AI systems to:

- Generate BigQuery SQL involving payment status data.
- Analyze repayment performance.
- Produce payment status reports.
- Join payment status information with payment transactions.
- Support collection and operational analytics.

---

# Related Documentation

- Payments Table
- Payment Methods Table
- Loans Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Payment Status** table is a master reference table containing standardized payment statuses. It ensures consistent classification of payment transactions, supports repayment monitoring and reporting, and provides a common reference for AI-assisted SQL generation.
