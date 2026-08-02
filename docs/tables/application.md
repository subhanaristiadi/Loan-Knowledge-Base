# Application Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `application`
>
> **Version:** 2.0

---

# Overview

The **Application** table stores information submitted by customers during the loan application process.

Each record represents a loan application and contains applicant references, financial information, education level, loan purpose, and the application creation date.

The table serves as the primary source for customer application data before loan approval and disbursement.

---

# Business Purpose

The Application table records customer loan applications and provides the information required for credit assessment.

Business objectives include:

- Recording loan applications
- Linking applications to customers
- Recording customer income and expenses
- Recording loan purpose
- Recording applicant education level
- Supporting loan approval analysis
- Supporting reporting and analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | application |
| Module | Loan Processing |
| Type | Transaction Table |
| Primary Key | applications_id |
| Parent Table | users |
| Child Tables | application_history, loans |
| Estimated Volume | High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| applications_id | INTEGER | No | ✓ | | Unique application identifier |
| user_id | INTEGER | No | | ✓ | Applicant |
| reason_id | INTEGER | No | | ✓ | Loan purpose |
| education_code | INTEGER | No | | | Applicant education level |
| created_date | TIMESTAMP | No | | | Application creation date |
| income | INTEGER | No | | | Monthly income |
| expense | INTEGER | No | | | Monthly expense |

---

# Column Descriptions

## applications_id

**Description**

Unique identifier for each loan application.

**Business Rules**

- Auto-generated
- Cannot be duplicated
- Immutable after creation

---

## user_id

**Description**

References the customer submitting the application.

**References**

```
users.user_id
```

**Business Rules**

- Required
- Must reference an existing customer

---

## reason_id

**Description**

References the customer's loan purpose.

**References**

```
reason.reason_id
```

---

## education_code

**Description**

Represents the applicant's education level.

**Business Rules**

- Required
- References the education master data when available

---

## created_date

**Description**

Date and time when the application was created.

**Business Rules**

- Automatically generated
- Cannot be NULL

---

## income

**Description**

Applicant's monthly income used during credit assessment.

**Business Rules**

- Must be greater than or equal to zero

---

## expense

**Description**

Applicant's monthly expenses declared during the application process.

**Business Rules**

- Must be greater than or equal to zero

---

# Primary Key

| Column | Description |
|---------|-------------|
| applications_id | Unique application identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| user_id | users.user_id |
| reason_id | reason.reason_id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| users | Many-to-One | Application belongs to one customer |
| reason | Many-to-One | Application has one loan purpose |
| application_history | One-to-Many | Application history records |
| loans | One-to-One (typically) | Approved application creates a loan |

---

# Entity Relationship

```text
users
   │
   │ user_id
   ▼
application
   │
   ├────────────► reason
   │
   ├────────────► application_history
   │
   └────────────► loans
```

---

# Business Rules

- Every application belongs to one customer.
- Every application must have one loan purpose.
- Income and expense must be valid numeric values.
- Every application has one education code.
- Approved applications may generate loans.
- Application history is maintained separately.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Customer | user_id cannot be NULL |
| Required Loan Purpose | reason_id cannot be NULL |
| Required Education | education_code cannot be NULL |
| Valid Income | income >= 0 |
| Valid Expense | expense >= 0 |
| Required Created Date | created_date cannot be NULL |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | applications_id |
| FOREIGN KEY | user_id |
| FOREIGN KEY | reason_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_application | applications_id | Primary key lookup |
| idx_application_user | user_id | Customer lookup |
| idx_application_reason | reason_id | Loan purpose reporting |
| idx_application_created | created_date | Date filtering |

---

# Common SQL Queries

## View All Applications

```sql
SELECT *
FROM `crediu-504100.Crediu.Application`;
```

---

## Monthly Applications

```sql
SELECT
    DATE_TRUNC(DATE(created_date), MONTH) AS application_month,
    COUNT(*) AS total_applications
FROM `crediu-504100.Crediu.Application`
GROUP BY application_month
ORDER BY application_month;
```

