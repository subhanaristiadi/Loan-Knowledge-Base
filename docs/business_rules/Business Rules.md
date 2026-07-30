
# Business Rules

> **Project:** Loan Knowledge Base
>
> **Module:** Business Rules
>
> **Version:** 2.0
>
> **Purpose:** Define the business rules, constraints, validations, and operational standards governing the Loan Management System.

---

# Overview

Business Rules define how the Loan Management System should behave from both operational and business perspectives.

These rules ensure:

- Data consistency
- Business process standardization
- Reliable reporting
- Regulatory compliance
- High-quality analytics
- Accurate AI-generated SQL

This document describes the logical business rules independent of any programming language or database implementation.

---

# Business Domains

The rules in this document are grouped into the following domains:

- Customer Management
- Loan Applications
- Loan Processing
- Loan Portfolio
- Payment Processing
- Status Management
- Geographic Data
- Data Integrity
- Reporting & Analytics

---

# Customer Management Rules

## BR-001 — Customer Registration

Every loan application must belong to a registered customer.

**Rule**

- One customer can submit multiple loan applications.
- A loan application cannot exist without a customer record.

Relationship

```text
Users
    │
    ▼
Applications
```

---

## BR-002 — Customer Identity

Each customer must have a unique identifier.

Expected constraint:

```text
user_id
```

must be unique.

---

## BR-003 — Customer Demographics

Every customer should reference valid demographic information.

Examples:

- Education
- City
- Province

Lookup values must exist in their respective master tables.

---

# Loan Application Rules

## BR-004 — Application Ownership

Each application belongs to exactly one customer.

```text
Users (1)

↓

Applications (Many)
```

---

## BR-005 — Loan Purpose

Every application must specify a valid loan purpose.

Example:

```text
reason_id

↓

Reason
```

Applications without a valid reason should not proceed to approval.

---

## BR-006 — Mandatory Information

Applications should contain:

- Requested loan amount
- Loan period
- Monthly income
- Monthly expenses
- Loan purpose

Missing mandatory information prevents further processing.

---

## BR-007 — Multiple Applications

A customer may submit multiple applications over time.

Business recommendation:

- Multiple active applications should be monitored.
- Duplicate submissions within a short period should be reviewed.

---

# Application History Rules

## BR-008 — Audit Trail

Every significant application event should be recorded.

Examples:

- Submitted
- Documents Verified
- Credit Assessment
- Approved
- Rejected
- Loan Created

---

## BR-009 — Immutable History

Historical records should never be deleted or overwritten.

Corrections should create a new history record rather than modifying an existing one.

---

# Approval Rules

## BR-010 — Approval Eligibility

Only applications satisfying all validation requirements may be approved.

Minimum validation includes:

- Customer exists
- Documents complete
- Eligibility passed
- Credit assessment completed

---

## BR-011 — One Approved Application → One Loan

Each approved application creates one loan record.

```text
Application

↓

Loan
```

---

## BR-012 — Rejected Applications

Rejected applications do not create loans.

Their status should remain available for reporting and auditing.

---

# Loan Rules

## BR-013 — Loan Ownership

Each loan originates from exactly one application.

Expected relationship:

```text
Loans.applications_id

↓

Application.applications_id
```

---

## BR-014 — Loan Status

Every loan must have one valid status.

Examples:

- Active
- Closed
- Default
- Cancelled

Status values should be stored in the **Loan Status** master table.

---

## BR-015 — Loan Amount

Loan amount should always be greater than zero.

Recommended validation:

```text
loan_amount > 0
```

---

## BR-016 — Credit Score

If a credit score is used:

- It must fall within the organization's accepted range.
- Invalid values should be rejected during processing.

---

# Payment Rules

## BR-017 — Loan Payments

Payments cannot exist without a loan.

Relationship

```text
Loans

↓

Payments
```

---

## BR-018 — Payment Status

Every payment must reference a valid payment status.

Examples:

- Pending
- Paid
- Failed
- Overdue

---

## BR-019 — Payment Method

Each payment should specify the payment channel.

Examples:

- Bank Transfer
- Virtual Account
- E-Wallet
- Cash

---

## BR-020 — Payment Amount

Payment amount should never be negative.

Recommended validation:

```text
paid_amount >= 0
```

---

## BR-021 — Due Amount

Due amount should never be negative.

---

## BR-022 — Interest Amount

Interest should be calculated according to the organization's lending policy.

Negative interest values are not allowed.

---

## BR-023 — Late Fees

Late fees should only be applied when payment occurs after the due date.

---

# Geographic Rules

## BR-024 — City

Every customer should belong to one city.

---

## BR-025 — Province

Every city should belong to one province.

Expected relationship:

```text
Province

↓

City

↓

Customer
```

---

# Data Integrity Rules

## BR-026 — Primary Keys

Primary keys must be unique.

Examples:

- user_id
- application_id
- loan_id
- payment_id

---

## BR-027 — Foreign Keys

Foreign keys must reference valid parent records.

No orphan records should exist.

---

## BR-028 — Duplicate Records

Duplicate business transactions should be avoided.

Examples:

- Duplicate loan
- Duplicate payment
- Duplicate application

---

## BR-029 — Date Consistency

Chronological order should always be maintained.

Examples:

```text
Customer Registration

↓

Application

↓

Loan

↓

Payment
```

Invalid examples:

- Payment before loan creation.
- Loan before application.
- Application before customer registration.

---

# Reporting Rules

## BR-030 — Historical Reporting

Reports should preserve historical values and status changes.

Historical transactions should not be removed from analytical reporting.

---

## BR-031 — Consistent KPI Definitions

All dashboards should use standardized KPI formulas.

Examples:

- Approval Rate
- Collection Rate
- Default Rate
- Outstanding Balance

---

## BR-032 — Time-Based Reporting

Reports should support aggregation by:

- Day
- Week
- Month
- Quarter
- Year

---

# AI & Analytics Rules

## BR-033 — RAG Documentation

All documentation should be written in Markdown to maximize compatibility with vector databases and Retrieval-Augmented Generation (RAG).

---

## BR-034 — SQL Consistency

SQL examples throughout the knowledge base should:

- Use descriptive aliases.
- Follow ANSI SQL where possible.
- Be easy to adapt to PostgreSQL, MySQL, SQL Server, or BigQuery.

---

## BR-035 — Business Terminology

Business terms should remain consistent across all documentation.

Examples:

- Customer
- Application
- Loan
- Payment
- Outstanding Balance
- Collection Rate
- Default Rate

---

# Business Rule Dependency

```text
Customer
      │
      ▼
Application
      │
      ▼
Approval
      │
      ▼
Loan
      │
      ▼
Payment
      │
      ▼
Reporting
      │
      ▼
Business Intelligence
```

---

# Rule Validation Checklist

| Validation | Status |
|------------|--------|
| Customer Exists | ✓ |
| Required Fields Complete | ✓ |
| Foreign Keys Valid | ✓ |
| Primary Keys Unique | ✓ |
| Loan Amount Valid | ✓ |
| Payment Amount Valid | ✓ |
| Status Codes Valid | ✓ |
| Date Sequence Valid | ✓ |
| Duplicate Check | ✓ |
| Historical Records Preserved | ✓ |

---

# Related Documentation

- Approval Process
- Loan Lifecycle
- Loan ERD
- Database Schema
- KPI Catalog
- Business Questions
- SQL Cookbook
- Data Quality Guide

---

# Summary

This document defines the core business rules governing the Loan Management System. These rules establish a consistent framework for customer registration, loan applications, approvals, loan servicing, payment processing, data integrity, reporting, and AI-assisted analytics. Maintaining these standards ensures reliable operations, accurate business reporting, and high-quality SQL generation for Business Intelligence and Retrieval-Augmented Generation (RAG) applications.
