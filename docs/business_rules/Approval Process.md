# Approval Process

> **Project:** Loan Knowledge Base
>
> **Module:** Business Rules
>
> **Version:** 2.0
>
> **Purpose:** Define the end-to-end loan approval workflow, business rules, decision criteria, and status transitions used in the Loan Management System.

---

# Overview

The Approval Process governs how a loan application progresses from submission to either approval or rejection.

Its objectives are to:

- Ensure every application follows a standardized review process.
- Reduce operational risk.
- Improve decision consistency.
- Maintain a complete audit trail.
- Support regulatory compliance.

---

# Business Workflow

```text
Customer Registration
        │
        ▼
Submit Loan Application
        │
        ▼
Initial Validation
        │
        ▼
Document Verification
        │
        ▼
Eligibility Assessment
        │
        ▼
Credit Assessment
        │
        ▼
Approval Decision
   ┌──────────────┐
   │              │
Approved      Rejected
   │              │
   ▼              ▼
Create Loan   Close Application
   │
   ▼
Loan Active
```

---

# Approval Lifecycle

| Stage | Description |
|---------|-------------|
| Submitted | Customer submits a new application. |
| Validation | Required fields are validated. |
| Document Verification | Supporting documents are reviewed. |
| Eligibility Review | Customer eligibility is evaluated. |
| Credit Assessment | Creditworthiness is assessed. |
| Decision | Application is approved or rejected. |
| Loan Creation | Approved applications become loans. |

---

# Business Rule 1 — Customer Registration

A customer must exist before submitting a loan application.

Relationship:

```text
Users
    │
    ▼
Applications
```

Validation:

- Customer ID must exist.
- Customer account must be active.

---

# Business Rule 2 — Required Information

A loan application cannot proceed if mandatory information is missing.

Examples:

- Customer ID
- Loan purpose
- Monthly income
- Monthly expenses
- Requested loan amount
- Loan period

Applications with incomplete information remain in **Pending Validation**.

---

# Business Rule 3 — Document Verification

Required documents should be verified before eligibility assessment.

Typical documents include:

- Government-issued ID
- Proof of income
- Proof of address
- Supporting financial documents

Possible outcomes:

- Verified
- Incomplete
- Rejected

---

# Business Rule 4 — Eligibility Assessment

Applicants are evaluated against predefined business requirements.

Typical criteria:

- Minimum age
- Maximum age
- Valid customer profile
- Income above minimum threshold
- Expense-to-income ratio
- Required documentation completed

Failure to meet mandatory requirements results in rejection.

---

# Business Rule 5 — Credit Assessment

Credit assessment determines repayment capability.

Possible evaluation criteria:

- Credit score
- Existing obligations
- Income stability
- Previous repayment history
- Internal risk score

Possible outcomes:

- Low Risk
- Medium Risk
- High Risk

---

# Business Rule 6 — Approval Decision

Applications are classified into one of three outcomes.

| Decision | Description |
|-----------|-------------|
| Approved | Loan may be created. |
| Rejected | Application is closed. |
| Pending | Additional review required. |

---

# Business Rule 7 — Loan Creation

Only approved applications may generate a loan.

Relationship:

```text
Application

↓

Loan
```

Each approved application should create **one loan record**.

---

# Business Rule 8 — Application History

Every significant event must be recorded.

Examples:

- Submitted
- Validation Completed
- Documents Verified
- Credit Reviewed
- Approved
- Rejected
- Loan Created

These events are stored in **Application History**.

---

# Status Transition

```text
Submitted
     │
     ▼
Pending Validation
     │
     ▼
Document Verification
     │
     ▼
Eligibility Review
     │
     ▼
Credit Assessment
     │
     ▼
Decision
 ┌──────────────┐
 │              │
 ▼              ▼
Approved    Rejected
 │
 ▼
Loan Created
```

---

# Approval Matrix

| Validation | Documents | Eligibility | Credit | Result |
|------------|-----------|-------------|---------|--------|
| Pass | Pass | Pass | Pass | Approved |
| Pass | Fail | - | - | Rejected |
| Pass | Pass | Fail | - | Rejected |
| Pass | Pass | Pass | Fail | Rejected |
| Pending | - | - | - | Pending |

---

# Audit Requirements

Every approval decision should capture:

- Application ID
- Customer ID
- Decision
- Decision timestamp
- Reviewer (if applicable)
- Status
- Remarks

This information supports traceability and compliance.

---

# Risk Considerations

Examples of applications requiring additional review:

- Very high loan amount
- Extremely low credit score
- Multiple recent applications
- Inconsistent customer information
- Missing supporting documents

These cases may require manual approval.

---

# SQL Analysis Examples

Business questions supported by this process:

- What is the approval rate?
- What is the rejection rate?
- Which stage causes the most rejections?
- What is the average approval time?
- Which loan purpose has the highest approval rate?
- Which city has the highest approval rate?
- Which education level has the highest approval rate?

---

# KPI Impact

This approval workflow contributes to the following KPIs:

- Approval Rate
- Rejection Rate
- Average Processing Time
- Pending Applications
- Loan Conversion Rate
- Customer Conversion Rate

---

# AI & RAG Notes

This document enables AI assistants to:

- Explain the approval workflow.
- Generate SQL for approval analytics.
- Recommend operational improvements.
- Identify bottlenecks.
- Answer business process questions.
- Produce documentation-aware responses.

---

# Related Documentation

- Loan ERD
- Database Schema
- Business Rules
- KPI Catalog
- Business Questions
- SQL Cookbook
- Application Table Documentation

---

# Summary

The Approval Process defines the standard lifecycle of a loan application from submission through validation, eligibility assessment, credit evaluation, and final decision. By documenting each stage, decision point, and business rule, the organization ensures consistent loan processing, improved operational transparency, and accurate analytics for reporting, Business Intelligence, and AI-powered decision support.
