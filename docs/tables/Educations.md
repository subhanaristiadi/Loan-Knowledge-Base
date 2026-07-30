# Educations Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `educations`
>
> **Version:** 2.0

---

# Overview

The **Educations** table is a master reference table that stores standardized education levels used throughout the Loan Management System.

Each customer may optionally be associated with one education level. Standardizing education information improves reporting consistency, customer segmentation, and demographic analysis.

---

# Business Purpose

The Educations table provides a controlled list of education levels for customer profiles.

Business objectives include:

- Standardizing education information
- Preventing inconsistent education values
- Supporting demographic reporting
- Improving customer segmentation
- Enabling educational analytics
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | educations |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Table | users |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Education identifier |
| education_name | VARCHAR(100) | No | | | Education level |

---

# Column Descriptions

## id

**Description**

Unique identifier for each education level.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## education_name

**Description**

Official education level.

Examples:

- Elementary School
- Junior High School
- Senior High School
- Diploma
- Bachelor's Degree
- Master's Degree
- Doctoral Degree

**Business Rules**

- Required
- Must be unique
- Use standardized naming
- Remove leading and trailing spaces

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique education identifier |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| users | One-to-Many | One education level may belong to many customers |

---

# Entity Relationship

```text
educations
      │
      │ id
      ▼
users
```

---

# Business Rules

- Every education level should be unique.
- Customers may optionally have an education level.
- Education values should follow standardized terminology.
- Education records should rarely change.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Name | education_name cannot be NULL |
| Unique Name | No duplicate education levels |
| Standard Naming | Use official education terminology |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| UNIQUE | education_name |
| NOT NULL | education_name |

Example:

```sql
UNIQUE (education_name)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_educations | id | Primary key lookup |
| idx_educations_name | education_name | Fast lookup |

---

# Sample Records

| id | education_name |
|---:|----------------|
| 1 | Elementary School |
| 2 | Junior High School |
| 3 | Senior High School |
| 4 | Diploma |
| 5 | Bachelor's Degree |
| 6 | Master's Degree |
| 7 | Doctoral Degree |

---

# Common SQL Queries

## View All Education Levels

```sql
SELECT *
FROM educations;
```

---

## Customers by Education

```sql
SELECT
    e.education_name,
    COUNT(u.id) AS total_customers
FROM educations e
LEFT JOIN users u
    ON e.id = u.education_id
GROUP BY e.education_name
ORDER BY total_customers DESC;
```

---

## Percentage of Customers by Education

```sql
SELECT
    e.education_name,
    COUNT(u.id) AS total_customers,
    ROUND(
        COUNT(u.id) * 100.0 /
        SUM(COUNT(u.id)) OVER (),
        2
    ) AS percentage
FROM educations e
LEFT JOIN users u
    ON e.id = u.education_id
GROUP BY e.education_name
ORDER BY percentage DESC;
```

---

# Reporting Usage

This table is commonly used in:

- Customer Demographics Dashboard
- Executive Dashboard
- Customer Segmentation Report
- Marketing Analysis
- Loan Approval Analysis
- Credit Risk Analysis

---

# KPIs Supported

- Customers by Education
- Loan Applications by Education
- Approval Rate by Education
- Average Loan Amount by Education
- Customer Distribution by Education

---

# ETL Considerations

- Load education master data before customer data.
- Prevent duplicate education names.
- Preserve standardized naming conventions.
- Validate foreign key references from the Users table.

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

- users

---

# AI & RAG Notes

The **Educations** table provides standardized educational categories that enable AI systems to:

- Generate demographic SQL queries.
- Segment customers by education level.
- Produce education-based reports.
- Support business intelligence dashboards.
- Recommend joins with customer data.
- Improve customer profile analysis.

---

# Related Documentation

- Users Table
- Database Schema
- Relationship Matrix
- Data Dictionary
- Customer Demographics Dashboard

---

# Summary

The **Educations** table is a master reference table containing standardized education levels used across the Loan Management System. It supports consistent customer profiling, demographic reporting, business intelligence, and AI-assisted analytics while maintaining data quality and referential integrity.
