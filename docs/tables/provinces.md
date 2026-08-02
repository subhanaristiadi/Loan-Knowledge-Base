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

The **Provinces** table stores the master list of provinces used throughout the Loan Management System.

It serves as a reference table that standardizes provincial information, ensuring consistent geographical data across customer records, city information, reporting, and analytics.

Each province is identified by a unique province identifier.

---

# Business Purpose

The Provinces table maintains standardized province information.

Business objectives include:

- Standardizing province data
- Supporting customer location management
- Supporting geographical reporting
- Preventing inconsistent province names
- Supporting regional analytics

---

# Table Information

| Property | Value |
|----------|-------|
| Table Name | provinces |
| Module | Master Data |
| Type | Master Table |
| Primary Key | province_id |
| Parent Table | None |
| Child Tables | cities |
| Estimated Volume | Very Low |
| Update Frequency | Rare |

---

# Table Structure

| Column | Data Type | Nullable | PK | FK | Description |
|----------|----------|----------|----|----|-------------|
| province_id | INTEGER | No | ✓ | | Unique province identifier |
| province | STRING | No | | | Province name |

---

# Column Descriptions

## province_id

**Description**

Unique identifier for each province.

**Business Rules**

- Must be unique
- Cannot be NULL
- Immutable after creation

---

## province

**Description**

Official name of the province.

Example values:

- Banten
- DKI Jakarta
- Jawa Barat
- Jawa Tengah
- Jawa Timur

**Business Rules**

- Required
- Cannot be NULL
- Should contain standardized province names

---

# Primary Key

| Column | Description |
|---------|-------------|
| province_id | Unique province identifier |

---

# Foreign Keys

None.

---

# Relationships

| Related Table | Relationship | Description |
|---------------|--------------|-------------|
| cities | One-to-Many | One province can contain many cities |

---

# Entity Relationship

```text
provinces
      │
      │ province_id
      ▼
cities
```

---

# Business Rules

- Every province must have a unique identifier.
- Province names should follow official administrative names.
- Every city should reference a valid province.
- Province records should not be deleted if they are referenced by city records.

---

# Data Quality Rules

| Rule | Description |
|------|-------------|
| Required Province ID | province_id cannot be NULL |
| Required Province Name | province cannot be NULL |
| Unique Province ID | province_id must be unique |

---

# Constraints

| Constraint | Description |
|------------|-------------|
| PRIMARY KEY | province_id |
| NOT NULL | Required columns |

---

# Recommended Indexes

| Index | Columns | Purpose |
|---------|----------|---------|
| pk_provinces | province_id | Primary key lookup |
| idx_province_name | province | Province search |

---

# Common SQL Queries

## View All Provinces

```sql
SELECT *
FROM `crediu-504100.Crediu.Provinces`;
```

---

## Count Provinces

```sql
SELECT
    COUNT(*) AS total_provinces
FROM `crediu-504100.Crediu.Provinces`;
```

---

## Search Province

```sql
SELECT *
FROM `crediu-504100.Crediu.Provinces`
WHERE province = 'DKI Jakarta';
```

---

# Reporting Usage

This table is frequently used in:

- Regional Dashboard
- Geographic Analysis
- Customer Distribution Report
- Province Summary Report
- Executive Dashboard

---

# KPIs Supported

- Total Provinces
- Customer Distribution by Province
- Cities per Province
- Regional Coverage

---

# ETL Considerations

- Preserve province identifiers.
- Prevent duplicate province records.
- Standardize province names.
- Validate province references before loading city data.

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

- None

### Referenced By

- cities

---

# AI & RAG Notes

The **Provinces** table provides standardized province information used throughout the Loan Management System.

It enables AI systems to:

- Generate BigQuery SQL involving province data.
- Analyze customer distribution by province.
- Produce regional reports.
- Join province information with city and customer data.
- Support geographical analytics.

---

# Related Documentation

- Cities Table
- Users Table
- Database Schema
- Relationship Matrix

---

# Summary

The **Provinces** table is a master reference table containing standardized province information. It provides the geographical foundation for regional reporting, customer location management, analytics, and AI-assisted SQL generation by serving as the parent reference for city data.
