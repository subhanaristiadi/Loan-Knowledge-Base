# Loans Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `loans`
>
> **Version:** 2.0

---

# Overview

The **Loans** table stores approved loan records that have been created from customer loan applications.

Each record contains loan information such as the associated application, loan status, credit score, loan period, interest rate, and disbursed amount.

The table represents the final stage of the loan approval process and is the primary source for loan portfolio analysis.

---

# Business Purpose

The Loans table records approved loans and their financial attributes.

Business objectives include:

- Recording approved loans
- Tracking loan status
- Recording customer credit scores
- Recording loan terms
- Recording loan interest rates
- Recording disbursed loan amounts
- Supporting reporting and portfolio analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | loans |
| Module | Loan Processing |
| Type | Transaction Table |
| Primary Key | loan_id |
| Parent Table | application |
| Child Tables | None |
| Estimated Volume | High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| loan_id | STRING | No | ✓ | | Unique loan identifier |
| applications_id | INTEGER | No | | ✓ | References the associated application |
| loan_status_code | INTEGER | No | | ✓ | References the current loan status |
| credit_score | STRING | No | | | Customer credit score |
| loan_period | INTEGER | No | | | Loan term in months |
| interest | FLOAT | No | | | Annual interest rate |
| disbursed_amount | INTEGER | No | | | Amount disbursed to the customer |

---

# Column Descriptions

## loan_id

**Description**

Unique identifier for each loan.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## applications_id

**Description**

References the approved loan application.

**References**

```
application.applications_id
```

**Business Rules**

- Required
- Must reference an existing application

---

## loan_status_code

**Description**

References the current loan status.

**References**

```
loan_status.loan_status_code
```

**Business Rules**

- Required
- Must reference a valid loan status

---

## credit_score

**Description**

Credit score assigned during the loan approval process.

**Business Rules**

- Required
- Numeric value used for credit assessment

---

## loan_period

**Description**

Loan repayment period expressed in months.

**Business Rules**

- Required
- Must be greater than zero

---

## interest

**Description**

Annual interest rate applied to the loan.

**Business Rules**

- Required
- Must be greater than or equal to zero

---

## disbursed_amount

**Description**

Amount of money disbursed to the customer.

**Business Rules**

- Required
- Must be greater than zero

---

# Primary Key

| Column | Description |
|---------|-------------|
| loan_id | Unique loan identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| applications_id | application.applications_id |
| loan_status_code | loan_status.loan_status_code |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-One (typically) | One approved application creates one loan |
| loan_status | Many-to-One | Many loans can share the same status |

---

# Entity Relationship

```text
application
      │
      │ applications_id
      ▼
loans
      │
      └────────────► loan_status
```

---

# Business Rules

- Every loan must originate from an application.
- Every loan must have one loan status.
- Credit scores must be valid numeric values.
- Loan period must be greater than zero.
- Interest rates must be valid.
- Disbursed amount must be greater than zero.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Application | applications_id cannot be NULL |
| Required Loan Status | loan_status_code cannot be NULL |
| Required Credit Score | credit_score cannot be NULL |
| Positive Loan Period | loan_period > 0 |
| Positive Interest | interest >= 0 |
| Positive Disbursed Amount | disbursed_amount > 0 |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | loan_id |
| FOREIGN KEY | applications_id |
| FOREIGN KEY | loan_status_code |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_loans | loan_id | Primary key lookup |
| idx_loans_application | applications_id | Application lookup |
| idx_loans_status | loan_status_code | Status reporting |
| idx_loans_credit_score | credit_score | Credit score analysis |

---

# Common SQL Queries

## View All Loans

```sql
SELECT *
FROM `crediu-504100.Crediu.Loans`;
```

---

## Loan Portfolio by Status

```sql
SELECT
    loan_status_code,
    COUNT(*) AS total_loans
FROM `crediu-504100.Crediu.Loans`
GROUP BY loan_status_code;
```

---

## Average Credit Score

```sql
SELECT
    AVG(credit_score) AS average_credit_score
FROM `crediu-504100.Crediu.Loans`;
```

---

## Average Interest Rate

```sql
SELECT
    AVG(interest) AS average_interest_rate
FROM `crediu-504100.Crediu.Loans`;
```

---

## Total Disbursed Amount

```sql
SELECT
    SUM(disbursed_amount) AS total_disbursed
FROM `crediu-504100.Crediu.Loans`;
```

---

# Reporting Usage

This table is frequently used in:

- Loan Portfolio Dashboard
- Credit Score Analysis
- Loan Performance Report
- Interest Rate Analysis
- Executive Dashboard

---

# KPIs Supported

- Total Loans
- Total Disbursed Amount
- Average Credit Score
- Average Interest Rate
- Average Loan Period
- Loan Status Distribution

---

# ETL Considerations

- Preserve loan identifiers.
- Validate application references.
- Validate loan status references.
- Validate numeric financial values.
- Preserve original loan records.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer loan information |

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
- loan_status

### Referenced By

- None

---

# AI & RAG Notes

The **Loans** table contains approved loan records and financial information.

It enables AI systems to:

- Generate BigQuery SQL involving loan data.
- Analyze loan portfolio performance.
- Calculate disbursed loan amounts.
- Analyze credit score distributions.
- Produce loan performance reports.
- Support lending analytics.

---

# Related Documentation

- Application Table
- Loan Status Table
- Users Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Loans** table stores approved loan records, including their associated applications, loan status, credit scores, loan terms, interest rates, and disbursed amounts. It serves as the primary transaction table for loan portfolio management, reporting, business analytics, and AI-assisted SQL generation.
