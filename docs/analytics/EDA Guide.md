
# Exploratory Data Analysis (EDA) Guide

> **Project:** Loan Knowledge Base
>
> **Module:** Analytics
>
> **Version:** 2.0
>
> **Purpose:** A practical guide for performing Exploratory Data Analysis (EDA) on the Loan Management Database.

---

# Overview

Exploratory Data Analysis (EDA) is the process of understanding a dataset before building dashboards, reports, machine learning models, or performing statistical analysis.

For the Loan Management Database, EDA aims to answer four fundamental questions:

1. What data do we have?
2. Is the data reliable?
3. What business patterns exist?
4. What insights can support business decisions?

---

# EDA Workflow

```text
Understand Dataset
        │
        ▼
Data Quality Assessment
        │
        ▼
Univariate Analysis
        │
        ▼
Bivariate Analysis
        │
        ▼
Multivariate Analysis
        │
        ▼
Business Insights
        │
        ▼
Dashboard Design
```

---

# Step 1 — Understand the Database

Before analyzing data, understand:

- Business objective
- Database schema
- Primary keys
- Foreign keys
- Table relationships
- Data granularity

Questions:

- What does each table represent?
- What is the transaction table?
- What are the master tables?
- Which table stores customer information?
- Which table stores financial transactions?

---

# Step 2 — Data Quality Assessment

## Missing Values

Check:

- NULL values
- Blank values
- Invalid values

Example SQL

```sql
SELECT
COUNT(*) AS total_rows,
COUNT(user_id) AS valid_user_id
FROM Users;
```

---

## Duplicate Records

Check duplicate primary keys.

Example:

```sql
SELECT
user_id,
COUNT(*)
FROM Users
GROUP BY user_id
HAVING COUNT(*) > 1;
```

---

## Invalid Foreign Keys

Example:

```sql
Applications.user_id

↓

Users.user_id
```

Check whether every foreign key exists.

---

## Date Validation

Look for:

- Future dates
- Impossible dates
- Missing timestamps

Examples:

- Loan before registration
- Payment before loan creation

---

## Numeric Validation

Identify:

- Negative income
- Negative expenses
- Negative loan amount
- Negative payment

---

# Step 3 — Univariate Analysis

Analyze one variable at a time.

---

## Customer Variables

Examples:

- Gender distribution
- Age distribution
- Education level
- Province
- City

Charts:

- Bar Chart
- Pie Chart
- Histogram

---

## Loan Variables

Analyze:

- Loan amount
- Loan period
- Interest rate
- Credit score

Charts:

- Histogram
- Boxplot
- Density Plot

---

## Payment Variables

Analyze:

- Paid amount
- Due amount
- Interest amount
- Late fee

Charts:

- Histogram
- Boxplot

---

# Step 4 — Bivariate Analysis

Study relationships between two variables.

Examples:

- Loan amount vs Credit Score
- Loan amount vs Income
- Age vs Loan Amount
- Interest Rate vs Loan Period
- Province vs Default Rate

Recommended charts:

- Scatter Plot
- Boxplot
- Grouped Bar Chart

---

# Step 5 — Multivariate Analysis

Analyze three or more variables simultaneously.

Examples:

- Province × Loan Purpose × Approval Rate
- Education × Credit Score × Loan Amount
- Age × Income × Default Rate
- City × Loan Amount × Payment Status

Recommended:

- Heatmap
- Bubble Chart
- Pivot Table

---

# Step 6 — Time Series Analysis

Analyze trends over time.

Examples:

- Monthly applications
- Monthly loan issuance
- Monthly repayments
- Monthly interest income

Recommended charts:

- Line Chart
- Area Chart

Questions:

- Is demand increasing?
- Are repayments seasonal?
- Which month has the highest approvals?

---

# Step 7 — Customer Analysis

Metrics:

- Number of customers
- Repeat borrowers
- Average income
- Average expenses
- Average loan amount

Segmentation:

- Gender
- Education
- Province
- City
- Age Group

---

# Step 8 — Loan Analysis

Metrics:

- Total loans
- Active loans
- Closed loans
- Rejected loans
- Average loan amount
- Largest loan
- Smallest loan

Recommended visualizations:

- Histogram
- Boxplot
- Treemap

---

# Step 9 — Credit Risk Analysis

Analyze:

- Credit score distribution
- Approval rate
- Default rate
- Late payment rate

