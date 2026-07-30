# Executive Dashboard

> **Project:** Loan Knowledge Base
>
> **Module:** Dashboards
>
> **Version:** 2.0
>
> **Audience:** Executive Management, Directors, Business Leaders
>
> **Purpose:** Provide a high-level view of the overall health, growth, profitability, and risk of the loan portfolio through a single executive dashboard.

---

# Overview

The Executive Dashboard is designed to answer one primary question:

> **"How is the business performing today?"**

Unlike operational dashboards, this dashboard focuses on strategic KPIs and long-term business trends.

The dashboard should allow executives to:

- Monitor business growth
- Track portfolio health
- Assess credit risk
- Measure collection performance
- Evaluate financial performance
- Compare regional performance
- Identify emerging trends

---

# Dashboard Objectives

The Executive Dashboard should enable decision makers to:

- Understand the overall loan portfolio.
- Monitor customer growth.
- Track application and approval trends.
- Measure repayment performance.
- Monitor financial performance.
- Identify high-risk portfolios.
- Compare regional performance.
- Support strategic planning.

---

# Executive Questions

The dashboard should answer the following business questions.

## Business Growth

- Is the customer base growing?
- Are loan applications increasing?
- How much has the portfolio grown this month?
- Which month recorded the highest growth?

---

## Portfolio Performance

- How many active loans exist?
- What is the total outstanding balance?
- What is the average loan amount?
- Which loan purpose dominates the portfolio?

---

## Credit Risk

- What is the current default rate?
- Is delinquency increasing?
- Which regions have the highest credit risk?
- What percentage of loans are overdue?

---

## Collection Performance

- What is the collection rate?
- How much principal has been collected?
- How much interest has been collected?
- Which payment methods perform best?

---

## Financial Performance

- Monthly revenue
- Interest income
- Outstanding balance
- Monthly cash flow
- Portfolio growth

---

# Dashboard Layout

```text
+----------------------------------------------------------------------------------+
|                          LOAN EXECUTIVE DASHBOARD                                |
+----------------------------------------------------------------------------------+

 KPI Cards
------------------------------------------------------------------------------------

 Total Customers
 Total Applications
 Active Loans
 Approval Rate
 Collection Rate
 Default Rate
 Outstanding Balance
 Monthly Revenue

------------------------------------------------------------------------------------

 Monthly Loan Trend

------------------------------------------------------------------------------------

 Loan Portfolio by Status

 Payment Status

------------------------------------------------------------------------------------

 Revenue Trend

 Outstanding Balance Trend

------------------------------------------------------------------------------------

 Top Provinces

 Top Cities

------------------------------------------------------------------------------------

 Loan Purpose

 Education Distribution

------------------------------------------------------------------------------------

 Credit Score Distribution

 Default Rate by Province

------------------------------------------------------------------------------------

 Executive Summary
```

---

# KPI Cards

The first section should display the most important business metrics.

| KPI | Description |
|------|-------------|
| Total Customers | Registered customers |
| Total Applications | Submitted applications |
| Active Loans | Current active loans |
| Approval Rate | Approved applications / total applications |
| Collection Rate | Collected amount / due amount |
| Default Rate | Defaulted loans / total loans |
| Outstanding Balance | Remaining balance |
| Monthly Revenue | Revenue for current month |

---

# Section 1 — Portfolio Growth

## Purpose

Measure portfolio expansion over time.

### Recommended Charts

- Monthly Loan Growth (Line Chart)
- Monthly Applications (Column Chart)
- Monthly Customers (Line Chart)

### KPIs

- New Customers
- New Loans
- Portfolio Growth %
- Loan Volume

---

# Section 2 — Portfolio Composition

## Purpose

Understand the composition of the loan portfolio.

### Charts

- Loan Status (Donut Chart)
- Loan Purpose (Bar Chart)
- Loan Period Distribution (Histogram)
- Loan Amount Distribution (Histogram)

---

# Section 3 — Revenue

## Purpose

Track financial performance.

### Charts

- Monthly Revenue
- Interest Income
- Principal Collected
- Cash Flow Trend

