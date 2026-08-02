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

The **Users** table stores customer profile information for individuals registered in the Loan Management System.

Each record represents a unique customer and contains demographic information, registration details, education level, and residential location. The table serves as the central customer dimension referenced throughout the lending process.

---

# Business Purpose

The Users table maintains customer information used throughout the lending lifecycle.

Business objectives include:

- Managing customer profiles
- Recording customer registration information
- Supporting demographic analysis
- Supporting loan application processing
- Supporting customer segmentation
- Supporting business reporting

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | users |
| Module | Customer Management |
| Type | Master Table |
| Primary Key | user_id |
| Parent Table | None |
| Child Tables | application |
| Estimated Volume | High |
| Update Frequency | Continuous |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| user_id | BIGINT | No | ✓ | | Unique customer identifier |
| register_date | TIMESTAMP | No | | | Customer registration date and time |
| gender | STRING | No | | | Customer gender |
| date_of_birth | DATE | No | | | Customer date of birth |
| education_code | INTEGER | No | | ✓ | References customer education level |
| locations_id | INTEGER | No | | ✓ | References customer's city/location |

---

# Column Descriptions

## user_id

**Description**

Unique identifier assigned to each customer.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## register_date

**Description**

Date and time when the customer registered in the system.

**Business Rules**

- Required
- Cannot be NULL

---

## gender

**Description**

Customer gender.

Example values:

- Male
- Female

**Business Rules**

- Required
- Should contain standardized values

---

## date_of_birth

**Description**

Customer's date of birth.

**Business Rules**

- Required
- Cannot be in the future

---

## education_code

**Description**

References the customer's highest education level.

**References**

```
educations.education_code
```

**Business Rules**

- Required
- Must reference an existing education level

---

## locations_id

**Description**

References the customer's registered city.

**References**

```
cities.locations_id
```

**Business Rules**

- Required
- Must reference an existing city

---

# Primary Key

| Column | Description |
|---------|-------------|
| user_id | Unique customer identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| education_code | educations.education_code |
| locations_id | cities.locations_id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| application | One-to-Many | One customer can submit multiple loan applications |
| educations | Many-to-One | Many customers can share the same education level |
| cities | Many-to-One | Many customers can reside in the same city |

---

# Entity Relationship

```text
educations
      │
      │ education_code
      ▼
users
 ▲    │
 │    │ locations_id
 │    ▼
cities

users
  │
  │ user_id
  ▼
application
```

---

# Business Rules

- Every customer must have a unique identifier.
- Every customer must have one education level.
- Every customer must belong to one city.
- Registration date must represent the customer's first registration.
- Date of birth cannot be later than the current date.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required User ID | user_id cannot be NULL |
| Required Registration Date | register_date cannot be NULL |
| Required Gender | gender cannot be NULL |
| Required Date of Birth | date_of_birth cannot be NULL |
| Required Education | education_code cannot be NULL |
| Required Location | locations_id cannot be NULL |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | user_id |
| FOREIGN KEY | education_code |
| FOREIGN KEY | locations_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_users | user_id | Primary key lookup |
| idx_users_registration | register_date | Registration analysis |
| idx_users_education | education_code | Education analysis |
| idx_users_location | locations_id | Geographic analysis |

---

# Common SQL Queries

## View All Users

```sql
SELECT *
FROM `crediu-504100.Crediu.Users`;
```

---

## Users by Education

```sql
SELECT
    education_code,
    COUNT(*) AS total_users
FROM `crediu-504100.Crediu.Users`
GROUP BY education_code;
```

---

## Users by City

```sql
SELECT
    locations_id,
    COUNT(*) AS total_users
FROM `crediu-504100.Crediu.Users`
GROUP BY locations_id;
```

---

## Monthly User Registrations

```sql
SELECT
    DATE_TRUNC(DATE(register_date), MONTH) AS registration_month,
    COUNT(*) AS total_users
FROM `crediu-504100.Crediu.Users`
GROUP BY registration_month
ORDER BY registration_month;
```

---

# Reporting Usage

This table is frequently used in:

- Customer Dashboard
- Registration Trend Report
- Demographic Analysis
- Geographic Distribution Dashboard
- Executive Dashboard

---

# KPIs Supported

- Total Customers
- Monthly Registrations
- Customer Distribution by Education
- Customer Distribution by Location
- Gender Distribution

---

# ETL Considerations

- Preserve customer identifiers.
- Validate education references.
- Validate location references.
- Standardize gender values.
- Validate registration timestamps and birth dates.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Confidential | Contains customer demographic information |

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

- educations
- cities

### Referenced By

- application

---

# AI & RAG Notes

The **Users** table contains customer demographic and registration information.

It enables AI systems to:

- Generate BigQuery SQL involving customer data.
- Analyze customer demographics.
- Produce registration trend reports.
- Join customer information with applications, education, and location data.
- Support customer segmentation and lending analytics.

---

# Related Documentation

- Application Table
- Educations Table
- Cities Table
- Provinces Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Users** table stores customer demographic and registration information, including registration date, gender, date of birth, education level, and location. It acts as the central customer master table and supports lending operations, demographic analysis, reporting, and AI-assisted SQL generation.
