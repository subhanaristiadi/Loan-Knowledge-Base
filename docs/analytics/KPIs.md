# Key Performance Indicators (KPIs)

> **Project:** Loan Knowledge Base
>
> **Module:** Analytics
>
> **Version:** 2.0
>
> **Purpose:** Standard KPI definitions for monitoring loan portfolio performance, operational efficiency, credit risk, collections, and financial performance.

---

# Overview

This document defines the Key Performance Indicators (KPIs) used throughout the Loan Management System.

Each KPI includes:

- Business Purpose
- Formula
- SQL Implementation Guidance
- Interpretation
- Recommended Dashboard Visualization

These KPIs are intended to ensure consistent reporting across dashboards, SQL queries, and AI-generated analyses.

---

# KPI Categories

| Category | Description |
|----------|-------------|
| Customer | Customer acquisition and behavior |
| Application | Loan application performance |
| Loan Portfolio | Portfolio size and growth |
| Credit Risk | Loan quality and repayment risk |
| Collection | Payment performance |
| Financial | Revenue and outstanding balance |
| Operational | Processing efficiency |

---

# 1. Customer KPIs

## Total Registered Customers

### Business Purpose

Measures the total number of registered customers.

### Formula

```text
COUNT(DISTINCT user_id)
```

### Interpretation

Higher values indicate customer growth.

### Visualization

- KPI Card

---

## New Customers

Measures newly registered customers during a selected period.

### Formula

```text
Customers Registered During Period
```

Visualization

- Line Chart
- Monthly Trend

---

## Active Borrowers

Customers who currently have at least one active loan.

### Formula

```text
Customers With Active Loan
```

Visualization

- KPI Card

---

## Repeat Borrower Rate

Percentage of customers submitting more than one application.

### Formula

```text
Customers With Multiple Applications
────────────────────────────────────
Total Customers
```

Visualization

- KPI Card

---

# 2. Loan Application KPIs

## Total Applications

Total submitted loan applications.

### Formula

```text
COUNT(application_id)
```

Visualization

- KPI Card

---

## Approval Rate

Percentage of approved applications.

### Formula

```text
Approved Applications
─────────────────────
Total Applications
```

Target

Higher is generally better.

Visualization

- Gauge
- KPI Card

---

## Rejection Rate

### Formula

```text
Rejected Applications
─────────────────────
Total Applications
```

Visualization

- Gauge

---

## Average Processing Time

Average duration between application submission and approval.

### Formula

```text
Approval Date
─────────────
Submission Date
```

Unit

Days

Visualization

- KPI Card

---

# 3. Loan Portfolio KPIs

## Total Loan Amount

Total value of all approved loans.

### Formula

```text
SUM(loan_amount)
```

Visualization

- KPI Card

---

## Average Loan Amount

### Formula

```text
AVG(loan_amount)
```

Visualization

- KPI Card

---

## Active Loans

Current active loans.

### Formula

```text
COUNT(active loans)
```

Visualization

- KPI Card

---

## Closed Loans

Loans that have been fully repaid.

Visualization

- KPI Card

---

## Loan Growth Rate

Monthly growth of loan portfolio.

### Formula

```text
(Current Month Loans
-
Previous Month Loans)

────────────────────

Previous Month Loans
```

Visualization

- Line Chart

---

# 4. Credit Risk KPIs

## Average Credit Score

Average customer credit score.

### Formula

```text
AVG(credit_score)
```

Visualization

- KPI Card

---

## Default Rate

Percentage of loans classified as default.

### Formula

```text
Default Loans
─────────────
Total Loans
```

Visualization

- Gauge

---

## Delinquency Rate

Percentage of overdue loans.

### Formula

```text
Overdue Loans
─────────────
Total Active Loans
```

Visualization

- KPI Card

---

## High Risk Portfolio

Loan value classified as high risk.

Visualization

- Bar Chart

---

# 5. Collection KPIs

## Collection Rate

