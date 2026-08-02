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

The **Educations** table stores the master list of education levels used throughout the Loan Management System.

It serves as a reference table that standardizes applicant education information and ensures consistent data across loan applications and customer records.

Each education level is uniquely identified by an education code.

---

# Business Purpose

The Educations table maintains standardized education level data.

Business objectives include:

- Standardizing education levels
- Supporting customer profile information
- Supporting demographic analysis
- Preventing inconsistent education values
- Supporting reporting and analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | educations |
| Module | Master Data |
| Type | Master Table |
| Primary Key | education_code |
| Parent Table | None |
| Child Tables | application |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| education_code | INTEGER | No | ✓ | | Unique education level code |
| education | STRING | No | | | Education level name |

---

# Column Descriptions

## education_code

**Description**

Unique identifier for each education level.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## education

**Description**

Name of the education level.

Example values:

- SD
- SMP
- SMA
- Kuliah - Perguruan Tinggi
- Pasca Sarjana

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized education names

---

# Primary Key

| Column | Description |
|---------|-------------|
| education_code | Unique education level identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-Many | One education level can be referenced by many applications |

---

# Entity Relationship

```text
educations
      │
      │ education_code
      ▼
application
```

---

# Business Rules

- Every education level must have a unique code.
- Education names should be standardized.
- Applications should reference a valid education code.
- Education records should not be deleted if referenced by applications.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Code | education_code cannot be NULL |
| Required Education | education cannot be NULL |
| Unique Code | education_code must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | education_code |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_educations | education_code | Primary key lookup |
| idx_education_name | education | Education search |

---

# Common SQL Queries

## View All Education Levels

```sql
SELECT *
FROM `crediu-504100.Crediu.Educations`;
```

---

## Count Education Levels

```sql
SELECT
    COUNT(*) AS total_education_levels
FROM `crediu-504100.Crediu.Educations`;
```

---

## Search Education Level

```sql
SELECT *
FROM `crediu-504100.Crediu.Educations`
WHERE education = 'SMA';
```

---

# Reporting Usage

This table is frequently used in:

- Applicant Demographics
- Customer Profile Report
- Education Distribution
- Executive Dashboard

---

# KPIs Supported

- Total Education Levels
- Applications by Education Level
- Customer Distribution by Education
- Education Demographics

---

# ETL Considerations

- Preserve education codes.
- Prevent duplicate education codes.
- Standardize education names.
- Validate education references before loading applications.

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

The **Educations** table provides standardized education level information used throughout the loan application process.

It enables AI systems to:

- Generate BigQuery SQL involving education data.
- Analyze applicant demographics.
- Produce education distribution reports.
- Join education information with application records.
- Support customer profile analytics.

---

# Related Documentation

- Application Table
- Users Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Educations** table is a master reference table containing standardized education levels. It supports consistent data entry, customer demographic analysis, reporting, and AI-assisted SQL generation by providing a common reference for applicant education information.
