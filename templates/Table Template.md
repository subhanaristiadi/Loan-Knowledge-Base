# Table Documentation Template

> **Project:** Loan Knowledge Base
>
> **Module:** Database Documentation
>
> **Document:** Table Template
>
> **Version:** 2.0

---

# Overview

This template provides a standardized structure for documenting every database table in the Loan Management System.

Each table document should explain:

- Business purpose
- Table structure
- Relationships
- Constraints
- Business rules
- SQL examples
- Reporting usage
- AI & RAG context

A consistent format improves collaboration between Business Analysts, Developers, Data Engineers, BI teams, and AI assistants.

---

# Table Metadata

| Field | Description |
|---------|-------------|
| Table Name | Physical database table |
| Display Name | Business-friendly name |
| Module | Functional module |
| Description | Purpose of the table |
| Primary Key | Primary key column |
| Estimated Records | Approximate row count |
| Refresh Frequency | Real-time / Daily / Weekly |
| Owner | Responsible team |
| Source System | Originating application |
| Version | Documentation version |
| Last Updated | Latest revision |

---

# Table Overview

## Table Name

```text
users
```

---

## Display Name

```text
Customers
```

---

## Module

```text
Customer Management
```

---

## Business Purpose

Describe why the table exists.

Example:

> Stores master information for customers who submit loan applications.

---

## Business Description

Explain how the table is used within the system.

Example:

> Each customer may submit multiple loan applications.
The table acts as the master entity for all customer-related processes.

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Unique identifier |
| full_name | VARCHAR(255) | No | | | Customer name |
| email | VARCHAR(255) | No | | | Email address |
| phone | VARCHAR(30) | Yes | | | Phone number |
| city_id | BIGINT | No | | ✓ | Customer city |
| education_id | BIGINT | Yes | | ✓ | Education level |
| created_at | TIMESTAMP | No | | | Creation timestamp |

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique table identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| city_id | cities.id |
| education_id | educations.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-Many | Customer submits applications |
| cities | Many-to-One | Customer belongs to a city |
| educations | Many-to-One | Customer education level |

---

# Entity Relationship

```text
users
   │
   ├──────────────► application
   │
   ├──────────────► cities
   │
   └──────────────► educations
```

---

# Column Details

## id

### Description

Unique customer identifier.

### Data Type

```text
BIGINT
```

### Nullable

```text
No
```

### Business Rules

- Must be unique.
- Auto-generated.
- Cannot be modified.

---

## full_name

### Description

Customer's legal name.

### Data Type

```text
VARCHAR(255)
```

### Business Rules

- Required.
- Maximum 255 characters.
- Remove leading and trailing spaces.
- Store official legal name.

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | Unique identifier |
| FOREIGN KEY | Referential integrity |
| NOT NULL | Required fields |
| UNIQUE | Prevent duplicate values |
| CHECK | Business validation |

---

# Indexes

| Index Name | Columns | Purpose |
|-------------|----------|---------|
| pk_users | id | Primary key lookup |
| idx_users_email | email | Email search |
| idx_users_city | city_id | Geographic filtering |

---

# Business Rules

Examples:

- Every customer must have a unique email.
- A customer may submit multiple applications.
- A city must exist before assigning a customer.
- Deleted customers should be archived instead of physically removed.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required | Mandatory columns cannot be NULL |
| Unique | Email must be unique |
| Valid Format | Email format validation |
| Referential Integrity | Foreign keys must exist |
| Duplicate Prevention | Customer duplication not allowed |

---

# Sample Records

| id | full_name | city_id | education_id |
|----|-----------|----------|--------------|
| 1 | John Smith | 3 | 2 |
| 2 | Jane Doe | 4 | 5 |
| 3 | Michael Brown | 2 | 1 |

---

# Common SQL Queries

## Retrieve all records

```sql
SELECT *
FROM users;
```

---

## Count records

```sql
SELECT COUNT(*)
FROM users;
```

---

## Latest customers

```sql
SELECT *
FROM users
ORDER BY created_at DESC
LIMIT 10;
```

---

## Customer with city

```sql
SELECT
    u.full_name,
    c.city_name
FROM users u
JOIN cities c
    ON u.city_id = c.id;
```

---

# Reporting Usage

This table is commonly used in:

- Customer Dashboard
- Loan Portfolio Report
- Geographic Analysis
- Customer Demographics
- Executive Dashboard
- Marketing Analysis

---

# KPI Usage

Example KPIs:

- Total Customers
- New Customers
- Active Customers
- Customer Growth Rate
- Customers by Province
- Customers by Education

---

# ETL Considerations

Document ETL behavior.

Example:

- Incremental loading supported.
- Duplicate detection enabled.
- Foreign key validation performed.
- Invalid records rejected.
- Audit timestamps preserved.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Public | Non-sensitive |
| Internal | Internal business data |
| Confidential | Customer information |
| Highly Confidential | Personally identifiable information (PII) |

Example

```text
Confidential
```

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | 7 Years |
| Archive Strategy | Annual Archive |
| Deletion Policy | Regulatory Compliance |

---

# Dependencies

This table depends on:

- cities
- educations

This table is referenced by:

- application

---

# Documentation Checklist

Before publishing:

- [ ] Business purpose documented
- [ ] All columns described
- [ ] Keys identified
- [ ] Relationships verified
- [ ] Constraints documented
- [ ] SQL examples included
- [ ] Reporting usage documented
- [ ] Security classification assigned
- [ ] Version updated

---

# Best Practices

When documenting database tables:

- Use business-friendly language.
- Document every column.
- Include business context, not only technical details.
- Keep relationships synchronized with the ERD.
- Include representative SQL examples.
- Review documentation after every schema change.
- Maintain version history.

---

# AI & RAG Notes

This template is optimized for Retrieval-Augmented Generation (RAG) and AI-assisted database exploration. Standardized table documentation enables AI assistants to:

- Understand table purposes.
- Explain relationships.
- Recommend joins.
- Generate SQL queries.
- Produce technical documentation.
- Assist with impact analysis and schema discovery.

---

# Related Documentation

- Database Schema
- Relationship Matrix
- Data Dictionary
- Business Rules
- SQL Cookbook
- ERD Documentation
- API Documentation

---

# Summary

This template provides a comprehensive, enterprise-grade standard for documenting database tables in the Loan Management System. By combining business context, technical metadata, relationships, constraints, SQL examples, reporting usage, and governance information, it creates high-quality documentation that supports development, analytics, governance, and AI-powered knowledge retrieval.
