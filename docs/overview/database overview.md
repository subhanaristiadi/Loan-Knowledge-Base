# Database Overview

> **Project:** Loan Knowledge Base
>
> **Module:** Overview
>
> **Version:** 2.0
>
> **Purpose:** Provide a high-level overview of the Loan Management System database, including its objectives, architecture, core entities, relationships, and analytical capabilities.

---

# Overview

The Loan Management System database is designed to manage the complete lifecycle of a loan, from customer registration through loan repayment and closure.

It serves as the central repository for operational, financial, and analytical data, supporting:

- Customer Management
- Loan Processing
- Payment Management
- Risk Analysis
- Business Intelligence
- Executive Reporting
- AI-powered Analytics

The database follows a normalized relational design to ensure data integrity, minimize redundancy, and simplify analytical reporting.

---

# Database Objectives

The database is designed to support the following business objectives:

- Store customer information.
- Record loan applications.
- Track application approval history.
- Manage active loans.
- Record loan repayments.
- Monitor loan performance.
- Support operational reporting.
- Enable Business Intelligence.
- Provide structured knowledge for AI and RAG systems.

---

# Database Architecture

```text
                 Loan Management Database

                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
   Master Tables   Transaction Tables   Reference Data
        │                │                │
        └────────────────┼────────────────┘
                         ▼
                  Business Processes
                         │
                         ▼
                  SQL & Analytics
                         │
                         ▼
                 Dashboards & Reports
                         │
                         ▼
                      AI / RAG
```

---

# Database Layers

The database can be viewed as four logical layers.

```text
Reference Layer

↓

Master Data Layer

↓

Transaction Layer

↓

Analytics Layer
```

---

# Reference Layer

Reference tables contain standardized values used throughout the system.

Typical tables include:

| Table | Purpose |
|---------|----------|
| Provinces | Province master data |
| Cities | City master data |
| Educations | Education levels |
| Reason | Loan purposes |
| Loan Status | Loan status definitions |
| Payment Status | Payment status definitions |
| Payment Methods | Payment channel definitions |

Reference data changes infrequently and ensures consistency across transactions.

---

# Master Data Layer

The Master Data Layer stores long-lived business entities.

| Table | Description |
|---------|-------------|
| Users | Registered customers |

Customer information is referenced by loan applications and other business processes.

---

# Transaction Layer

Transaction tables capture business events over time.

| Table | Description |
|---------|-------------|
| Application | Loan applications |
| Application History | Application status history |
| Loans | Approved loans |
| Payments | Loan repayment transactions |

These tables continuously grow as business transactions occur.

---

# Analytics Layer

The Analytics Layer supports reporting and Business Intelligence.

Typical outputs include:

- KPIs
- Portfolio Reports
- Collection Reports
- Risk Reports
- Executive Dashboards
- Customer Analytics
- Geographic Analytics

This layer is primarily driven by SQL queries, database views, and reporting tools.

---

# Core Business Entities

The system revolves around four primary entities.

```text
Customer

↓

Application

↓

Loan

↓

Payment
```

Each entity represents a major stage in the lending process.

---

# Entity Relationships

```text
Users
   │
   ▼
Applications
   │
   ▼
Loans
   │
   ▼
Payments
```

Supporting reference relationships:

```text
Province
   │
   ▼
City
   │
   ▼
Users

Reason
   │
   ▼
Applications

Loan Status
   │
   ▼
Loans

Payment Status
   │
   ▼
Payments

Payment Methods
   │
   ▼
Payments
```

---

# Database Flow

The operational flow follows the complete loan lifecycle.

```text
Customer Registration

↓

Loan Application

↓

Application Validation

↓

Approval Process

↓

Loan Creation

↓

Loan Servicing

↓

Payment Processing

↓

Loan Closure
```

Each stage generates transactional data that supports reporting and historical analysis.

---

# Normalization

The database follows relational database design principles.

### Goals

- Eliminate duplicate data.
- Preserve referential integrity.
- Simplify maintenance.
- Improve query consistency.
- Support scalable reporting.

Reference tables are separated from transaction tables to reduce redundancy.

---

# Primary Keys

Each table should have a unique primary key.

Examples:

| Table | Primary Key |
|---------|-------------|
| Users | `user_id` |
| Application | `application_id` |
| Application History | `application_history_id` |
| Loans | `loan_id` |
| Payments | `payment_id` |

---

# Foreign Keys

Foreign keys define relationships between tables.

Examples:

| Child Table | Parent Table |
|--------------|--------------|
| Application | Users |
| Application | Reason |
| Loans | Application |
| Loans | Loan Status |
| Payments | Loans |
| Payments | Payment Status |
| Payments | Payment Methods |
| Cities | Provinces |
| Users | Cities |
| Users | Educations |

---

# Data Categories

The database stores several categories of information.

### Customer Data

- Personal information
- Education
- Geographic information

### Application Data

- Requested loan amount
- Loan purpose
- Income
- Expenses
- Application status

### Loan Data

- Approved amount
- Interest rate
- Loan period
- Outstanding balance
- Loan status

### Payment Data

- Payment amount
- Due amount
- Interest paid
- Payment status
- Payment method
- Payment date

---

# Business Capabilities

The database supports:

- Customer management
- Loan processing
- Credit evaluation
- Loan servicing
- Payment collection
- Portfolio monitoring
- Financial reporting
- Risk management
- Geographic analysis

---

# Analytical Capabilities

Example analyses include:

- Customer segmentation
- Loan approval trends
- Monthly loan growth
- Collection performance
- Default analysis
- Revenue analysis
- Regional performance
- Payment behavior
- Loan portfolio composition

---

# Typical SQL Workloads

The database is suitable for:

- Operational reporting
- Dashboard development
- KPI calculation
- Executive reporting
- Time-series analysis
- Cohort analysis
- Ranking and window functions
- Financial analysis

---

# Technology Compatibility

The schema is designed to work with common relational database systems.

Supported platforms include:

- PostgreSQL
- MySQL
- MariaDB
- SQL Server
- Oracle Database
- SQLite (for learning purposes)

---

# AI & RAG Compatibility

The structured documentation supports AI assistants by providing:

- Table definitions
- Relationship mappings
- Business rules
- SQL examples
- KPI definitions
- Dashboard specifications
- Business terminology

This enables more accurate SQL generation, documentation retrieval, and business question answering through Retrieval-Augmented Generation (RAG).

---

# Related Documentation

- System Architecture
- Loan ERD
- Database Schema
- Business Rules
- Loan Lifecycle
- Business Glossary
- KPI Catalog
- Dashboard Ideas
- SQL Cookbook

---

# Summary

The Loan Management System database provides a normalized relational foundation for managing customers, loan applications, loans, and repayments. Its layered architecture separates reference data, master data, transactional data, and analytics, enabling reliable operations, scalable reporting, and advanced Business Intelligence. Combined with comprehensive documentation, the database also serves as a robust knowledge source for AI-powered analytics and Retrieval-Augmented Generation (RAG).
