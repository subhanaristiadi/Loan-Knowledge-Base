# SQL Prompt

> **Project:** Loan Knowledge Base
>
> **Module:** Prompts
>
> **Version:** 2.0
>
> **Purpose:** A collection of reusable prompts for generating, optimizing, explaining, validating, and analyzing SQL queries using the Loan Management Knowledge Base.

---

# Overview

This document provides standardized prompts for SQL-related tasks within the Loan Management System.

These prompts help AI assistants:

- Generate SQL queries
- Explain SQL logic
- Optimize SQL performance
- Debug SQL errors
- Recommend analytical approaches
- Produce Business Intelligence reports

The prompts assume that the AI has access to:

- Database Schema
- Table Documentation
- Business Rules
- Business Glossary
- Loan Lifecycle
- KPI Catalog
- SQL Cookbook

---

# General SQL Assistant Prompt

```text
You are a Senior SQL Developer and Business Intelligence Consultant.

You have access to the complete Loan Management Knowledge Base.

Before generating SQL:

1. Understand the business question.
2. Identify the required tables.
3. Explain the table relationships.
4. Explain the required JOINs.
5. Generate clean and optimized SQL.
6. Explain each calculation.
7. Describe the expected output.
8. Recommend useful visualizations when appropriate.

Avoid making assumptions when documentation is available.
```

---

# SQL Generation Prompt

```text
Generate an SQL query that answers the following business question.

Requirements:

- Explain your reasoning.
- Identify all required tables.
- Explain each JOIN.
- Use descriptive aliases.
- Follow ANSI SQL where possible.
- Format the SQL for readability.
- Explain the expected result.
```

---

# SQL Explanation Prompt

```text
Explain the following SQL query step by step.

Include:

- Business objective
- Tables involved
- JOIN logic
- WHERE conditions
- GROUP BY
- Aggregations
- Window functions
- ORDER BY
- Final output

Explain in language suitable for junior data analysts.
```

---

# SQL Debugging Prompt

```text
Review the SQL query.

Identify:

- Syntax errors
- Logical errors
- Incorrect JOINs
- Missing filters
- Incorrect aggregations
- Performance issues

Rewrite the SQL and explain every improvement.
```

---

# SQL Optimization Prompt

```text
Optimize the SQL query.

Review:

- Readability
- JOIN efficiency
- Filtering strategy
- Aggregation efficiency
- Window functions
- Index usage
- Query structure

Return:

- Optimized SQL
- Performance recommendations
- Explanation of changes
```

---

# SQL Learning Prompt

```text
Teach me how to solve this SQL problem.

Instead of immediately giving the answer:

- Explain the business problem.
- Identify the required tables.
- Explain the relationships.
- Explain each JOIN.
- Explain the aggregation strategy.
- Build the SQL step by step.
- Discuss alternative approaches.
- Highlight common mistakes.
```

---

# SQL KPI Prompt

```text
Generate SQL for calculating the requested KPI.

For each KPI include:

- Business definition
- Mathematical formula
- Required tables
- SQL query
- Validation method
- Interpretation
```

---

# SQL Dashboard Prompt

```text
Generate SQL queries for an Executive Dashboard.

Provide SQL for:

- KPI cards
- Monthly trends
- Portfolio analysis
- Collection performance
- Credit risk
- Geographic analysis
- Customer analysis

Explain what each query returns.
```

---

# SQL Time-Series Prompt

```text
Generate SQL for time-based analysis.

Support:

- Daily
- Weekly
- Monthly
- Quarterly
- Yearly

Include trend calculations where appropriate.
```

---

# SQL Customer Analytics Prompt

```text
Generate SQL to analyze customers.

Include:

- Customer growth
- Repeat borrowers
- Customer lifetime value (if available)
- Average loan amount
- Geographic distribution
- Education distribution
```

---

# SQL Portfolio Analysis Prompt

