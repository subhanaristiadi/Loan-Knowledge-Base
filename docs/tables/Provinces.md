# Provinces Table

> **Project:** Loan Knowledge Base
>
> **Module:** Database Tables
>
> **Table:** `provinces`
>
> **Version:** 2.0

---

# Overview

The **Provinces** table is a master reference table that stores standardized province or state information used throughout the Loan Management System.

Each province can contain multiple cities and serves as the highest geographic level for customer location management, regional reporting, and business intelligence.

The table ensures consistent geographic classification across all modules and supports hierarchical location relationships.

---

# Business Purpose

The Provinces table provides standardized province-level geographic information.

Business objectives include:

- Standardizing province names
- Preventing duplicate province records
- Supporting geographic hierarchy
- Enabling regional analysis
- Improving reporting consistency
- Maintaining referential integrity

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | provinces |
| Module | Master Data |
| Type | Master Table |
| Primary Key | id |
| Parent Table | None |
| Child Table | cities |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| id | BIGINT | No | ✓ | | Province identifier |
| province_name | VARCHAR(150) | No | | | Province or state name |

---

# Column Descriptions

## id

**Description**

Unique identifier for each province.

**Business Rules**

- Auto-generated
- Unique
- Immutable

---

## province_name

**Description**

Official province or state name.

Examples:

- DKI Jakarta
- West Java
- East Java
- Bali
- East Nusa Tenggara

**Business Rules**

- Required
- Must be unique
- Follow official administrative naming
- Remove leading and trailing spaces

---

# Primary Key

| Column | Description |
|---------|-------------|
| id | Unique province identifier |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| cities | One-to-Many | One province may contain many cities |

---

# Entity Relationship

```text
provinces
      │
      │ id
      ▼
cities
      │
      ▼
users
```

---

# Business Rules

- Every province name must be unique.
- Province records should use official administrative names.
- A province may contain multiple cities.
- Cities cannot exist without a valid province.
- Province records should rarely change.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Name | province_name cannot be NULL |
| Unique Name | No duplicate province names |
| Standard Naming | Use official administrative names |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | id |
| UNIQUE | province_name |
| NOT NULL | province_name |

Example:

```sql
UNIQUE (province_name)
```

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_provinces | id | Primary key lookup |
| idx_provinces_name | province_name | Province search |

---

# Sample Records

| id | province_name |
|---:|---------------|
| 11 | Aceh |
| 31 | DKI Jakarta |
| 32 | West Java |
| 35 | East Java |
| 51 | Bali |
| 53 | East Nusa Tenggara |

---

# Common SQL Queries

## View All Provinces

```sql
SELECT *
FROM provinces;
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

## Number of Customers by Province

```sql
SELECT
    p.province_name,
    COUNT(u.id) AS total_customers
FROM provinces p
LEFT JOIN cities c
    ON p.id = c.province_id
LEFT JOIN users u
    ON c.id = u.city_id
GROUP BY p.province_name
ORDER BY total_customers DESC;
```

---

## Loan Portfolio by Province

```sql
SELECT
    p.province_name,
    SUM(l.approved_amount) AS portfolio_value
FROM loans l
JOIN application a
    ON l.application_id = a.id
JOIN users u
    ON a.user_id = u.id
JOIN cities c
    ON u.city_id = c.id
JOIN provinces p
    ON c.province_id = p.id
GROUP BY p.province_name
ORDER BY portfolio_value DESC;
```

---

# Reporting Usage

This table is commonly used in:

- Executive Dashboard
- Geographic Dashboard
- Regional Performance Dashboard
- Customer Distribution Report
- Loan Portfolio by Region
- Market Expansion Analysis

---

# KPIs Supported

- Customers by Province
- Loan Applications by Province
- Loan Portfolio by Province
- Approval Rate by Province
- Collection Rate by Province
- Regional Loan Growth

---

# ETL Considerations

- Load province master data before cities.
- Prevent duplicate province names.
- Validate official administrative naming.
- Preserve primary key consistency.
- Avoid unnecessary updates to master records.

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

- cities

---

# AI & RAG Notes

The **Provinces** table provides the highest geographic classification used in the Loan Management System. It enables AI systems to:

- Generate regional SQL queries.
- Produce geographic performance reports.
- Support customer distribution analysis.
- Recommend joins between provinces, cities, users, and loans.
- Build executive dashboards with regional insights.
- Improve AI understanding of geographic hierarchies.

---

# Related Documentation

- Cities Table
- Users Table
- Database Schema
- Relationship Matrix
- Executive Dashboard
- Geographic Analysis
- Data Dictionary

---

# Summary

The **Provinces** table is a master reference table that stores standardized province or state information used throughout the Loan Management System. As the top level of the geographic hierarchy, it ensures consistent location management, supports regional reporting and analytics, and provides the foundation for geographic segmentation in operational systems, business intelligence solutions, and AI-powered applications.
