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

The **Reason** table is a master reference table that stores the predefined purposes for which customers apply for loans.

Rather than allowing free-text input, the Loan Management System uses this table to standardize loan purposes, ensuring consistent reporting, accurate analytics, and reliable business intelligence.

Each loan application references exactly one loan purpose from this table.

---

# Business Purpose

The Reason table provides standardized loan purpose categories.

Business objectives include:

- Standardizing loan purposes
- Preventing inconsistent data entry
- Supporting business analytics
- Improving loan portfolio reporting
- Enabling customer segmentation
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | reason |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Table | application |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Loan purpose identifier |
| reason_name | VARCHAR(100) | No | | | Loan purpose name |

---

# Column Descriptions

## id

**Description**

Unique identifier for each loan purpose.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## reason_name

**Description**

Defines the customer's purpose for requesting a loan.

Typical values:

- Business Capital
- Education
- Medical Expenses
- Home Renovation
- Vehicle Purchase
- Personal Expenses
- Debt Consolidation
- Wedding
- Travel
- Other

**Business Rules**

- Required
- Must be unique
- Use standardized naming
- Avoid abbreviations unless officially defined

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique loan purpose identifier |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-Many | One loan purpose may be used by many applications |

---

# Entity Relationship

```text
reason
    │
    │ id
    ▼
application
      │
      ▼
loans
```

---

# Business Rules

- Every loan application must have one loan purpose.
- Loan purposes must be selected from this table.
- Duplicate purpose names are not allowed.
- New loan purposes require administrative approval.
- Existing purpose names should not be modified without impact analysis.

---

# Common Loan Purposes

| Purpose | Description |
|----------|-------------|
| Business Capital | Business expansion or working capital |
| Education | Tuition or educational expenses |
| Medical Expenses | Healthcare and emergency treatment |
| Home Renovation | Property improvement |
| Vehicle Purchase | Purchase of cars or motorcycles |
| Personal Expenses | General personal financial needs |
| Debt Consolidation | Combining multiple debts |
| Wedding | Wedding-related expenses |
| Travel | Business or personal travel |
| Other | Miscellaneous approved purposes |

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Purpose | reason_name cannot be NULL |
| Unique Purpose | Duplicate values are not allowed |
| Standard Naming | Use approved business terminology |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| UNIQUE | reason_name |
| NOT NULL | reason_name |

Example:

```sql
UNIQUE (reason_name)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_reason | id | Primary key lookup |
| idx_reason_name | reason_name | Purpose lookup |

---

# Sample Records

| id | reason_name |
|---:|-------------|
| 1 | Business Capital |
| 2 | Education |
| 3 | Medical Expenses |
| 4 | Home Renovation |
| 5 | Vehicle Purchase |
| 6 | Personal Expenses |
| 7 | Debt Consolidation |
| 8 | Wedding |
| 9 | Travel |
| 10 | Other |

---

# Common SQL Queries

## View All Loan Purposes

```sql
SELECT *
FROM reason;
```

---

## Applications by Loan Purpose

```sql
SELECT
    r.reason_name,
    COUNT(a.id) AS total_applications
FROM reason r
LEFT JOIN application a
    ON r.id = a.reason_id
GROUP BY r.reason_name
ORDER BY total_applications DESC;
```

---

## Approved Loan Amount by Purpose

```sql
SELECT
    r.reason_name,
    SUM(l.approved_amount) AS total_portfolio
FROM loans l
JOIN application a
    ON l.application_id = a.id
JOIN reason r
    ON a.reason_id = r.id
GROUP BY r.reason_name
ORDER BY total_portfolio DESC;
```

---

## Average Loan Amount by Purpose

```sql
SELECT
    r.reason_name,
    ROUND(AVG(l.approved_amount), 2) AS average_amount
FROM loans l
JOIN application a
    ON l.application_id = a.id
JOIN reason r
    ON a.reason_id = r.id
GROUP BY r.reason_name
ORDER BY average_amount DESC;
```

---

# Reporting Usage

This table is commonly used in:

- Loan Purpose Dashboard
- Executive Dashboard
- Customer Behavior Analysis
- Loan Portfolio Report
- Marketing Analysis
- Credit Risk Report

---

# KPIs Supported

- Applications by Purpose
- Loan Portfolio by Purpose
- Approval Rate by Purpose
- Average Loan Amount by Purpose
- Customer Distribution by Loan Purpose
- Monthly Loan Demand by Purpose

---

# ETL Considerations

- Load loan purpose master data before application records.
- Prevent duplicate purpose names.
- Maintain standardized naming.
- Validate foreign key references from the Application table.
- Review new categories before deployment.

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

- application

---

# AI & RAG Notes

The **Reason** table provides standardized loan purpose categories that enable AI systems to:

- Analyze borrowing trends.
- Generate SQL grouped by loan purpose.
- Produce customer behavior reports.
- Build loan demand dashboards.
- Recommend joins between applications, loans, and loan purposes.
- Improve portfolio segmentation and business insights.

---

# Related Documentation

- Application Table
- Loans Table
- Database Schema
- Relationship Matrix
- Business Rules
- Executive Dashboard
- Customer Analytics

---

# Summary

The **Reason** table is a master reference table that defines the standardized purposes for loan applications within the Loan Management System. By centralizing loan purpose categories, it ensures consistent data entry, reliable reporting, meaningful portfolio analysis, and strong referential integrity while supporting operational processes, business intelligence, and AI-powered analytics.