Measures repayment success.

### Formula

```text
Collected Amount
────────────────
Due Amount
```

Visualization

- KPI Card

---

## Payment Success Rate

### Formula

```text
Successful Payments
───────────────────
Total Payments
```

Visualization

- Gauge

---

## Late Payment Rate

### Formula

```text
Late Payments
─────────────
Total Payments
```

Visualization

- KPI Card

---

## Average Days Late

Average delay before payment.

Unit

Days

Visualization

- KPI Card

---

# 6. Financial KPIs

## Total Principal Collected

### Formula

```text
SUM(principal_amount)
```

Visualization

- KPI Card

---

## Total Interest Collected

### Formula

```text
SUM(interest_amount)
```

Visualization

- KPI Card

---

## Outstanding Balance

### Formula

```text
SUM(outstanding_balance)
```

Visualization

- KPI Card

---

## Total Revenue

Revenue generated from:

- Interest
- Late Fees
- Other Charges

Visualization

- KPI Card

---

## Monthly Revenue

Visualization

- Line Chart

---

# 7. Geographic KPIs

Province Level

- Total Customers
- Total Loans
- Approval Rate
- Default Rate
- Outstanding Balance

Visualization

- Filled Map
- Bar Chart

---

City Level

- Applications
- Loans
- Collection Rate
- Average Loan

Visualization

- Ranked Bar Chart

---

# 8. Operational KPIs

## Pending Applications

Applications awaiting review.

Visualization

- KPI Card

---

## Daily Processing Volume

Applications processed each day.

Visualization

- Line Chart

---

## Average Approval Time

Average time required to approve a loan.

Visualization

- KPI Card

---

## Application Backlog

Applications not yet processed.

Visualization

- KPI Card

---

# Executive Dashboard KPIs

The executive dashboard should display:

| KPI | Priority |
|------|----------|
| Total Customers | High |
| Total Applications | High |
| Approval Rate | High |
| Active Loans | High |
| Outstanding Balance | High |
| Collection Rate | High |
| Default Rate | High |
| Monthly Revenue | High |

---

# Operations Dashboard KPIs

Recommended KPIs:

- Pending Applications
- Daily Applications
- Loans Approved Today
- Average Processing Time
- Active Loans
- Payment Status

---

# Risk Dashboard KPIs

Recommended KPIs:

- Credit Score Distribution
- Default Rate
- Delinquency Rate
- High Risk Loans
- Overdue Loans
- Outstanding Balance

---

# Finance Dashboard KPIs

Recommended KPIs:

- Revenue
- Interest Income
- Principal Collected
- Outstanding Balance
- Collection Rate
- Monthly Cash Flow

---

# KPI Relationships

```text
Applications
        │
        ▼
Approval Rate
        │
        ▼
Loans
        │
        ▼
Collection Rate
        │
        ▼
Outstanding Balance
        │
        ▼
Revenue
```

---

# Recommended Refresh Frequency

| KPI | Refresh |
|------|----------|
| Applications | Daily |
| Customers | Daily |
| Loan Portfolio | Daily |
| Payments | Daily |
| Collection Rate | Daily |
| Revenue | Daily |
| Dashboard | Daily |
| Executive Report | Weekly / Monthly |

---

# Common KPI Mistakes

Avoid the following:

- Mixing approved and rejected applications.
- Calculating collection rate using incorrect denominators.
- Ignoring partial payments.
- Comparing KPIs across different time periods.
- Using inconsistent loan status definitions.
- Ignoring inactive or closed loans.
- Double-counting customers with multiple applications.

---

# Related Documentation

- Business Questions
- EDA Guide
- Dashboard Ideas
- SQL Cookbook
- Business Rules
- Loan ERD

---

# Summary

This KPI catalog provides standardized business metrics for the Loan Management System. By using consistent definitions, formulas, and reporting practices, analysts, BI developers, and AI assistants can generate reliable insights and comparable dashboards across different reporting periods.
