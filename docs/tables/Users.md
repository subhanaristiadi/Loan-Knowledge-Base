# Users Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `users`
>
> **Version:** 2.0

---

# Overview

The **Users** table is the primary master table that stores customer information within the Loan Management System.

Each customer is uniquely identified and may submit one or more loan applications throughout their relationship with the organization.

This table contains demographic and contact information that supports loan processing, customer management, analytics, and reporting.

---

# Business Purpose

The Users table maintains the master records of all customers.

Business objectives include:

- Managing customer identities
- Supporting loan application processing
- Maintaining customer contact information
- Enabling demographic analysis
- Supporting customer segmentation
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | users |
| Module | Customer Management |
| Type | Master Table |
| Primary Key | id |
| Parent Tables | cities, educations |
| Child Table | application |
| Estimated Volume | High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Customer identifier |
| full_name | VARCHAR(255) | No | | | Customer full name |
| email | VARCHAR(255) | No | | | Email address |
| phone | VARCHAR(30) | Yes | | | Phone number |
| city_id | BIGINT | No | | ✓ | Customer city |
| education_id | BIGINT | Yes | | ✓ | Customer education level |
| created_at | TIMESTAMP | No | | | Customer registration date |

---

# Column Descriptions

## id

**Description**

Unique identifier for each customer.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## full_name

**Description**

Official full name of the customer.

**Business Rules**

- Required
- Maximum 255 characters
- Store legal name
- Remove leading and trailing spaces

---

## email

**Description**

Primary email address.

**Business Rules**

- Required
- Must be unique
- Valid email format
- Used for customer communication

Example:

```text
john.smith@email.com
```

---

## phone

**Description**

Customer phone number.

**Business Rules**

- Optional
- Store using standardized format
- May include country code

Example:

```text
+62-812-3456-7890
```

---

## city_id

**Description**

References the customer's city.

**References**

```text
cities.id
```

**Business Rules**

- Required
- City must exist
- Foreign key enforced

---

## education_id

**Description**

References the customer's education level.

**References**

```text
educations.id
```

**Business Rules**

- Optional
- Must reference a valid education level if provided

---

## created_at

**Description**

Date and time the customer record was created.

**Business Rules**

- Automatically generated
- Cannot be modified
- Used for auditing and reporting

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique customer identifier |

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
| cities | Many-to-One | Customer belongs to one city |
| educations | Many-to-One | Customer has one education level |
| application | One-to-Many | Customer may submit multiple loan applications |

---

# Entity Relationship

```text
cities
    │
    ▼
users
    ▲
    │
educations

users
    │
    ▼
application
```

---

# Business Rules

- Every customer must have a unique identifier.
- Every customer must belong to one city.
- Education level is optional.
- Email addresses must be unique.
- A customer may submit multiple loan applications.
- Customer records should not be physically deleted.
- Customer identity information should remain consistent.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Name | full_name cannot be NULL |
| Required Email | email cannot be NULL |
| Unique Email | Duplicate emails are not allowed |
| Valid Email | Must follow email format |
| Valid City | city_id must exist |
| Valid Education | education_id must exist if populated |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | city_id |
| FOREIGN KEY | education_id |
| UNIQUE | email |
| NOT NULL | full_name |
| NOT NULL | email |
| NOT NULL | city_id |

Example:

```sql
UNIQUE (email)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_users | id | Primary key lookup |
| idx_users_email | email | Customer search |
| idx_users_city | city_id | Geographic reporting |
| idx_users_education | education_id | Demographic reporting |
| idx_users_created | created_at | Registration trend analysis |

---

# Sample Records

| id | full_name | email | phone | city_id | education_id | created_at |
|---:|-----------|-------|-------|--------:|-------------:|------------|
| 1 | John Smith | john@email.com | +62-812-1111-1111 | 31 | 5 | 2026-01-05 09:12:00 |
| 2 | Jane Doe | jane@email.com | +62-813-2222-2222 | 35 | 6 | 2026-01-07 14:30:00 |
| 3 | Michael Brown | michael@email.com | +62-811-3333-3333 | 53 | 4 | 2026-01-10 08:45:00 |

---

# Common SQL Queries

## View All Customers

```sql
SELECT *
FROM users;
```

---

## Customer Count

```sql
SELECT
    COUNT(*) AS total_customers
FROM users;
```

---

## Customers by City

```sql
SELECT
    c.city_name,
    COUNT(u.id) AS total_customers
FROM cities c
LEFT JOIN users u
    ON c.id = u.city_id
GROUP BY c.city_name
ORDER BY total_customers DESC;
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

## Monthly Customer Registrations

```sql
SELECT
    DATE_TRUNC('month', created_at) AS month,
    COUNT(*) AS new_customers
FROM users
GROUP BY month
ORDER BY month;
```

---

## Customers with Loan Applications

```sql
SELECT
    u.full_name,
    COUNT(a.id) AS total_applications
FROM users u
LEFT JOIN application a
    ON u.id = a.user_id
GROUP BY u.full_name
ORDER BY total_applications DESC;
```

---

# Reporting Usage

This table is commonly used in:

- Customer Dashboard
- Executive Dashboard
- Customer Demographics Report
- Loan Portfolio Dashboard
- Customer Segmentation Analysis
- Regional Performance Dashboard
- Marketing Campaign Analysis

---

# KPIs Supported

- Total Customers
- New Customers
- Customer Growth Rate
- Customers by City
- Customers by Province
- Customers by Education
- Average Applications per Customer
- Customer Retention Rate

---

# ETL Considerations

- Load reference tables before customer data.
- Validate city and education references.
- Remove duplicate email addresses.
- Standardize phone number formats.
- Preserve customer identifiers.
- Record creation timestamps consistently.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer personally identifiable information (PII) |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | 10 Years |
| Archive Policy | Annual Archive |
| Deletion Policy | Regulatory Compliance and privacy policy compliance |

---

# Dependencies

### Depends On

- cities
- educations

### Referenced By

- application

---

# AI & RAG Notes

The **Users** table is the primary customer entity within the Loan Management System and provides essential context for AI-assisted analytics. It enables AI systems to:

- Generate customer demographic reports.
- Analyze customer growth and segmentation.
- Recommend joins between customers, applications, and geographic data.
- Produce SQL for customer analytics.
- Support marketing, risk assessment, and portfolio analysis.
- Enhance Retrieval-Augmented Generation (RAG) with structured customer metadata.

---

# Related Documentation

- Cities Table
- Provinces Table
- Educations Table
- Application Table
- Database Schema
- Relationship Matrix
- Customer Dashboard
- Business Rules

---

# Summary

The **Users** table is the central master table for customer information within the Loan Management System. It stores demographic, geographic, and contact information that supports loan processing, customer management, analytics, reporting, and AI-powered applications. As the parent entity for loan applications, it forms the foundation of customer-centric operations across the entire platform.
