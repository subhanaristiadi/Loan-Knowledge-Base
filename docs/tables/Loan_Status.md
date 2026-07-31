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

The **Loan Status** table stores the master list of loan statuses used throughout the Loan Management System.

It serves as a reference table that standardizes the status assigned to every loan, ensuring consistent reporting and business processes.

Each loan status is identified by a unique status code.

---

# Business Purpose

The Loan Status table maintains standardized loan status information.

Business objectives include:

- Standardizing loan statuses
- Supporting loan lifecycle management
- Supporting operational reporting
- Preventing inconsistent status values
- Supporting business analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | loan_status |
| Module | Master Data |
| Type | Master Table |
| Primary Key | loan_status_code |
| Parent Table | None |
| Child Tables | loans |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| loan_status_code | INTEGER | No | ✓ | | Unique loan status code |
| loan_status | STRING | No | | | Loan status name |

---

# Column Descriptions

## loan_status_code

**Description**

Unique identifier for each loan status.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## loan_status

**Description**

Descriptive name of the loan status.

Example values:

- Paid_Off
- Not_Paid_Off

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized status names

---

# Primary Key

| Column | Description |
|---------|-------------|
| loan_status_code | Unique loan status identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| loans | One-to-Many | One loan status can be assigned to many loans |

---

# Entity Relationship

```text
loan_status
      │
      │ loan_status_code
      ▼
loans
```

---

# Business Rules

- Every loan status must have a unique code.
- Loan status names should be standardized.
- Every loan should reference a valid loan status.
- Loan status records should not be deleted if referenced by loan records.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Status Code | loan_status_code cannot be NULL |
| Required Status Name | loan_status cannot be NULL |
| Unique Status Code | loan_status_code must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | loan_status_code |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_loan_status | loan_status_code | Primary key lookup |
| idx_loan_status_name | loan_status | Loan status search |

---

# Common SQL Queries

## View All Loan Statuses

```sql
SELECT *
FROM `crediu-504100.Crediu.Loan Status`;
```

---

## Count Loan Statuses

```sql
SELECT
    COUNT(*) AS total_statuses
FROM `crediu-504100.Crediu.Loan Status`;
```

---

## Find a Loan Status

```sql
SELECT *
FROM `crediu-504100.Crediu.Loan Status`
WHERE loan_status = 'Paid_Off';
```

---

# Reporting Usage

This table is frequently used in:

- Loan Portfolio Dashboard
- Loan Status Distribution
- Collection Report
- Executive Dashboard
- Loan Performance Analysis

---

# KPIs Supported

- Paid Off Loans
- Not Paid Off Loans
- Loan Status Distribution
- Portfolio Performance

---

# ETL Considerations

- Preserve status codes.
- Prevent duplicate status codes.
- Standardize status names.
- Validate loan status references before loading loan data.

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

- loans

---

# AI & RAG Notes

The **Loan Status** table provides standardized loan status information used throughout the Loan Management System.

It enables AI systems to:

- Generate BigQuery SQL involving loan status data.
- Analyze loan portfolio performance.
- Produce loan status distribution reports.
- Join loan status information with loan records.
- Support operational and business analytics.

---

# Related Documentation

- Loans Table
- Application Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Loan Status** table is a master reference table containing standardized loan statuses. It ensures consistent classification of loan records, supports reporting and analytics, and provides a common reference for AI-assisted SQL generation.