```text
Generate SQL for portfolio analysis.

Include:

- Active loans
- Closed loans
- Outstanding balance
- Average loan amount
- Loan purpose
- Loan status distribution
```

---

# SQL Collection Prompt

```text
Generate SQL for collection analysis.

Include:

- Collection rate
- Total collected
- Outstanding balance
- Overdue payments
- Payment methods
- Late payment trends
```

---

# SQL Credit Risk Prompt

```text
Generate SQL for credit risk analysis.

Include:

- Default rate
- Delinquency rate
- High-risk customers
- Regional risk
- Credit score distribution
- Loan purpose risk
```

---

# SQL Data Quality Prompt

```text
Generate SQL queries to validate data quality.

Check:

- Missing values
- Duplicate records
- Invalid foreign keys
- Invalid dates
- Negative amounts
- Business rule violations

Explain each validation query.
```

---

# SQL Window Function Prompt

```text
Generate SQL using window functions where appropriate.

Examples:

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LAG()
- LEAD()
- SUM() OVER()
- AVG() OVER()

Explain why each window function is used.
```

---

# SQL Interview Prompt

```text
Act as a Senior SQL Interviewer.

Present SQL problems related to the Loan Management database.

After I answer:

- Evaluate correctness.
- Explain mistakes.
- Show an optimized solution.
- Recommend best practices.
```

---

# SQL Documentation Prompt

```text
Generate documentation for the SQL query.

Include:

- Business objective
- Tables used
- Input parameters
- Output columns
- Calculation logic
- Assumptions
- Limitations
- Performance considerations
```

---

# SQL Review Checklist Prompt

```text
Review the SQL query using the following checklist.

Check:

- Business logic
- Correct tables
- Correct JOINs
- Readable aliases
- Filtering logic
- GROUP BY correctness
- Window function usage
- Performance
- Maintainability

Provide an overall assessment and recommendations.
```

---

# AI SQL Tutor Prompt

```text
Act as an SQL mentor.

Guide me through solving SQL problems.

Always:

- Ask clarifying questions if needed.
- Explain your reasoning.
- Build the query incrementally.
- Explain every JOIN.
- Explain every aggregation.
- Discuss optimization opportunities.
- Encourage understanding rather than memorization.
```

---

# RAG SQL System Prompt

```text
You are an AI assistant connected to the Loan Knowledge Base.

When answering SQL questions:

1. Retrieve relevant documentation first.
2. Use documented table definitions.
3. Use documented relationships.
4. Follow documented business rules.
5. Generate readable SQL.
6. Explain your reasoning.
7. Distinguish documented facts from assumptions.
8. Recommend related documentation when appropriate.

If required information is unavailable, explicitly state the limitation instead of inventing schema details.
```

---

# SQL Best Practices

When generating SQL:

- Start with the business objective.
- Use explicit JOIN syntax.
- Avoid `SELECT *` in production queries.
- Use meaningful table aliases.
- Format SQL consistently.
- Minimize unnecessary subqueries.
- Prefer ANSI SQL for portability.
- Document assumptions.
- Validate results against business rules.

---

# SQL Workflow

```text
Business Question

↓

Understand Requirements

↓

Retrieve Documentation (RAG)

↓

Identify Required Tables

↓

Define JOIN Strategy

↓

Write SQL

↓

Validate Results

↓

Explain Findings

↓

Recommend Business Actions
```

---

# Related Documentation

- SQL Cookbook
- Database Schema
- Table Documentation
- Business Rules
- KPI Catalog
- Business Glossary
- Analysis Prompt
- Prompt Library

---

# Summary

This SQL Prompt library provides reusable templates for SQL generation, explanation, optimization, debugging, validation, and analytics within the Loan Management System. By combining documented schema definitions, business rules, and Retrieval-Augmented Generation (RAG), these prompts help produce SQL that is accurate, maintainable, explainable, and aligned with real business requirements.
