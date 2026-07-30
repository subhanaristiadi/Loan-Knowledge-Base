# Relationship Matrix

> **Project:** Loan Knowledge Base
>
> **Module:** Database Schema
>
> **Version:** 2.0
>
> **Purpose:** Provide a complete matrix of relationships between database tables, including cardinality, foreign keys, and business meaning.

---

# Overview

The Relationship Matrix summarizes every relationship within the Loan Management database.

It helps developers, analysts, database administrators, and AI assistants quickly understand:

- Parent and child tables
- Primary keys
- Foreign keys
- Cardinality
- Referential integrity
- Business meaning

This document complements the Entity Relationship Diagram (ERD) by presenting relationships in a tabular format.

---

# Relationship Summary

| Parent Table | Child Table | Foreign Key | Cardinality | Required |
|---------------|-------------|-------------|-------------|----------|
| Provinces | Cities | `province_id` | 1 : Many | Yes |
| Cities | Users | `city_id` | 1 : Many | Yes |
| Educations | Users | `education_id` | 1 : Many | Yes |
| Users | Application | `user_id` | 1 : Many | Yes |
| Reason | Application | `reason_id` | 1 : Many | Yes |
| Application | Application History | `application_id` | 1 : Many | Yes |
| Application | Loans | `application_id` | 1 : 1 *(logical)* | Yes |
| Loan Status | Loans | `loan_status_id` | 1 : Many | Yes |
| Loans | Payments | `loan_id` | 1 : Many | Yes |
| Payment Status | Payments | `payment_status_id` | 1 : Many | Yes |
| Payment Methods | Payments | `payment_method_id` | 1 : Many | Yes |

---

# Relationship Matrix

| Parent Table | Cities | Provinces | Educations | Users | Application | Application History | Loans | Payments | Reason | Loan Status | Payment Status | Payment Methods |
|--------------|:------:|:---------:|:----------:|:----:|:-----------:|:-------------------:|:-----:|:--------:|:------:|:-----------:|:--------------:|:---------------:|
| Provinces | ✓ | — | | | | | | | | | | |
| Cities | | — | | ✓ | | | | | | | | |
| Educations | | | — | ✓ | | | | | | | | |
| Users | | | | — | ✓ | | | | | | | |
| Application | | | | | — | ✓ | ✓ | | | | | |
| Application History | | | | | | — | | | | | | |
| Loans | | | | | | | — | ✓ | | | | |
| Payments | | | | | | | | — | | | | |
| Reason | | | | | ✓ | | | | — | | | |
| Loan Status | | | | | | | ✓ | | | — | | |
| Payment Status | | | | | | | | ✓ | | | — | |
| Payment Methods | | | | | | | | ✓ | | | | — |

**Legend**

- ✓ = Direct relationship exists
- — = Same table / not applicable
- Blank = No direct relationship

---

# Relationship Details

## 1. Provinces → Cities

### Relationship

```text
Province (1)

↓

Cities (Many)
```

### Foreign Key

```text
Cities.province_id
```

### Business Meaning

Each province can contain many cities, while every city belongs to exactly one province.

---

## 2. Cities → Users

### Relationship

```text
Cities (1)

↓

Users (Many)
```

### Foreign Key

```text
Users.city_id
```

### Business Meaning

Customers are associated with a city of residence.

---

## 3. Educations → Users

### Relationship

```text
Educations (1)

↓

Users (Many)
```

### Foreign Key

```text
Users.education_id
```

### Business Meaning

Each customer references one education level from the master table.

---

## 4. Users → Application

### Relationship

```text
Users (1)

↓

Application (Many)
```

### Foreign Key

```text
Application.user_id
```

### Business Meaning

A customer may submit multiple loan applications over time.

---

## 5. Reason → Application

### Relationship

```text
Reason (1)

↓

Application (Many)
```

### Foreign Key

```text
Application.reason_id
```

### Business Meaning

Every application must specify one valid loan purpose.

---

## 6. Application → Application History

### Relationship