### KPIs

- Interest Revenue
- Principal Collected
- Outstanding Balance
- Average Revenue per Loan

---

# Section 4 — Collections

## Purpose

Monitor repayment performance.

### Charts

- Collection Rate Trend
- Payment Status Breakdown
- Payment Method Distribution
- Monthly Collections

### KPIs

- Collection Rate
- Total Paid
- Overdue Loans
- Late Payment Rate

---

# Section 5 — Credit Risk

## Purpose

Monitor portfolio quality.

### Charts

- Credit Score Distribution
- Default Rate Trend
- Delinquency Trend
- High Risk Portfolio

### KPIs

- Average Credit Score
- Default Rate
- Delinquency Rate
- High Risk Loans

---

# Section 6 — Geographic Performance

## Purpose

Compare regional business performance.

### Charts

- Province Performance
- City Performance
- Geographic Map

### KPIs

- Customers by Province
- Loans by Province
- Collection Rate by Province
- Default Rate by Province

---

# Section 7 — Customer Analytics

## Purpose

Understand borrower characteristics.

### Charts

- Gender Distribution
- Age Distribution
- Education Distribution
- Repeat Borrowers

### KPIs

- Average Age
- Average Income
- Repeat Borrower Rate
- Average Loan per Customer

---

# Global Filters

Every visualization should respond to global filters.

Recommended filters:

- Date Range
- Province
- City
- Loan Status
- Payment Status
- Loan Purpose
- Education
- Payment Method

---

# Recommended SQL Views

The following aggregated views are recommended for performance.

| View | Purpose |
|------|----------|
| vw_customer_summary | Customer KPIs |
| vw_application_summary | Application KPIs |
| vw_loan_summary | Loan Portfolio |
| vw_payment_summary | Collections |
| vw_revenue_summary | Financial KPIs |
| vw_geographic_summary | Province & City KPIs |
| vw_risk_summary | Credit Risk |

---

# Drill-Down Flow

The dashboard should support hierarchical navigation.

```text
Executive Dashboard

        │

        ▼

Province

        │

        ▼

City

        │

        ▼

Customer

        │

        ▼

Application

        │

        ▼

Loan

        │

        ▼

Payment
```

---

# Refresh Strategy

| Data | Refresh Frequency |
|------|-------------------|
| Customers | Daily |
| Applications | Daily |
| Loans | Daily |
| Payments | Daily |
| Revenue | Daily |
| Dashboard Cache | Hourly (optional) |

---

# Executive Summary Panel

The bottom section should automatically summarize key insights.

Example:

> - Portfolio grew by **8.3%** compared to last month.
> - Approval Rate increased from **78.5%** to **81.2%**.
> - Collection Rate remains above target at **97.1%**.
> - Province A contributed **24%** of total loan volume.
> - Default Rate decreased by **0.8 percentage points**.
> - Monthly revenue reached the highest level in the past 12 months.

This section can later be generated automatically using an LLM.

---

# Dashboard Design Principles

- Display the most important KPIs first.
- Show trends instead of isolated values.
- Use consistent metric definitions.
- Prioritize readability over decorative elements.
- Highlight exceptions and risks.
- Support drill-down analysis.
- Keep the dashboard responsive for desktop and tablet devices.

---

# AI & RAG Notes

This document enables AI assistants to:

- Recommend executive-level KPIs.
- Generate SQL queries for dashboard widgets.
- Explain chart selection.
- Produce dashboard specifications.
- Generate executive summaries automatically.
- Assist BI developers in implementing dashboards.

---

# Related Documentation

- KPI Catalog
- Dashboard Ideas
- Business Questions
- EDA Guide
- SQL Cookbook
- Loan ERD
- Business Rules

---

# Summary

The Executive Dashboard provides a strategic overview of the Loan Management System by combining portfolio growth, financial performance, credit risk, collections, customer analytics, and geographic performance into a single decision-support interface. It is designed for senior management and serves as the primary dashboard for monitoring business health, identifying risks, and supporting data-driven decision making.