---

## Average Income and Expense

```sql
SELECT
    AVG(income) AS avg_income,
    AVG(expense) AS avg_expense
FROM `crediu-504100.Crediu.Application`;
```

---

## Applications by Loan Purpose

```sql
SELECT
    reason_id,
    COUNT(*) AS total_applications
FROM `crediu-504100.Crediu.Application`
GROUP BY reason_id
ORDER BY total_applications DESC;
```

---

# Reporting Usage

This table is frequently used in:

- Loan Application Dashboard
- Customer Financial Profile
- Loan Purpose Analysis
- Income Analysis
- Application Trend Report

---

# KPIs Supported

- Total Applications
- Average Applicant Income
- Average Applicant Expense
- Applications by Loan Purpose
- Applications by Education Level
- Monthly Application Volume

---

# ETL Considerations

- Preserve original application IDs.
- Validate customer references.
- Validate loan purpose references.
- Validate numeric income and expense values.
- Preserve original creation timestamps.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer financial information |

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

- users
- reason

### Referenced By

- application_history
- loans

---

# AI & RAG Notes

The **Application** table is the primary source of customer loan application information.

It enables AI systems to:

- Analyze applicant financial profiles.
- Generate BigQuery SQL involving loan applications.
- Analyze application trends.
- Produce customer financial reports.
- Support loan approval analytics.

---

# Related Documentation

- Users Table
- Loans Table
- Application History Table
- Reason Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Application** table records customer loan applications and stores applicant references, education level, financial information, loan purpose, and application timestamps. It serves as the central transaction table supporting credit assessment, loan processing, reporting, and AI-assisted SQL generation.# Application Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `application`
>
> **Version:** 2.0

---

# Overview

The **Application** table stores every loan application submitted by customers.

It represents the first transactional entity in the loan lifecycle and serves as the bridge between customer information and approved loans.

Each application contains:

- Applicant
- Requested loan amount
- Loan purpose
- Submission date
- Current application status

An application may eventually be approved, rejected, or remain under review.

---

# Business Purpose

The Application table records all customer loan requests before approval.

Business objectives include:

- Recording loan requests
- Tracking application status
- Supporting approval workflows
- Recording requested loan amounts
- Providing historical application data
- Supporting reporting and analytics

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
| applications_codes | STRING | No | | | Application status or workflow code recorded for the history event |
| application_id | BIGINT | No | | ✓ | References the associated application |

---

# Column Descriptions

## id

**Description**

Unique identifier for each loan application.

**Business Rules**

- Auto-generated
- Cannot be duplicated
- Immutable after creation

---

## user_id

**Description**

References the customer submitting the application.

**References**

```
users.id
```

**Business Rules**

- Customer must exist
- Required field
- Foreign key enforced

---

## reason_id

**Description**

Specifies the purpose of the requested loan.

**References**

```
reason.id
```

Examples include:

- Business
- Education
- Medical
- Vehicle
- Home Renovation

---

## requested_amount

**Description**

Requested loan amount before underwriting.

**Business Rules**

- Must be greater than zero
- Cannot be NULL
- May differ from approved amount

Example

```
15000.00
```

---

## application_date

**Description**

Date when the application was submitted.

**Business Rules**

- Cannot be in the future
- Required
- Immutable

---

## status

**Description**

Current application status.

Typical values:

- Submitted
- Under Review
- Approved
- Rejected
- Cancelled

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique application identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| user_id | users.id |
| reason_id | reason.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| users | Many-to-One | Application belongs to one customer |
| reason | Many-to-One | One loan purpose |
| application_history | One-to-Many | Status history |
| loans | One-to-One (typically) | Approved application creates a loan |

---

# Entity Relationship

```text
users
   │
   │ user_id
   ▼
application
   │
   ├────────────► reason
   │
   ├────────────► application_history
   │
   └────────────► loans
```

