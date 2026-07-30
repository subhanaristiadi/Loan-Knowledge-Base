# Database Schema

> **Project:** Loan Knowledge Base
>
> **Module:** Database Schema
>
> **Version:** 2.0
>
> **Purpose:** Document the complete logical database schema, including all entities, columns, data types, keys, relationships, and design principles.

---

# Overview

The Loan Management database is designed using a **normalized relational database model**.

The schema supports the complete lifecycle of a loan:

- Customer registration
- Loan application
- Application review
- Loan approval
- Loan management
- Repayment
- Payment tracking

The database consists of **master tables** and **transaction tables** connected through foreign keys.

---

# Database Architecture

```text
Master Tables
─────────────
Provinces
Cities
Educations
Reason
Loan Status
Payment Status
Payment Methods

                │

                ▼

Transaction Tables
──────────────────
Users
Application
Application History
Loans
Payments
```

---

# Design Principles

The schema follows these principles:

- Third Normal Form (3NF)
- Referential integrity
- Primary and foreign key constraints
- Minimal data redundancy
- Scalable design
- Consistent naming convention
- Business-oriented relationships

---

# Naming Convention

| Object | Convention | Example |
|---------|------------|---------|
| Tables | PascalCase | `ApplicationHistory` |
| Primary Key | `id` | `id` |
| Foreign Key | `<table>_id` | `user_id` |
| Timestamp | `created_at` | `created_at` |
| Boolean | Prefix `is_` | `is_active` |

---

# Schema Overview

| Table | Category | Description |
|---------|----------|-------------|
| Provinces | Master | Province reference |
| Cities | Master | City reference |
| Educations | Master | Education levels |
| Users | Transaction | Customer data |
| Reason | Master | Loan purpose |
| Application | Transaction | Loan applications |
| Application History | Transaction | Application status history |
| Loan Status | Master | Loan status lookup |
| Loans | Transaction | Approved loans |
| Payment Status | Master | Payment status lookup |
| Payment Methods | Master | Payment channels |
| Payments | Transaction | Loan repayments |

---

# Table Schemas

---

# 1. Provinces

## Purpose

Stores province reference data.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Province identifier |
| province_name | VARCHAR | | No | Province name |

---

# 2. Cities

## Purpose

Stores city reference data.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | City identifier |
| province_id | INT | FK | No | References Provinces |
| city_name | VARCHAR | | No | City name |

---

# 3. Educations

## Purpose

Stores education categories.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Education identifier |
| education_name | VARCHAR | | No | Education level |

---

# 4. Users

## Purpose

Stores customer information.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Customer identifier |
| full_name | VARCHAR | | No | Customer name |
| email | VARCHAR | Unique | Yes | Email address |
| phone_number | VARCHAR | | Yes | Phone number |
| city_id | INT | FK | No | Customer city |
| education_id | INT | FK | No | Education level |
| created_at | TIMESTAMP | | No | Registration timestamp |

---

# 5. Reason

## Purpose

Stores predefined loan purposes.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Purpose identifier |
| reason_name | VARCHAR | | No | Loan purpose |

Examples:

- Business
- Education
- Medical
- Vehicle
- Home Renovation

---

# 6. Application

## Purpose

Stores every loan application submitted by customers.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Application ID |
| user_id | INT | FK | No | Applicant |
| reason_id | INT | FK | No | Loan purpose |
| requested_amount | DECIMAL | | No | Requested loan |
| application_date | DATE | | No | Submission date |
| status | VARCHAR | | No | Current application status |

---

# 7. Application History

## Purpose

Maintains the audit trail of application status changes.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | History identifier |
| application_id | INT | FK | No | Related application |
| previous_status | VARCHAR | | Yes | Previous status |
| current_status | VARCHAR | | No | Current status |
| changed_at | TIMESTAMP | | No | Change timestamp |

---

# 8. Loan Status

## Purpose

Master table for loan lifecycle statuses.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Status identifier |
| status_name | VARCHAR | | No | Loan status |

Typical values:

- Active
- Paid Off
- Default
- Closed
- Written Off

---

# 9. Loans

## Purpose

