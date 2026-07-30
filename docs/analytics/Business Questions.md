
# Business Questions

> **Project:** Loan Knowledge Base
>
> **Module:** Analytics
>
> **Version:** 2.0
>
> **Purpose:** A catalog of business questions that can be answered using the Loan Management Database.

---

# Overview

This document contains business questions commonly asked by management, business analysts, risk analysts, finance teams, and executives.

These questions are organized by analytical domain and are intended to support:

- Business Intelligence
- Dashboard Development
- SQL Practice
- KPI Development
- Exploratory Data Analysis (EDA)
- AI-powered SQL Generation
- Retrieval-Augmented Generation (RAG)

---

# 1. Executive Overview

### Portfolio Performance

- How many customers are registered?
- How many loan applications have been submitted?
- How many active loans currently exist?
- What is the total loan portfolio value?
- What is the total amount collected?
- What is the outstanding balance?
- How many completed loans are there?
- What percentage of loans are currently active?

---

### Growth

- How many new users registered each month?
- How many applications are submitted monthly?
- Is loan demand increasing over time?
- Which month has the highest application volume?
- Which month has the highest loan disbursement?

---

# 2. Customer Analytics

### Customer Demographics

- How many customers are there by gender?
- What is the average customer age?
- What is the age distribution?
- Which education level is most common?
- Which city has the highest number of customers?
- Which province has the most registered users?

---

### Customer Behavior

- How many applications does each customer submit?
- Which customers apply multiple times?
- What is the average loan amount per customer?
- Which customers have the highest borrowing history?
- Which customers have fully repaid all loans?
- Which customers currently have overdue loans?

---

# 3. Loan Application Analytics

### Application Volume

- How many applications are submitted each day?
- Which month receives the most applications?
- What is the daily average number of applications?
- Which loan purpose is the most common?
- Which cities generate the most applications?

---

### Approval Analysis

- What is the approval rate?
- What is the rejection rate?
- Which loan purpose has the highest approval rate?
- Which city has the highest approval rate?
- Which education level has the highest approval rate?
- What is the average processing time from submission to approval?

---

# 4. Loan Portfolio Analytics

### Portfolio Overview

- Total number of loans
- Total loan amount
- Average loan amount
- Median loan amount
- Largest loan issued
- Smallest loan issued

---

### Loan Characteristics

- Average loan period
- Distribution of loan periods
- Average interest rate
- Average credit score
- Average installment amount

---

### Portfolio Segmentation

- Loan amount by province
- Loan amount by city
- Loan amount by education
- Loan amount by loan purpose
- Loan amount by customer age group

---

# 5. Credit Risk Analytics

### Credit Score

- Average credit score
- Credit score distribution
- Credit score by city
- Credit score by education
- Credit score by age group

---

### Default Risk

- Which customers have overdue payments?
- Which loans have the highest risk?
- What is the default rate?
- Which province has the highest default rate?
- Which loan purpose has the highest default rate?
- Which education level has the highest default rate?

---

### Risk Indicators

- Loans with late payments
- Loans with repeated missed payments
- High-value loans with poor payment history
- Customers with multiple rejected applications

---

# 6. Payment Analytics

### Payment Overview

- Total number of payments
- Total payment amount
- Average payment amount
- Total principal collected
- Total interest collected
- Total late fees collected

---

### Payment Performance

- Collection rate
- On-time payment rate
- Late payment rate
- Average payment delay
- Percentage of unpaid installments

---

### Payment Methods

- Most frequently used payment method
- Payment amount by payment method
- Success rate by payment method
- Failed payment rate by payment method

---

### Payment Status

- Number of completed payments
- Number of pending payments
- Number of failed payments
- Number of overdue payments

---

# 7. Geographic Analytics

### Province

- Total customers by province
- Total applications by province
- Total loan value by province
- Average loan size by province
- Default rate by province

---

### City

- Top cities by loan amount
- Top cities by application volume
- Cities with highest approval rate
- Cities with highest repayment rate
- Cities with highest default rate

---

# 8. Financial Analytics

### Revenue

- Total interest earned
- Monthly interest revenue
- Interest revenue by province
- Interest revenue by loan purpose

---

### Outstanding Balance

- Total outstanding balance
- Outstanding balance by city
- Outstanding balance by province
- Outstanding balance by customer

---

### Cash Flow

- Monthly cash inflow
- Monthly loan disbursement
- Monthly repayment
- Monthly interest income

---

# 9. Operational Analytics

### Processing

- Average application processing time
- Applications pending review
- Average approval duration
- Average rejection duration

---

### Workload

- Number of applications processed daily
- Number of applications waiting for approval
- Number of applications by status
- Daily approval volume

---

# 10. Business Rules Validation

- Does every loan originate from exactly one application?
- Does every payment belong to exactly one loan?
- Can one customer have multiple loans?
- Are there orphan records?
- Are foreign keys valid?
- Are loan statuses consistent?

---

# 11. Dashboard Questions

Executive Dashboard

- How is the loan portfolio performing?
- What is the current approval rate?
- What is the repayment rate?
- What is the total outstanding balance?

---

Operations Dashboard

- How many applications are pending?
- How many loans are active?
- Which loans require attention?

---

Risk Dashboard

- Which loans are overdue?
- Which customers are high risk?
- What is the portfolio default rate?

---

Finance Dashboard

- Interest income
- Principal collected
- Outstanding balance
- Monthly revenue

---

# 12. Advanced SQL Practice

Examples of advanced analytical questions:

- Rank customers by total borrowing.
- Identify customers with increasing loan amounts.
- Calculate cumulative repayments.
- Compare monthly loan growth using window functions.
- Identify repeat borrowers.
- Detect customers with abnormal payment behavior.
- Calculate rolling 12-month loan disbursement.
- Identify provinces with above-average loan growth.
- Analyze customer lifetime borrowing value.
- Compare approval rates across education levels.

---

# 13. AI Prompt Examples

Example prompts for AI-powered SQL assistants:

- Generate SQL to calculate monthly approval rates.
- Find the top 10 customers by total loan amount.
- Calculate total outstanding balance by province.
- Show repayment performance by payment method.
- Identify customers with multiple active loans.
- Build a dashboard query for executive reporting.
- Analyze loan trends over the last 12 months.
- Detect high-risk loans using payment history.
- Compare approval rates across cities.
- Generate SQL using window functions to rank borrowers.

---

# Summary

This document provides over **100 business questions** covering:

- Executive Reporting
- Customer Analytics
- Loan Portfolio Analysis
- Credit Risk
- Payment Performance
- Geographic Analysis
- Financial Reporting
- Operational Performance
- Dashboard Design
- Advanced SQL Practice
- AI-powered Analytics

These questions form the analytical foundation of the **Loan Knowledge Base** and are intended to support both human analysts and AI systems in generating meaningful insights from the loan management database.