---

# Business Rules

- Every application belongs to one customer.
- Every application must have one loan purpose.
- Requested amount must be positive.
- Only approved applications may generate loans.
- Every status change should be recorded in Application History.
- Applications cannot exist without a valid customer.
- Rejected applications never create loans.

---

# Status Lifecycle

```text
Submitted

↓

Under Review

↓

Approved ─────────► Loan Created

OR

Rejected

OR

Cancelled
```

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Customer | user_id cannot be NULL |
| Required Purpose | reason_id cannot be NULL |
| Positive Amount | requested_amount > 0 |
| Valid Date | application_date cannot be in the future |
| Valid Status | Status must match allowed values |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | user_id |
| FOREIGN KEY | reason_id |
| NOT NULL | Required columns |
| CHECK | Positive requested amount |

Example:

```sql
CHECK (requested_amount > 0)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_application | id | Primary key lookup |
| idx_application_user | user_id | Customer search |
| idx_application_reason | reason_id | Loan purpose reporting |
| idx_application_status | status | Workflow filtering |
| idx_application_date | application_date | Date-based reporting |

---

# Sample Records

| id | user_id | reason_id | requested_amount | application_date | status |
|----|---------|-----------|-----------------:|------------------|--------|
| 1 | 12 | 2 | 15000.00 | 2026-01-15 | Approved |
| 2 | 18 | 5 | 8000.00 | 2026-01-16 | Under Review |
| 3 | 25 | 1 | 25000.00 | 2026-01-17 | Rejected |

---

# Common SQL Queries

## View All Applications

```sql
SELECT *
FROM application;
```

---

## Applications by Status

```sql
SELECT
    status,
    COUNT(*) AS total
FROM application
GROUP BY status;
```

---

## Monthly Applications

```sql
SELECT
    DATE_TRUNC('month', application_date) AS month,
    COUNT(*) AS applications
FROM application
GROUP BY month
ORDER BY month;
```

---

## Applications with Customer Information

```sql
SELECT
    a.id,
    u.full_name,
    a.requested_amount,
    a.status
FROM application a
JOIN users u
    ON a.user_id = u.id;
```

---

## Applications by Loan Purpose

```sql
SELECT
    r.reason_name,
    COUNT(*) AS total_applications
FROM application a
JOIN reason r
    ON a.reason_id = r.id
GROUP BY r.reason_name
ORDER BY total_applications DESC;
```

---

# Reporting Usage

This table is frequently used in:

- Application Dashboard
- Approval Funnel
- Approval Rate Report
- Loan Pipeline Report
- Executive Dashboard
- Monthly Application Trend
- Loan Purpose Analysis

---

# KPIs Supported

- Total Applications
- Application Growth
- Approval Rate
- Rejection Rate
- Average Requested Amount
- Applications by Purpose
- Applications by Customer
- Monthly Applications
- Pending Applications

---

# ETL Considerations

- Preserve original submission date.
- Validate customer references before loading.
- Enforce foreign key integrity.
- Standardize application statuses.
- Reject negative requested amounts.
- Capture incremental updates for status changes.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer financial request information |

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

- users
- reason

### Referenced By

- application_history
- loans

---

# AI & RAG Notes

The **Application** table is central to the loan processing workflow and provides essential context for AI-assisted analytics. It enables AI systems to:

- Analyze loan demand.
- Calculate approval rates.
- Generate customer application reports.
- Build approval funnel dashboards.
- Produce SQL involving customer applications.
- Explain the relationship between applications, loans, and status history.

---

# Related Documentation

- Users Table
- Loans Table
- Application History Table
- Database Schema
- Relationship Matrix
- Loan Lifecycle
- Business Rules

---

# Summary

The **Application** table records every loan request submitted by customers and serves as the core entry point of the loan processing workflow. It links customers with loan purposes, tracks requested amounts and application status, and provides the foundation for approval processing, historical tracking, reporting, and business intelligence across the Loan Management System.
