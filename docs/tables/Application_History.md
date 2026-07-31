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

The **Application History** table stores every status change and activity that occurs throughout the lifecycle of a loan application.

It provides a complete audit trail of each application, allowing users to monitor how an application progresses from submission to its final outcome.

Each history record represents a single event associated with an application, including status changes, timestamps, and operational remarks.

---

# Business Purpose

The Application History table records every change made to a loan application.

Business objectives include:

- Tracking application progress
- Recording status transitions
- Supporting audit and compliance requirements
- Maintaining historical application events
- Providing application timelines
- Supporting operational reporting and analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | application_history |
| Module | Loan Processing |
| Type | Transaction Table |
| Primary Key | id |
| Parent Table | application |
| Child Tables | None |
| Estimated Volume | Very High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | History record ID |
| application_id | BIGINT | No | | ✓ | Loan application |
| status | VARCHAR(30) | No | | | Application status |
| remarks | TEXT | Yes | | | Status remarks |
| created_at | TIMESTAMP | No | | | Event timestamp |
| created_by | BIGINT | Yes | | | User or system creating the record |

---

# Column Descriptions

## id

**Description**

Unique identifier for each application history record.

**Business Rules**

- Auto-generated
- Cannot be duplicated
- Immutable after creation

---

## application_id

**Description**

References the application associated with this history record.

**References**

```
application.id
```

**Business Rules**

- Must reference an existing application
- Required field
- Foreign key enforced

---

## status

**Description**

Application status recorded at the time of the event.

Typical values include:

- Submitted
- Under Review
- Approved
- Rejected
- Cancelled
- Disbursed

---

## remarks

**Description**

Additional notes explaining the status change or operational activity.

**Business Rules**

- Optional
- May be entered manually or generated automatically

---

## created_at

**Description**

Date and time when the history event was recorded.

**Business Rules**

- Required
- Automatically generated
- Cannot be modified after creation

---

## created_by

**Description**

User or system responsible for creating the history record.

**Business Rules**

- May reference an internal system user
- Can be NULL for automated events

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique application history identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| application_id | application.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | Many-to-One | History belongs to one application |

---

# Entity Relationship

```text
application
      │
      │ application_id
      ▼
application_history
```

---

# Business Rules

- Every history record must belong to one application.
- An application may have multiple history records.
- Every status transition should generate a history record.
- History records cannot be deleted.
- History records represent immutable audit events.

---

# Status Lifecycle

```text
Submitted

↓

Under Review

↓

Approved

↓

Loan Created

OR

Rejected

OR

Cancelled
```

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Application | application_id cannot be NULL |
| Valid Status | Status must match allowed values |
| Required Timestamp | created_at cannot be NULL |
| Immutable History | Existing history records cannot be modified |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | application_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_application_history | id | Primary key lookup |
| idx_history_application | application_id | Application history lookup |
| idx_history_status | status | Status reporting |
| idx_history_created_at | created_at | Timeline queries |

---

# Sample Records

| id | application_id | status | remarks | created_at |
|----|----------------|---------|---------|---------------------|
| 1 | 1001 | Submitted | Initial application submitted | 2026-01-15 08:30:00 |
| 2 | 1001 | Under Review | Assigned to credit analyst | 2026-01-15 09:10:00 |
| 3 | 1001 | Approved | Credit approved | 2026-01-15 14:25:00 |

---

# Common SQL Queries

## View Application History

```sql
SELECT *
FROM `crediu-504100.Crediu.Application History`;
```

---

## Latest History Records

```sql
SELECT *
FROM `crediu-504100.Crediu.Application History`
ORDER BY created_at DESC
LIMIT 100;
```

---

## History for a Specific Application

```sql
SELECT
    application_id,
    status,
    remarks,
    created_at
FROM `crediu-504100.Crediu.Application History`
WHERE application_id = 1001
ORDER BY created_at;
```

---

## Latest Status per Application

```sql
SELECT
    application_id,
    status,
    created_at
FROM `crediu-504100.Crediu.Application History`
QUALIFY ROW_NUMBER() OVER (
    PARTITION BY application_id
    ORDER BY created_at DESC
) = 1;
```

---

# Reporting Usage

This table is frequently used in:

- Application Timeline Report
- Audit Report
- Operational Dashboard
- Application Status Report
- Approval Workflow Analysis
- Executive Dashboard

---

# KPIs Supported

- Average Processing Time
- Status Transition Count
- Approval Cycle Time
- Rejection Timeline
- Pending Applications
- Application Processing Duration

---

# ETL Considerations

- Preserve all historical records.
- Never overwrite previous events.
- Validate application references before loading.
- Maintain chronological order.
- Support incremental loading.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains operational application history |

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

The **Application History** table records every status transition during the loan application lifecycle.

It enables AI systems to:

- Explain application history.
- Generate application timeline reports.
- Analyze approval workflows.
- Produce BigQuery SQL involving application history.
- Determine the latest status of an application.
- Support audit and compliance analysis.

---

# Related Documentation

- Application Table
- Users Table
- Loans Table
- Database Schema
- Relationship Matrix
- Loan Lifecycle
- Business Rules

---

# Summary

The **Application History** table provides a complete historical record of every event and status transition associated with a loan application. It serves as the primary audit trail for monitoring application progress, supporting compliance requirements, operational reporting, workflow analysis, and AI-assisted SQL generation.