Stores approved loans.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Loan identifier |
| application_id | INT | FK | No | Approved application |
| loan_status_id | INT | FK | No | Current status |
| approved_amount | DECIMAL | | No | Approved amount |
| interest_rate | DECIMAL | | No | Interest rate |
| tenor_months | INT | | No | Loan tenor |
| start_date | DATE | | No | Loan start |
| end_date | DATE | | No | Loan maturity |

---

# 10. Payment Status

## Purpose

Stores payment states.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Status identifier |
| status_name | VARCHAR | | No | Payment status |

Examples:

- Pending
- Paid
- Failed
- Overdue

---

# 11. Payment Methods

## Purpose

Stores available payment channels.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Method identifier |
| method_name | VARCHAR | | No | Payment channel |

Examples:

- Bank Transfer
- Virtual Account
- QRIS
- E-Wallet
- Cash

---

# 12. Payments

## Purpose

Stores repayment transactions.

### Columns

| Column | Type | Key | Nullable | Description |
|--------|------|-----|----------|-------------|
| id | INT | PK | No | Payment identifier |
| loan_id | INT | FK | No | Related loan |
| payment_status_id | INT | FK | No | Payment status |
| payment_method_id | INT | FK | No | Payment method |
| payment_date | DATE | | No | Payment date |
| amount | DECIMAL | | No | Payment amount |

---

# Primary Key Summary

| Table | Primary Key |
|---------|-------------|
| Provinces | id |
| Cities | id |
| Educations | id |
| Users | id |
| Reason | id |
| Application | id |
| Application History | id |
| Loan Status | id |
| Loans | id |
| Payment Status | id |
| Payment Methods | id |
| Payments | id |

---

# Foreign Key Summary

| Child Table | Foreign Key | Parent Table |
|-------------|-------------|--------------|
| Cities | province_id | Provinces |
| Users | city_id | Cities |
| Users | education_id | Educations |
| Application | user_id | Users |
| Application | reason_id | Reason |
| Application History | application_id | Application |
| Loans | application_id | Application |
| Loans | loan_status_id | Loan Status |
| Payments | loan_id | Loans |
| Payments | payment_status_id | Payment Status |
| Payments | payment_method_id | Payment Methods |

---

# Entity Relationship Flow

```text
Province
    │
    ▼
City
    │
    ▼
User
    │
    ▼
Application
    │
    ├────────► Application History
    │
    ▼
Loan
    │
    ▼
Payment
```

Supporting master data:

```text
Education ─────────► User

Reason ────────────► Application

Loan Status ───────► Loan

Payment Status ────► Payment

Payment Methods ───► Payment
```

---

# Normalization

The schema satisfies Third Normal Form (3NF):

- Every table has a single primary key.
- Non-key attributes depend only on the primary key.
- Lookup values are stored in dedicated master tables.
- No transitive dependencies exist.

---

# Index Recommendations

Recommended indexes:

| Table | Index |
|--------|-------|
| Users | email |
| Users | city_id |
| Application | user_id |
| Application | application_date |
| Loans | application_id |
| Loans | loan_status_id |
| Payments | loan_id |
| Payments | payment_date |

---

# Benefits of This Schema

- Easy to maintain.
- Minimal data duplication.
- Supports reporting and analytics.
- Efficient SQL JOIN operations.
- Suitable for dashboards.
- Supports AI-generated SQL.
- Scales well as transaction volume grows.

---

# AI & RAG Notes

This schema document is designed to support Retrieval-Augmented Generation (RAG) by providing:

- Complete table definitions.
- Standardized column names.
- Key relationships.
- Business semantics.
- Reliable context for SQL generation.
- Reduced schema hallucination by AI assistants.

---

# Related Documentation

- Database Overview
- Relationship Matrix
- Loan ERD
- Table Documentation
- Business Rules
- SQL Cookbook

---

# Summary

The Database Schema defines the logical structure of the Loan Management system, including all master and transaction tables, their columns, primary keys, foreign keys, and relationships. It serves as the authoritative reference for developers, database administrators, BI analysts, and AI systems when building applications, writing SQL queries, or generating analytics.
