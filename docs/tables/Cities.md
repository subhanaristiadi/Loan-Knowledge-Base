# Cities Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `cities`
>
> **Version:** 2.0

---

# Overview

The **Cities** table is a master reference table that stores city and municipality information used throughout the Loan Management System.

Each city belongs to exactly one province and can be referenced by many customers.

The table standardizes geographic information to ensure consistent reporting, filtering, and data integrity across the database.

---

# Business Purpose

The Cities table provides standardized geographic reference data for customer addresses and regional analysis.

Business objectives include:

- Standardizing city names
- Preventing duplicate city records
- Supporting customer location management
- Enabling regional reporting
- Supporting dashboard filters
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | cities |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | provinces |
| Child Table | users |
| Estimated Volume | Medium |
| Update Frequency | Low |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | City identifier |
| province_id | BIGINT | No | | ✓ | Province identifier |
| city_name | VARCHAR(150) | No | | | City or municipality name |

---

# Column Descriptions

## id

**Description**

Unique identifier for each city.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## province_id

**Description**

References the province where the city is located.

**References**

```text
provinces.id
```

**Business Rules**

- Province must exist
- Required field
- Foreign key enforced

---

## city_name

**Description**

Official city or municipality name.

Examples:

- Jakarta Selatan
- Bandung
- Surabaya
- Kupang
- Denpasar

**Business Rules**

- Required
- Should be unique within the same province
- Use official government naming
- Remove leading and trailing spaces

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique city identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| province_id | provinces.id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| provinces | Many-to-One | City belongs to one province |
| users | One-to-Many | One city may have many customers |

---

# Entity Relationship

```text
provinces
     │
     │ province_id
     ▼
cities
     │
     │ id
     ▼
users
```

---

# Business Rules

- Every city must belong to one province.
- A city cannot exist without a valid province.
- City names should follow official administrative names.
- Duplicate city names within the same province should not be allowed.
- Customers must reference an existing city.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Province | province_id cannot be NULL |
| Required Name | city_name cannot be NULL |
| Unique Combination | province_id + city_name should be unique |
| Valid Province | Referenced province must exist |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| FOREIGN KEY | province_id |
| NOT NULL | Required columns |
| UNIQUE | province_id + city_name |

Example:

```sql
UNIQUE (province_id, city_name)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_cities | id | Primary key lookup |
| idx_cities_province | province_id | Province filtering |
| idx_cities_name | city_name | City search |
| idx_cities_province_name | province_id, city_name | Duplicate prevention and reporting |

---

# Sample Records

| id | province_id | city_name |
|---:|------------:|-----------|
| 1 | 31 | Jakarta Selatan |
| 2 | 32 | Bandung |
| 3 | 35 | Surabaya |
| 4 | 53 | Kupang |
| 5 | 51 | Denpasar |

---

# Common SQL Queries

## View All Cities

```sql
SELECT *
FROM cities;
```

---

## Cities by Province

```sql
SELECT
    p.province_name,
    c.city_name
FROM cities c
JOIN provinces p
    ON c.province_id = p.id
ORDER BY
    p.province_name,
    c.city_name;
```

---

## Number of Cities per Province

```sql
SELECT
    p.province_name,
    COUNT(c.id) AS total_cities
FROM provinces p
LEFT JOIN cities c
    ON p.id = c.province_id
GROUP BY p.province_name
ORDER BY total_cities DESC;
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

# Reporting Usage

This table is commonly used in:

- Customer Demographics
- Geographic Analysis
- Regional Performance Dashboard
- Executive Dashboard
- Customer Distribution Report
- Loan Portfolio by Region

---

# KPIs Supported

- Customers by City
- Customers by Province
- Loan Applications by City
- Loan Portfolio by Region
- Regional Approval Rate
- Regional Collection Performance

---

# ETL Considerations

- Load provinces before cities.
- Validate province references.
- Standardize city names.
- Prevent duplicate records.
- Preserve official administrative naming.

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
| Deletion Policy | Soft delete or administrative update only |

---

# Dependencies

### Depends On

- provinces

### Referenced By

- users

---

# AI & RAG Notes

The **Cities** table provides standardized geographic information that enables AI systems to:

- Generate location-based SQL queries.
- Explain customer geographic distribution.
- Support regional business analysis.
- Recommend joins between customers, cities, and provinces.
- Produce dashboards segmented by location.

---

# Related Documentation

- Provinces Table
- Users Table
- Database Schema
- Relationship Matrix
- Data Dictionary
- Executive Dashboard

---

# Summary

The **Cities** table is a master reference table that stores standardized city and municipality information. It maintains geographic consistency across the Loan Management System by linking each city to a province and serving as the location reference for customers, enabling accurate reporting, regional analysis, and reliable referential integrity.
