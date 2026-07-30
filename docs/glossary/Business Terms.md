# Business Terms

> **Project:** Loan Knowledge Base
>
> **Module:** Business Glossary
>
> **Version:** 2.0
>
> **Purpose:** Define standardized business terminology used throughout the Loan Management System to ensure consistent understanding across business users, analysts, developers, and AI assistants.

---

# Overview

This glossary provides standardized definitions for the business terms used in the Loan Management System.

The objectives of this glossary are to:

- Standardize business terminology.
- Improve communication between business and technical teams.
- Support SQL development.
- Improve dashboard consistency.
- Enhance AI-generated explanations.
- Optimize Retrieval-Augmented Generation (RAG).

Unless otherwise stated, these definitions represent generic lending concepts and should be adapted to match organizational policies.

---

# A

## Active Loan

A loan that has been approved, disbursed, and has not yet been fully repaid or closed.

---

## Applicant

A customer who submits a loan application.

---

## Application

A formal request submitted by a customer to obtain a loan.

An application exists before a loan is approved.

---

## Application History

A chronological record of every important event during the application process.

Examples include:

- Submitted
- Document Verified
- Credit Review
- Approved
- Rejected

---

## Approval

The business decision confirming that a loan application satisfies all required criteria and may proceed to loan creation.

---

## Approval Rate

The percentage of submitted applications that are approved.

Formula

```text
Approved Applications
─────────────────────
Total Applications
```

---

# B

## Borrower

A customer who has at least one approved loan.

---

## Business Rule

A policy or constraint that governs how the Loan Management System operates.

Examples:

- Every loan must belong to one application.
- Payments cannot exist without a loan.

---

# C

## Cash Flow

Movement of money into and out of the lending business.

Examples:

- Loan disbursement
- Loan repayment
- Interest collection

---

## Collection

The process of receiving repayments from borrowers.

---

## Collection Rate

The percentage of scheduled repayments successfully collected.

Formula

```text
Collected Amount
────────────────
Due Amount
```

---

## Credit Assessment

Evaluation of a customer's ability to repay a loan.

Typical inputs:

- Credit score
- Income
- Existing obligations
- Payment history

---

## Credit Score

A numerical indicator representing the estimated creditworthiness of a borrower.

Higher scores generally indicate lower credit risk.

---

## Customer

A registered user who may submit one or more loan applications.

---

# D

## Data Dictionary

Documentation describing database tables, columns, data types, and business meanings.

---

## Default

Failure to repay a loan according to agreed terms.

---

## Default Rate

The percentage of loans that enter default status.

Formula

```text
Default Loans
─────────────
Total Loans
```

---

## Delinquency

A payment that has not been made by its due date.

---

## Delinquency Rate

Percentage of loans with overdue payments.

---

## Disbursement

The process of releasing approved loan funds to the borrower.

---

# E

## Eligibility Assessment

Evaluation of whether an applicant satisfies minimum lending requirements.

Typical criteria include:

- Age
- Income
- Documentation
- Employment
- Internal policies

---

## Executive Dashboard

A high-level dashboard designed for executives to monitor overall business performance.

---

# F

## Foreign Key

A database column linking one table to another.

Example

```text
Applications.user_id

↓

Users.user_id
```

---

# G

## Geographic Analysis

Analysis of loan performance by location, such as city or province.

---

# I

## Installment

A scheduled repayment made during the loan period.

An installment typically includes:

- Principal
- Interest
- Fees (if applicable)

---

## Interest

The cost charged to a borrower for using borrowed funds.

---

## Interest Income

Revenue earned from loan interest payments.

---

# K

## KPI

Key Performance Indicator.

A measurable metric used to evaluate business performance.

Examples:

- Approval Rate
- Collection Rate
- Default Rate
- Outstanding Balance

---

# L

## Late Fee

A penalty charged when payment is received after the due date.

---

## Late Payment

A repayment made after the scheduled due date.

---

## Loan

A financial agreement created after an application has been approved.

---

## Loan Amount

The total amount of money borrowed by the customer.

---

## Loan Lifecycle

The complete journey of a loan from application through repayment and closure.

---

## Loan Period

The agreed repayment duration.

Common units:

- Months
- Years

---

## Loan Portfolio

The collection of all loans managed by the organization.

---

## Loan Purpose

The reason provided by a customer for requesting financing.

Examples:

- Education
- Business
- Medical
- Home Improvement

---

## Loan Status

The current stage of a loan.

Examples:

- Pending
- Active
- Closed
- Default
- Cancelled

---

# M

## Master Table

A reference table storing relatively static information.

Examples:

- Cities
- Provinces
- Payment Methods
- Loan Status

---

# O

## Outstanding Balance

The remaining unpaid balance of a loan.

Formula

```text
Loan Amount
-
Total Payments
```

---

## Overdue Payment

A payment that remains unpaid after its due date.

---

# P

## Partial Payment

A payment that covers only part of the scheduled amount due.

---

## Payment

A financial transaction made by a borrower toward repayment of a loan.

---

## Payment Method

The channel used to make a payment.

Examples:

- Bank Transfer
- Virtual Account
- Credit Card
- E-Wallet
- Cash

---

## Payment Schedule

The timetable showing all expected repayments during the loan period.

---

## Payment Status

The current condition of a payment.

Examples:

- Pending
- Paid
- Failed
- Overdue

---

## Portfolio

The complete set of loans managed by the organization.

---

## Principal

The original loan amount excluding interest and fees.

---

## Principal Amount

The portion of a payment applied directly to reduce the outstanding balance.

---

# R

## RAG

Retrieval-Augmented Generation.

A technique where an AI model retrieves relevant documentation before generating responses.

---

## Reason

The customer's stated purpose for requesting a loan.

---

## Repayment

The process of returning borrowed funds through scheduled payments.

---

## Revenue

Income generated from lending operations.

Typically includes:

- Interest
- Late Fees
- Service Charges

---

## Risk Assessment

The process of evaluating the likelihood that a borrower will fail to repay a loan.

---

# S

## SQL Cookbook

A collection of SQL examples for reporting and analytics.

---

## Status Transition

The movement of an entity from one state to another.

Example

```text
Pending

↓

Approved

↓

Active

↓

Closed
```

---

# T

## Transaction Table

A table containing business events that occur over time.

Examples:

- Applications
- Loans
- Payments
- Application History

---

# U

## User

A registered customer in the Loan Management System.

---

# V

## Validation

The process of ensuring submitted data satisfies business rules.

Examples:

- Required fields
- Valid foreign keys
- Positive loan amount
- Valid dates

---

# W

## Window Function

An SQL feature used for advanced analytical calculations without collapsing rows.

Common examples:

- RANK()
- ROW_NUMBER()
- LAG()
- LEAD()
- SUM() OVER()

---

# AI & RAG Notes

This glossary is intended to improve Retrieval-Augmented Generation by providing AI assistants with consistent definitions of business terminology. It reduces ambiguity, improves SQL generation, and ensures that analytical explanations use standardized language across the entire Loan Knowledge Base.

---

# Related Documentation

- Business Rules
- Loan Lifecycle
- Approval Process
- KPI Catalog
- Business Questions
- SQL Cookbook
- Loan ERD
- Database Schema

---

# Summary

The Business Glossary establishes a common vocabulary for the Loan Management System. By standardizing key business terms, metrics, and concepts, it supports accurate communication, consistent reporting, high-quality SQL development, and reliable AI-powered analytics. This glossary serves as a foundational knowledge source for both human users and Retrieval-Augmented Generation (RAG) systems.
