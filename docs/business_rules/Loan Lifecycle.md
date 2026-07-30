# Loan Lifecycle

> **Project:** Loan Knowledge Base
>
> **Module:** Business Rules
>
> **Version:** 2.0
>
> **Purpose:** Describe the complete lifecycle of a loan, from customer registration through loan closure, including business events, status transitions, and operational responsibilities.

---

# Overview

The Loan Lifecycle defines every major stage a loan passes through during its existence.

Understanding this lifecycle helps:

- Standardize loan operations
- Improve business process consistency
- Support Business Intelligence reporting
- Generate accurate SQL queries
- Train AI assistants to understand business workflows
- Identify operational bottlenecks

---

# Loan Lifecycle Overview

```text
Customer Registration
        │
        ▼
Loan Application
        │
        ▼
Application Validation
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
    ┌─────────────┐
    │             │
Rejected     Approved
    │             │
    ▼             ▼
Application    Loan Creation
Closed              │
                    ▼
              Active Loan
                    │
                    ▼
           Payment Schedule
                    │
                    ▼
          Monthly Repayments
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
    Overdue Payment      On-Time Payment
          │                   │
          └─────────┬─────────┘
                    ▼
             Loan Settlement
                    │
                    ▼
               Loan Closed
```

---

# Lifecycle Stages

## Stage 1 — Customer Registration

### Objective

Create a valid customer profile before any loan application can be submitted.

### Primary Table

```text
Users
```

### Business Activities

- Register customer
- Validate identity
- Capture demographic information
- Assign education and location

### Outputs

- Valid customer record
- Unique customer ID

---

## Stage 2 — Loan Application

### Objective

Customer submits a request for financing.

### Primary Table

```text
Application
```

### Business Activities

- Select loan purpose
- Enter income
- Enter expenses
- Specify requested amount
- Choose repayment period

### Outputs

- New application
- Initial application status

---

## Stage 3 — Application Validation

### Objective

Verify that all required information has been provided.

### Validation Examples

- Required fields
- Customer exists
- Loan amount
- Income
- Expenses
- Loan purpose

### Possible Outcomes

- Passed
- Pending
- Failed

---

## Stage 4 — Document Verification

### Objective

Ensure all supporting documents are complete and valid.

Typical documents include:

- Identification
- Income verification
- Address verification

### Outcomes

- Verified
- Incomplete
- Rejected

---

## Stage 5 — Eligibility Assessment

### Objective

Determine whether the customer satisfies minimum lending requirements.

Typical checks include:

- Age
- Income
- Expense ratio
- Employment status
- Internal policy requirements

### Outcomes

- Eligible
- Not Eligible

---

## Stage 6 — Credit Assessment

### Objective

Evaluate the applicant's repayment capability.

Possible evaluation criteria:

- Credit score
- Debt level
- Previous repayment history
- Internal risk assessment

### Risk Categories

- Low Risk
- Medium Risk
- High Risk

---

## Stage 7 — Approval Decision

### Objective

Determine whether financing will be granted.

Possible decisions:

| Decision | Description |
|-----------|-------------|
| Approved | Loan may be created. |
| Rejected | Application is closed. |
| Pending Review | Manual assessment required. |

---

## Stage 8 — Loan Creation

### Objective

Generate a loan record for approved applications.

### Primary Table

```text
Loans
```

### Business Activities

- Assign loan ID
- Record loan amount
- Assign interest rate
- Assign loan period
- Set initial loan status

---

## Stage 9 — Active Loan

The loan is officially active.

During this stage:

- Outstanding balance is tracked.
- Payment schedule is monitored.
- Loan status is updated when necessary.

---

## Stage 10 — Payment Schedule

The repayment plan is generated.

Typical information includes:

- Installment number
- Due date
- Principal amount
- Interest amount
- Total due amount

---

## Stage 11 — Payment Processing

### Primary Table

```text
Payments
```

Business activities include:

- Receive payment
- Validate payment
- Update payment status
- Update outstanding balance

---

## Stage 12 — Payment Monitoring

Payment performance is monitored continuously.

Possible statuses:

- Paid
- Pending
- Failed
- Overdue
- Partial Payment

Operational monitoring includes:

- Late payments
- Missed installments
- Outstanding balances

---

## Stage 13 — Loan Settlement

A loan is considered settled when:

- Principal balance reaches zero.
- All scheduled payments are completed.
- All applicable fees are paid.

---

## Stage 14 — Loan Closure

### Objective

Finalize the loan.

Typical activities:

- Update loan status
- Archive loan
- Retain historical records
- Generate reporting metrics

Loan data should remain available for analytics and auditing.

---

# Lifecycle State Diagram

```text
Registered

↓

Application Submitted

↓

Validation

↓

Verification

↓

Eligibility

↓

Credit Review

↓

Approved

↓

Loan Created

↓

Active Loan

↓

Payments

↓

Completed

↓

Closed
```

Rejected applications follow a separate path:

```text
Application Submitted

↓

Validation

↓

Rejected

↓

Closed
```

---

# Related Database Tables

| Table | Role |
|---------|------|
| Users | Customer information |
| Application | Loan application |
| Application History | Workflow history |
| Loans | Loan contract |
| Payments | Payment transactions |
| Loan Status | Loan state |
| Payment Status | Payment state |
| Payment Methods | Payment channel |
| Reason | Loan purpose |
| Cities | Customer location |
| Provinces | Geographic hierarchy |
| Educations | Customer education |

---

# Business Events

Major events generated during the lifecycle include:

- Customer Registered
- Application Submitted
- Documents Verified
- Eligibility Approved
- Credit Reviewed
- Application Approved
- Loan Created
- Payment Received
- Payment Failed
- Payment Overdue
- Loan Settled
- Loan Closed

These events should be recorded for auditing and historical analysis.

---

# Business Metrics by Lifecycle Stage

| Stage | Example KPIs |
|---------|--------------|
| Registration | New Customers |
| Application | Total Applications |
| Approval | Approval Rate |
| Loan Creation | Total Loan Amount |
| Active Loan | Outstanding Balance |
| Payment | Collection Rate |
| Monitoring | Delinquency Rate |
| Settlement | Loan Completion Rate |

---

# Common Operational Risks

Potential issues during the lifecycle include:

- Duplicate applications
- Missing customer information
- Invalid supporting documents
- Delayed approvals
- Incorrect credit assessment
- Late payments
- Payment failures
- Incomplete loan closure
- Inconsistent status updates

---

# AI & RAG Notes

This document enables AI assistants to:

- Explain the end-to-end loan process.
- Identify lifecycle stages for any loan.
- Recommend SQL queries for lifecycle analysis.
- Analyze operational bottlenecks.
- Support workflow documentation.
- Answer business process questions using structured knowledge.

---

# Related Documentation

- Loan ERD
- Approval Process
- Business Rules
- KPI Catalog
- Business Questions
- SQL Cookbook
- Database Schema
- Application Table Documentation
- Loan Table Documentation
- Payment Table Documentation

---

# Summary

The Loan Lifecycle describes the complete journey of a loan, beginning with customer registration and ending with loan closure. It provides a standardized view of operational activities, business events, status transitions, and supporting database entities. This lifecycle serves as the foundation for reporting, dashboard development, Business Intelligence, SQL generation, and Retrieval-Augmented Generation (RAG), ensuring both human analysts and AI systems share a consistent understanding of the loan management process.
