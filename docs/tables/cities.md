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

The **Cities** table stores the list of cities used throughout the Loan Management System.

It functions as a master reference table that standardizes customer location information and supports geographical reporting and analysis.

Each city belongs to a province and can be referenced by multiple customers.

---

# Business Purpose

The Cities table maintains the master list of cities.

Business objectives include:

- Standardizing city information
- Supporting customer location data
- Supporting geographical reporting
- Reducing duplicate location values
- Supporting regional analysis

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | cities |
| Module | Master Data |
| Type | Master Table |
| Primary Key | locations_id |
| Parent Table | provinces |
| Child Tables | users |
| Estimated Volume | Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| locations_id | INTEGER | No | ✓ | | Unique city identifier |
| province_id | INTEGER | No | | ✓ | References the province |
| city | STRING | No | | | City name |

---

# Column Descriptions

## locations_id

**Description**

Unique identifier for each city.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## province_id

**Description**

References the province where the city is located.

**References**

```
provinces.province_id
```

**Business Rules**

- Required
- Must reference an existing province

---

## city

**Description**

Official name of the city.

**Business Rules**

- Required
- Cannot be NULL
- Should follow official naming conventions

---

# Primary Key

| Column | Description |
|---------|-------------|
| locations_id | Unique city identifier |

---

# Foreign Keys

| Column | References |
|---------|------------|
| province_id | provinces.province_id |

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| provinces | Many-to-One | Each city belongs to one province |
| users | One-to-Many | One city can have many users |

---

# Entity Relationship

```text
provinces
      │
      │ province_id
      ▼
cities
      │
      │ locations_id
      ▼
users
```

---

# Business Rules

- Every city belongs to one province.
- City names should be standardized.
- Every customer location should reference an existing city.
- City records should not be deleted if referenced by users.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Province | province_id cannot be NULL |
| Required City Name | city cannot be NULL |
| Unique City ID | locations_id must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | locations_id |
| FOREIGN KEY | province_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_cities | locations_id | Primary key lookup |
| idx_cities_province | province_id | Province filtering |
| idx_cities_name | city | City search |

---

# Common SQL Queries

## View All Cities

```sql
SELECT *
FROM `crediu-504100.Crediu.Cities`;
```

---

## Cities by Province

```sql
SELECT
    province_id,
    COUNT(*) AS total_cities
FROM `crediu-504100.Crediu.Cities`
GROUP BY province_id
ORDER BY total_cities DESC;
```

---

## Search City

```sql
SELECT *
FROM `crediu-504100.Crediu.Cities`
WHERE city = 'Surabaya';
```

---

# Reporting Usage

This table is frequently used in:

- Customer Distribution Report
- Regional Dashboard
- Province Analysis
- Customer Demographics
- Geographic Reporting

---

# KPIs Supported

- Total Cities
- Cities per Province
- Customer Distribution by City
- Regional Customer Coverage

---

# ETL Considerations

- Preserve city identifiers.
- Validate province references before loading.
- Prevent duplicate city records.
- Standardize city names.

---

# Security Classification

| Classification | Description |
|----------------|-------------|
| Internal | Master reference data |

---

# Data Retention

| Item | Policy |
|------|--------|
| Retention Period | Permanent |
| Archive Policy | Not Applicable |
| Deletion Policy | Soft Delete Recommended |

---

# Dependencies

### Depends On

- provinces

### Referenced By

- users

---

# AI & RAG Notes

The **Cities** table provides standardized geographical reference data for customer locations.

It enables AI systems to:

- Generate BigQuery SQL involving customer locations.
- Analyze customer distribution by city.
- Produce regional reports.
- Support geographical analytics.
- Join customer and province information accurately.

---

# Related Documentation

- Provinces Table
- Users Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Cities** table is a master reference table containing standardized city information. It links cities to provinces and provides the geographical foundation for customer location management, reporting, analytics, and AI-assisted SQL generation.