Questions:

- Which segment has the highest default rate?
- Which city has the lowest repayment performance?
- Are larger loans more risky?

---

# Step 10 — Payment Analysis

Metrics:

- Collection rate
- Total repayments
- Outstanding balance
- Late fees
- Payment success rate

Visualizations:

- Stacked Bar Chart
- Waterfall Chart
- Trend Line

---

# Step 11 — Geographic Analysis

Province Analysis

- Customers
- Applications
- Loans
- Revenue
- Default Rate

City Analysis

- Loan Volume
- Average Loan
- Collection Rate
- Approval Rate

Maps (optional)

- Choropleth Map
- Bubble Map

---

# Step 12 — Correlation Analysis

Analyze relationships between numeric variables.

Variables:

- Income
- Expense
- Loan Amount
- Credit Score
- Interest Rate
- Loan Period
- Paid Amount

Recommended:

Correlation Matrix

Interpretation

| Correlation | Meaning |
|------------|---------|
| 0.90 – 1.00 | Very Strong Positive |
| 0.70 – 0.89 | Strong Positive |
| 0.40 – 0.69 | Moderate Positive |
| 0.20 – 0.39 | Weak Positive |
| -0.20 – 0.20 | Little or No Correlation |
| -0.40 – -0.69 | Moderate Negative |
| -0.70 – -1.00 | Strong Negative |

---

# Step 13 — Outlier Detection

Possible methods:

- Boxplot
- IQR
- Z-score
- Percentile

Typical variables:

- Loan Amount
- Income
- Interest Amount
- Paid Amount

Questions:

- Are there unusually large loans?
- Are there abnormal payment amounts?

---

# Step 14 — KPI Validation

Validate business metrics.

Examples:

Approval Rate

```text
Approved Applications
──────────────────────
Total Applications
```

Collection Rate

```text
Collected Amount
────────────────
Due Amount
```

Default Rate

```text
Defaulted Loans
───────────────
Total Loans
```

---

# Step 15 — Dashboard Planning

Executive Dashboard

KPIs

- Total Loans
- Outstanding Balance
- Collection Rate
- Approval Rate
- Default Rate

Operations Dashboard

KPIs

- Pending Applications
- Loans Awaiting Approval
- Overdue Payments

Risk Dashboard

KPIs

- Credit Score
- High Risk Customers
- Default Trend

Finance Dashboard

KPIs

- Revenue
- Interest Income
- Principal Collected
- Outstanding Balance

---

# Recommended Visualizations

| Business Question | Recommended Chart |
|-------------------|-------------------|
| Monthly Applications | Line Chart |
| Loan Distribution | Histogram |
| Approval Rate | KPI Card |
| Loan Status | Donut Chart |
| Province Comparison | Bar Chart |
| Payment Status | Stacked Bar |
| Correlation | Heatmap |
| Outstanding Balance | Treemap |
| Customer Segmentation | Boxplot |
| Revenue Trend | Area Chart |

---

# Common EDA Mistakes

- Skipping data quality checks.
- Ignoring duplicate records.
- Not validating foreign keys.
- Comparing metrics with different time periods.
- Using averages without checking outliers.
- Ignoring business context.
- Treating lookup tables as transactional data.

---

# Deliverables

A complete EDA should produce:

- Data Quality Report
- Descriptive Statistics
- Business Insights
- KPI Summary
- Dashboard Requirements
- SQL Queries
- Recommended Visualizations
- Executive Summary

---

# EDA Checklist

- Database understood
- Relationships validated
- Missing values checked
- Duplicate records checked
- Foreign keys validated
- Numeric fields reviewed
- Outliers detected
- Time trends analyzed
- Customer segments analyzed
- Loan portfolio analyzed
- Payment performance analyzed
- Credit risk analyzed
- KPIs validated
- Dashboard requirements documented

---

# Related Documentation

- Database Overview
- Database Schema
- Loan ERD
- Business Questions
- KPI Catalog
- SQL Cookbook
- Dashboard Ideas
- Business Rules

---

# Summary

This guide provides a structured EDA framework for the Loan Management Database, covering data quality, descriptive analysis, customer behavior, loan performance, payment analysis, credit risk, geographic insights, and dashboard planning. Following these steps ensures that analyses are accurate, business-focused, and suitable for Business Intelligence, reporting, machine learning, and AI-powered SQL generation.
