# Data Dictionary Template

> **Project:** Loan Knowledge Base
>
> **Module:** Data Documentation
>
> **Document:** Data Dictionary Template
>
> **Version:** 2.0

---

# Overview

This template provides a standardized format for documenting database tables and columns within the Loan Management System.

A comprehensive data dictionary helps:

- Data Analysts understand the dataset.
- Developers implement database logic consistently.
- BI teams build accurate dashboards.
- Data Engineers manage ETL pipelines.
- AI assistants retrieve database knowledge effectively.
- New team members quickly understand the data model.

---

# Table Metadata

| Field | Description |
|---------|-------------|
| Table Name | Physical database table name |
| Display Name | Business-friendly table name |
| Module | Functional module |
| Description | Purpose of the table |
| Primary Key | Primary key column |
| Estimated Rows | Approximate row count |
| Refresh Frequency | Real-time / Daily / Weekly |
| Owner | Responsible team |
| Source System | Originating system |
| Created Date | Table creation date |
| Last Updated | Latest schema update |
| Version | Schema version |

---

# Table Overview

## Table Name

```
users
```

---

## Business Description

Describe the purpose of the table.

Example:

> Stores customer master information used throughout the loan management process.

---

## Primary Key

```
id
```

---

## Foreign Keys

| Column | References |
|---------|------------|
| city_id | cities.id |
| education_id | educations.id |

---

## Relationships

| Related Table | Relationship |
|---------------|--------------|
| application | One-to-Many |
| cities | Many-to-One |
| educations | Many-to-One |

---

# Column Dictionary

| Column | Data Type | Nullable | PK | FK | Default | Description |
|----------|----------|----------|----|----|----------|-------------|
| id | BIGINT | No | Yes | No | Auto Increment | Unique customer identifier |
| full_name | VARCHAR(255) | No | No | No | — | Customer full name |
| email | VARCHAR(255) | No | No | No | — | Customer email address |
| phone | VARCHAR(30) | Yes | No | No | NULL | Contact number |
| city_id | BIGINT | No | No | Yes | — | Customer city |
| education_id | BIGINT | Yes | No | Yes | NULL | Highest education level |
| created_at | TIMESTAMP | No | No | No | CURRENT_TIMESTAMP | Record creation timestamp |

---

# Column Details

## Column Name

```
full_name
```

### Description

Customer's legal full name.

### Data Type

```
VARCHAR(255)
```

### Nullable

```
No
```

### Default Value

```
None
```

### Example Values

```
John Smith
Jane Doe
Michael Johnson
```

### Business Rules

- Cannot be empty.
- Maximum length 255 characters.
- Store official legal name.
- Leading and trailing spaces should be removed.

---

# Enumerated Values

Document possible values for categorical fields.

Example:

## loan_status

| Value | Description |
|---------|-------------|
| Pending | Awaiting review |
| Approved | Loan approved |
| Rejected | Loan rejected |
| Active | Loan is active |
| Closed | Loan fully repaid |

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Not Null | Required fields cannot be NULL |
| Unique | Email must be unique |
| Valid Format | Email must follow RFC format |
| Positive Number | Loan amount must be greater than zero |
| Valid Date | Future dates are not allowed where applicable |

---

# Constraints

Document database constraints.

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | Unique identifier |
| FOREIGN KEY | Referential integrity |
| UNIQUE | Duplicate values not allowed |
| CHECK | Business validation |
| NOT NULL | Mandatory value |

---

# Indexes

| Index Name | Columns | Type |
|-------------|----------|------|
| pk_users | id | Primary |
| idx_users_email | email | B-Tree |
| idx_users_city | city_id | B-Tree |

---

# Sample Records

| id | full_name | city_id | education_id |
|----|-----------|----------|--------------|
| 1 | John Smith | 3 | 2 |
| 2 | Jane Doe | 5 | 4 |
| 3 | Michael Brown | 2 | 1 |

---

# Business Usage

Describe how the table is used.

Example:

- Customer registration
- Loan applications
- Credit assessment
- BI dashboards
- Customer segmentation
- Marketing analysis

---

# Reporting Usage

Reports that depend on this table.

- Customer Report
- Loan Portfolio Dashboard
- Executive Dashboard
- Customer Demographics
- Approval Analysis

---

# Data Lineage

```text
Customer Registration

        │

        ▼

users

        │

        ▼

application

        │

        ▼

loans

        │

        ▼

payments

        │

        ▼

Executive Dashboard
```

---

# ETL Considerations

Document ETL requirements.

Example:

- Incremental loading supported.
- Duplicate records removed.
- Referential integrity validated.
- Data type conversions applied.
- Invalid records routed to quarantine.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Public | Safe to expose |
| Internal | Internal business use |
| Confidential | Restricted access |
| Highly Confidential | Sensitive customer information |

Example:

```
Classification:
Confidential
```

---

# Data Retention

| Item | Value |
|------|-------|
| Retention Period | 7 Years |
| Archive Policy | Annual |
| Deletion Policy | Regulatory Compliance |

---

# Common SQL Examples

Retrieve all customers.

```sql
SELECT *
FROM users;
```

Count total records.

```sql
SELECT COUNT(*)
FROM users;
```

Find recently created customers.

```sql
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 10;
```

---

# Documentation Checklist

Before publishing the data dictionary:

- [ ] Table metadata completed.
- [ ] Every column documented.
- [ ] Data types verified.
- [ ] Primary and foreign keys identified.
- [ ] Constraints documented.
- [ ] Business definitions reviewed.
- [ ] Sample data provided.
- [ ] Reporting usage identified.
- [ ] Security classification assigned.
- [ ] Version updated.

---

# Best Practices

When maintaining a data dictionary:

- Use business-friendly descriptions.
- Keep technical and business definitions aligned.
- Document every column.
- Update documentation whenever schemas change.
- Include examples for important fields.
- Track schema versions.
- Review documentation periodically.

---

# AI & RAG Notes

A well-structured data dictionary significantly improves Retrieval-Augmented Generation (RAG) by enabling AI assistants to:

- Understand table structures.
- Explain field meanings.
- Generate SQL accurately.
- Produce ETL documentation.
- Create BI metrics.
- Assist with schema discovery.
- Recommend joins and relationships based on metadata.

---

# Related Documentation

- Database Schema
- Relationship Matrix
- Table Documentation
- Business Rules
- SQL Cookbook
- API Documentation
- ETL Documentation

---

# Summary

This template provides a standardized framework for documenting database tables, columns, constraints, relationships, business definitions, data quality rules, and usage patterns within the Loan Management System. A complete data dictionary improves collaboration across business and technical teams while serving as a high-quality knowledge source for analytics, reporting, and AI-assisted data retrieval.
