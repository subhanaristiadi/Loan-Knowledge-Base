# Reason Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `reason`
>
> **Version:** 2.0

---

# Overview

The **Reason** table stores the master list of loan purposes used throughout the Loan Management System.

It serves as a reference table that standardizes the reasons customers apply for loans, ensuring consistent classification across loan applications, reporting, and business analytics.

Each loan purpose is identified by a unique reason identifier.

---

# Business Purpose

The Reason table maintains standardized loan purpose information.

Business objectives include:

- Standardizing loan purposes
- Supporting loan application processing
- Supporting lending analytics
- Preventing inconsistent loan purpose values
- Supporting business reporting

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | reason |
| Module | Master Data |
| Type | Master Table |
| Primary Key | reason_id |
| Parent Table | None |
| Child Tables | application |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| reason_id | INTEGER | No | ✓ | | Unique loan purpose identifier |
| reason_for_loan | STRING | No | | | Standardized loan purpose |

---

# Column Descriptions

## reason_id

**Description**

Unique identifier for each loan purpose.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## reason_for_loan

**Description**

Standardized description of the customer's reason for requesting a loan.

Example values:

- Capital
- Daily Needs
- Education
- Emergency
- Entertainment

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized loan purposes

---

# Primary Key

| Column | Description |
|---------|-------------|
| reason_id | Unique loan purpose identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-Many | One loan purpose can be referenced by many applications |

---

# Entity Relationship

```text
reason
   │
   │ reason_id
   ▼
application
```

---

# Business Rules

- Every loan purpose must have a unique identifier.
- Loan purpose names should be standardized.
- Every application should reference a valid loan purpose.
- Loan purpose records should not be deleted if they are referenced by loan applications.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Reason ID | reason_id cannot be NULL |
| Required Loan Purpose | reason_for_loan cannot be NULL |
| Unique Reason ID | reason_id must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | reason_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_reason | reason_id | Primary key lookup |
| idx_reason_name | reason_for_loan | Loan purpose search |

---

# Common SQL Queries

## View All Loan Purposes

```sql
SELECT *
FROM `crediu-504100.Crediu.Reason`;
```

---

## Count Loan Purposes

```sql
SELECT
    COUNT(*) AS total_loan_purposes
FROM `crediu-504100.Crediu.Reason`;
```

---

## Applications by Loan Purpose

```sql
SELECT
    r.reason_for_loan,
    COUNT(a.applications_id) AS total_applications
FROM `crediu-504100.Crediu.Reason` r
LEFT JOIN `crediu-504100.Crediu.Application` a
    ON r.reason_id = a.reason_id
GROUP BY r.reason_for_loan
ORDER BY total_applications DESC;
```

---

# Reporting Usage

This table is frequently used in:

- Loan Purpose Dashboard
- Loan Demand Analysis
- Customer Borrowing Report
- Executive Dashboard

---

# KPIs Supported

- Applications by Loan Purpose
- Most Popular Loan Purpose
- Loan Purpose Distribution
- Customer Borrowing Trends

---

# ETL Considerations

- Preserve reason identifiers.
- Prevent duplicate loan purposes.
- Standardize loan purpose names.
- Validate reason references before loading application data.

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

- application

---

# AI & RAG Notes

The **Reason** table provides standardized loan purpose information used throughout the Loan Management System.

It enables AI systems to:

- Generate BigQuery SQL involving loan purposes.
- Analyze customer borrowing reasons.
- Produce loan purpose distribution reports.
- Join loan purpose information with loan applications.
- Support lending and business analytics.

---

# Related Documentation

- Application Table
- Users Table
- Loans Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Reason** table is a master reference table containing standardized loan purposes. It provides consistent classification for customer loan applications, supports reporting and analytics, and serves as the reference table for the `application.reason_id` foreign key in AI-assisted SQL generation.
