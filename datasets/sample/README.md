# Sample Datasets

> **Project:** Loan Knowledge Base
>
> **Module:** Datasets
>
> **Directory:** `datasets/sample/`
>
> **Version:** 2.0

---

# Overview

This directory contains sample datasets used throughout the **Loan Knowledge Base** project.

The datasets are intended for:

- SQL practice
- Database testing
- BI dashboard development
- Data analysis
- Machine learning experiments
- AI-assisted SQL generation
- Demonstrations and tutorials

The sample data follows the same schema documented in the project and can be safely used for educational and portfolio purposes.

---

# Directory Structure

```text
datasets/

└── sample/
    ├── users.csv
    ├── application.csv
    ├── application_history.csv
    ├── loans.csv
    ├── payments.csv
    ├── provinces.csv
    ├── cities.csv
    ├── educations.csv
    ├── reason.csv
    ├── loan_status.csv
    ├── payment_status.csv
    ├── payment_methods.csv
    └── README.md
```

---

# Available Datasets

| File | Description |
|------|-------------|
| users.csv | Customer master data |
| application.csv | Loan applications |
| application_history.csv | Application status history |
| loans.csv | Approved loan records |
| payments.csv | Loan repayment transactions |
| provinces.csv | Province reference data |
| cities.csv | City reference data |
| educations.csv | Education reference data |
| reason.csv | Loan purpose reference |
| loan_status.csv | Loan status reference |
| payment_status.csv | Payment status reference |
| payment_methods.csv | Payment method reference |

---

# Dataset Relationships

```text
users
   │
   ▼
application
   │
   ▼
loans
   │
   ▼
payments

cities
   │
   ▼
provinces

users
 ├──► cities
 └──► educations

application
 └──► reason

loans
 └──► loan_status

payments
 ├──► payment_status
 └──► payment_methods
```

---

# Suggested Record Counts

These sample sizes are recommended for learning and testing.

| Table | Suggested Rows |
|---------|---------------:|
| provinces | 34 |
| cities | 500+ |
| educations | 8 |
| reason | 10 |
| loan_status | 5 |
| payment_status | 4 |
| payment_methods | 5 |
| users | 1,000 |
| application | 2,000 |
| application_history | 5,000 |
| loans | 1,500 |
| payments | 15,000 |

---

# Recommended CSV Format

- UTF-8 encoding
- Comma-separated values
- Header row included
- ISO 8601 date format (`YYYY-MM-DD`)
- Decimal values use `.` as the separator
- Empty values represented as blank fields or `NULL` (depending on import tool)

Example:

```csv
id,full_name,email,city_id,education_id,created_at
1,John Smith,john@example.com,15,3,2025-01-15
2,Jane Doe,jane@example.com,22,5,2025-01-20
```

---

# Sample Data Characteristics

The sample datasets should include realistic business scenarios such as:

- Multiple loan applications per customer
- Approved and rejected applications
- Active and closed loans
- Partial repayments
- Late payments
- Customers from different provinces
- Various education levels
- Different loan purposes
- Multiple payment methods

---

# Data Quality Guidelines

Sample datasets should satisfy the following requirements:

- No duplicate primary keys.
- All foreign keys reference valid records.
- Required fields are populated.
- Loan amounts are positive.
- Payment amounts are positive.
- Dates follow chronological order.
- Email addresses are unique.
- Customer names contain realistic values.

---

# Import Order

When loading data into the database, use the following sequence to preserve referential integrity.

```text
1. provinces

2. cities

3. educations

4. reason

5. loan_status

6. payment_status

7. payment_methods

8. users

9. application

10. application_history

11. loans

12. payments
```

---

# Example Import (PostgreSQL)

```sql
COPY provinces
FROM '/path/to/provinces.csv'
DELIMITER ','
CSV HEADER;
```

---

# Example Import (MySQL)

```sql
LOAD DATA INFILE 'users.csv'
INTO TABLE users
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

---

# Example Analytical Questions

These datasets can be used to answer questions such as:

- Which province has the largest loan portfolio?
- What is the approval rate?
- Which customers have multiple loans?
- What is the average approved loan amount?
- Which payment method is most frequently used?
- How many active loans exist?
- What is the monthly loan growth?
- Which loan purposes are most common?
- What is the collection rate?
- Which customers have overdue payments?

---

# Suggested Dashboard Metrics

Using these datasets, you can build dashboards showing:

- Total Customers
- Total Applications
- Approved Loans
- Loan Portfolio Value
- Average Loan Size
- Collection Rate
- Delinquency Rate
- Monthly Loan Trend
- Monthly Payment Trend
- Regional Performance

---

# Privacy Notice

These datasets should contain **synthetic or anonymized data only**.

Do **not** include:

- Real customer names
- Government-issued IDs
- Bank account numbers
- Credit card information
- Phone numbers belonging to real individuals
- Personally identifiable information (PII)

Use fictional data for demonstrations, documentation, and portfolio projects.

---

# AI & RAG Notes

The sample datasets complement the repository documentation and are useful for:

- SQL query validation
- BI dashboard testing
- AI-generated SQL verification
- Retrieval-Augmented Generation (RAG) demonstrations
- Prompt engineering
- Machine learning feature engineering
- Data exploration tutorials

Keeping the sample data aligned with the documented schema improves the accuracy of AI-assisted analysis and generated examples.

---

# Related Documentation

- README
- Database Schema
- Relationship Matrix
- Loan ERD
- Table Documentation
- Data Dictionary
- SQL Cookbook
- Business Rules

---

# Summary

The `datasets/sample/` directory contains representative datasets that mirror the Loan Management database schema. These datasets provide a safe environment for learning, SQL practice, analytics, dashboard development, AI-assisted workflows, and portfolio demonstrations while maintaining consistency with the project's documentation and database design.
