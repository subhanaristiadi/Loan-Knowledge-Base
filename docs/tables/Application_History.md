# Application History Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `application_history`
>
> **Version:** 2.0

---

# Overview

The **Application History** table stores historical records for every loan application.

Each record represents an event in an application's lifecycle and provides a chronological history of application processing.

The table enables tracking of application progress, workflow events, and historical analysis.

---

# Business Purpose

The Application History table maintains the historical records of loan applications.

Business objectives include:

- Recording application history
- Tracking application events
- Supporting audit requirements
- Supporting application timeline analysis
- Providing historical reporting
- Supporting operational analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | application_history |
| Module | Loan Processing |
| Type | Transaction Table |
| Primary Key | application_history_id |
| Parent Table | application |
| Child Tables | None |
| Estimated Volume | Very High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| application_history_id | STRING | No | ✓ | | Unique application history identifier |
| created_date | TIMESTAMP | No | | | Date and time when the history record was created |
| applications_codes | STRING | No | | | Application workflow or event code |
| application_id | BIGINT | No | | ✓ | References the associated application |

---

# Column Descriptions

## application_history_id

**Description**

Unique identifier for each application history record.

**Business Rules**

- Auto-generated
- Cannot be duplicated
- Immutable after creation

---

## created_date

**Description**

Date and time when the history record was created.

**Business Rules**

- Automatically generated
- Required
- Cannot be modified

---

## applications_codes

**Description**

Code representing the application event or workflow stage recorded in the history.

**Business Rules**

- Required
- Stores application processing codes
- Used for historical tracking and reporting

---

## application_id

**Description**

References the loan application associated with this history record.

**References**

```
application.applications_id
```

**Business Rules**

- Required
- Must reference an existing application

---

# Primary Key

| Column | Description |
|---------|-------------|
| application_history_id | Unique application history identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| application_id | application.applications_id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | Many-to-One | Multiple history records belong to one application |

---

# Entity Relationship

```text
application
      │
      │ applications_id
      ▼
application_history
```

---

# Business Rules

- Every history record must belong to an existing application.
- One application may have multiple history records.
- History records are immutable after creation.
- Historical records should never be overwritten.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Application | application_id cannot be NULL |
| Required Event Code | applications_codes cannot be NULL |
| Required Timestamp | created_date cannot be NULL |
| Unique History ID | application_history_id must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | application_history_id |
| FOREIGN KEY | application_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_application_history | application_history_id | Primary key lookup |
| idx_history_application | application_id | Retrieve application history |
| idx_history_created | created_date | Timeline queries |
| idx_history_code | applications_codes | Workflow analysis |

---

# Common SQL Queries

## View All History Records

```sql
SELECT *
FROM `crediu-504100.Crediu.Application History`;
```

---

## Latest History Records

```sql
SELECT *
FROM `crediu-504100.Crediu.Application History`
ORDER BY created_date DESC
LIMIT 100;
```

---

## History for a Specific Application

```sql
SELECT
    application_id,
    applications_codes,
    created_date
FROM `crediu-504100.Crediu.Application History`
WHERE application_id = 1015463
ORDER BY created_date;
```

---

## Number of History Records per Application

```sql
SELECT
    application_id,
    COUNT(*) AS total_history
FROM `crediu-504100.Crediu.Application History`
GROUP BY application_id
ORDER BY total_history DESC;
```

---

# Reporting Usage

This table is frequently used in:

- Application Timeline Report
- Operational Dashboard
- Workflow Analysis
- Audit Report
- Historical Activity Report

---

# KPIs Supported

- Total History Records
- Average History Records per Application
- Workflow Activity Volume
- Daily Application Events
- Historical Processing Trends

---

# ETL Considerations

- Preserve original history IDs.
- Validate application references before loading.
- Preserve event timestamps.
- Never overwrite existing history records.
- Support incremental loading.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains historical loan application records |

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

- application

### Referenced By

- None

---

# AI & RAG Notes

The **Application History** table records historical events associated with loan applications.

It enables AI systems to:

- Generate BigQuery SQL involving application history.
- Explain application timelines.
- Analyze workflow activity.
- Produce historical reports.
- Support audit and operational analysis.

---

# Related Documentation

- Application Table
- Loans Table
- Users Table
- Database Schema
- Relationship Matrix
- Business Rules

---

# Summary

The **Application History** table stores historical records for loan applications, including event codes and creation timestamps. It provides the historical timeline required for auditing, workflow analysis, reporting, and AI-assisted SQL generation.