```text
Application (1)

↓

Application History (Many)
```

### Foreign Key

```text
Application_History.application_id
```

### Business Meaning

Every status change or important event in the application process is recorded as a history entry.

---

## 7. Application → Loans

### Relationship

```text
Application (1)

↓

Loans (1)
```

### Foreign Key

```text
Loans.application_id
```

### Business Meaning

Only approved applications generate a loan.

From a business perspective, one approved application creates one loan. If rejected applications remain in the Application table, the physical relationship is effectively **1 : 0..1**.

---

## 8. Loan Status → Loans

### Relationship

```text
Loan Status (1)

↓

Loans (Many)
```

### Foreign Key

```text
Loans.loan_status_id
```

### Business Meaning

Each loan has exactly one current status, while many loans may share the same status.

---

## 9. Loans → Payments

### Relationship

```text
Loans (1)

↓

Payments (Many)
```

### Foreign Key

```text
Payments.loan_id
```

### Business Meaning

A loan typically has multiple repayment transactions throughout its lifecycle.

---

## 10. Payment Status → Payments

### Relationship

```text
Payment Status (1)

↓

Payments (Many)
```

### Foreign Key

```text
Payments.payment_status_id
```

### Business Meaning

Each payment is assigned one status, such as **Pending**, **Paid**, **Failed**, or **Overdue**.

---

## 11. Payment Methods → Payments

### Relationship

```text
Payment Methods (1)

↓

Payments (Many)
```

### Foreign Key

```text
Payments.payment_method_id
```

### Business Meaning

Each payment is made through one payment channel, while a payment method can be used by many payments.

---

# Cardinality Summary

| Relationship | Cardinality |
|--------------|-------------|
| Province → City | 1 : Many |
| City → User | 1 : Many |
| Education → User | 1 : Many |
| User → Application | 1 : Many |
| Reason → Application | 1 : Many |
| Application → Application History | 1 : Many |
| Application → Loan | 1 : 0..1 *(business rule)* |
| Loan Status → Loan | 1 : Many |
| Loan → Payment | 1 : Many |
| Payment Status → Payment | 1 : Many |
| Payment Method → Payment | 1 : Many |

---

# Referential Integrity Rules

The following constraints should be enforced:

- Every foreign key must reference an existing parent record.
- Orphan records should not exist.
- Primary keys must be unique.
- Mandatory foreign keys should not be `NULL`, unless explicitly allowed by the business model.
- Deleting parent records should be restricted or carefully managed to preserve historical data.

---

# Relationship Hierarchy

```text
Province
    │
    ▼
City
    │
    ▼
User
    │
    ▼
Application
    │
    ├──────────────► Application History
    │
    ▼
Loan
    │
    ▼
Payment
```

Supporting master tables:

```text
Education ─────► User

Reason ────────► Application

Loan Status ───► Loan

Payment Status ─► Payment

Payment Methods ─► Payment
```

---

# Analytical Implications

Understanding these relationships enables analysts to:

- Build accurate JOIN queries.
- Calculate KPIs consistently.
- Design normalized dashboards.
- Trace customer activity from registration to loan closure.
- Analyze payment performance.
- Perform regional and demographic analysis.
- Maintain referential integrity during ETL and reporting.

---

# AI & RAG Notes

This matrix provides structured relationship metadata that helps AI assistants:

- Select the correct tables for SQL generation.
- Recommend appropriate JOIN paths.
- Explain database relationships.
- Validate analytical queries.
- Reduce schema-related hallucinations in Retrieval-Augmented Generation (RAG).

---

# Related Documentation

- Loan ERD
- Database Overview
- Database Schema
- Table Documentation
- Business Rules
- Loan Lifecycle
- SQL Cookbook

---

# Summary

The Relationship Matrix provides a consolidated view of every table relationship in the Loan Management database. By documenting parent-child relationships, foreign keys, cardinality, and business meaning, it serves as a practical reference for database design, SQL development, Business Intelligence, and AI-assisted analytics.
