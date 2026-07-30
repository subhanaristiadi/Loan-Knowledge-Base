# Prompt Library

> **Project:** Loan Knowledge Base
>
> **Module:** Prompts
>
> **Version:** 2.0
>
> **Purpose:** A comprehensive library of reusable prompts for SQL generation, data analysis, business intelligence, documentation, dashboard development, and Retrieval-Augmented Generation (RAG).

---

# Overview

This Prompt Library contains reusable prompt templates for working with the Loan Management System.

The prompts are designed for:

- Database exploration
- SQL generation
- Business Intelligence
- Data Analytics
- Dashboard design
- Documentation
- Data Quality Assessment
- Executive reporting
- AI-powered assistance
- RAG applications

These prompts are compatible with modern Large Language Models (LLMs), including:

- GPT
- Claude
- Gemini
- Qwen
- Llama
- Mistral

---

# Prompt Categories

| Category | Purpose |
|----------|---------|
| Database | Understand the database structure |
| SQL | Generate and optimize SQL |
| Analytics | Perform business analysis |
| Dashboard | Design BI dashboards |
| KPI | Calculate business metrics |
| Documentation | Explain system documentation |
| Data Quality | Validate datasets |
| Business | Answer business questions |
| AI | RAG and AI assistant prompts |

---

# 1. Database Exploration

## Prompt

```text
Explain the structure of the Loan Management database.

Include:

- Main entities
- Master tables
- Transaction tables
- Relationships
- Business workflow
- Primary keys
- Foreign keys

Explain the system as if teaching a junior data analyst.
```

---

# 2. Database Relationship Analysis

```text
Explain how the tables relate to one another.

For every relationship include:

- Parent table
- Child table
- Relationship type
- Foreign key
- Business meaning

Provide an ERD-style explanation.
```

---

# 3. SQL Generation

```text
Generate an SQL query that answers the business question.

Requirements:

- Explain reasoning.
- Identify required tables.
- Explain joins.
- Use readable aliases.
- Optimize performance.
- Explain expected output.
```

---

# 4. SQL Optimization

```text
Review this SQL query.

Tasks:

- Find syntax issues.
- Find logic issues.
- Improve readability.
- Improve performance.
- Explain every optimization.
- Rewrite the SQL.
```

---

# 5. SQL Learning Assistant

```text
Teach me how to solve this SQL problem.

Do not only provide the final query.

Explain:

- Business problem
- Required tables
- Join logic
- Aggregations
- Window functions
- Final SQL
- Common mistakes
```

---

# 6. KPI Calculation

```text
Calculate the requested KPI.

Include:

- Definition
- Formula
- SQL query
- Validation method
- Business interpretation
- Dashboard recommendation
```

---

# 7. Dashboard Designer

```text
Design a dashboard for the following business objective.

Include:

- Dashboard name
- Audience
- KPIs
- Charts
- Filters
- Drill-down flow
- Layout
- Business questions answered
```

---

# 8. Executive Summary

```text
Summarize business performance for executives.

Include:

- Growth
- Portfolio
- Collections
- Revenue
- Credit Risk
- Geography
- Recommendations

Use concise executive language.
```

---

# 9. Data Quality Assessment

```text
Perform a Data Quality Assessment.

Evaluate:

- Missing values
- Duplicate records
- Invalid foreign keys
- Invalid dates
- Outliers
- Business rule violations

Rank issues by severity and recommend corrective actions.
```

---

# 10. Exploratory Data Analysis

```text
Perform an Exploratory Data Analysis.

Include:

- Data overview
- Missing values
- Distribution analysis
- Correlation analysis
- Time trends
- Geographic trends
- Customer analysis
- Loan analysis
- Payment analysis
- Key findings
```

---

# 11. Business Insight Discovery

```text
Identify the most important business insights.

For every insight include:

- Finding
- Supporting metrics
- Business impact
- Recommended visualization
- Recommended action
```

---

# 12. Root Cause Analysis

```text
Investigate the business problem.

Provide:

- Problem statement
- Possible causes
- Supporting evidence
- SQL recommendations
- Dashboard recommendations
- Business recommendations
```

---

# 13. Customer Analytics

```text
Analyze customer behavior.

Identify:

- High-value customers
- Repeat borrowers
- Geographic patterns
- Income segments
- Payment behavior

Recommend business strategies.
```

---

# 14. Portfolio Analysis

```text
Analyze the current loan portfolio.

Include:

- Portfolio growth
- Loan distribution
- Outstanding balance
- Active loans
- Closed loans
- Loan purposes
- Regional distribution
```

---

# 15. Collection Performance

```text
Analyze loan repayments.

Evaluate:

- Collection rate
- Late payments
- Payment trends
- Overdue balances
- Collection efficiency

Recommend operational improvements.
```

---

# 16. Credit Risk Analysis

```text
Act as a Credit Risk Analyst.

Evaluate:

- Default rate
- Delinquency
- High-risk customers
- Regional risk
- Loan purpose risk
- Credit score distribution

Provide recommendations.
```

---

# 17. Documentation Assistant

```text
Answer the user's question using the Loan Knowledge Base.

Always:

- Use documented facts.
- Reference relevant documentation.
- Explain technical concepts clearly.
- Recommend related documents.
- Avoid unsupported assumptions.
```

---

# 18. Business Rule Validator

```text
Review the scenario against the documented Business Rules.

Identify:

- Rules satisfied
- Rules violated
- Potential risks
- Recommended actions

Reference the applicable business rules.
```

---

# 19. RAG Assistant

```text
You are connected to the Loan Knowledge Base.

Before answering:

1. Retrieve relevant documents.
2. Prioritize retrieved knowledge.
3. Cite document names when appropriate.
4. Clearly separate facts from assumptions.
5. Recommend related documentation.

Do not invent missing information.
```

---

# 20. AI SQL Tutor

```text
Act as an SQL mentor.

Help me solve SQL problems step by step.

Explain:

- Why each table is needed.
- Why each JOIN is used.
- Why each aggregation is required.
- Performance considerations.
- Alternative SQL approaches.

Teach instead of only giving answers.
```

---

# 21. Dashboard Storytelling

```text
Explain dashboard results as a business story.

Include:

- What happened?
- Why it happened?
- Key drivers
- Risks
- Opportunities
- Recommended next actions

Use language suitable for executives.
```

---

# 22. Interview Preparation

```text
Pretend you are interviewing me for a Data Analyst position.

Ask questions related to:

- SQL
- Database Design
- Loan Analytics
- KPIs
- Dashboard Development
- Business Intelligence

Evaluate my answers and provide feedback.
```

---

# 23. Dataset Documentation

```text
Generate technical documentation for the uploaded dataset.

Include:

- Table overview
- Column definitions
- Data types
- Primary keys
- Foreign keys
- Business meaning
- Relationships
- Data quality considerations
```

---

# 24. AI Assistant System Prompt

```text
You are an expert Business Intelligence Analyst specializing in loan management systems.

You have access to the complete Loan Knowledge Base.

Your responsibilities include:

- Explaining business processes.
- Generating SQL.
- Designing dashboards.
- Calculating KPIs.
- Validating business rules.
- Interpreting analytical results.
- Answering documentation questions.

Always:

- Retrieve relevant documentation first.
- Explain your reasoning.
- Use standardized terminology.
- Distinguish facts from assumptions.
- Recommend related documentation.
```

---

# Best Practices

When using these prompts:

- Start with the business objective.
- Reference documented business rules.
- Explain reasoning before conclusions.
- Prefer evidence over assumptions.
- Use clear and consistent terminology.
- Generate readable and maintainable SQL.
- Recommend next analytical steps where appropriate.

---

# Prompt Workflow

```text
Business Question

↓

Understand Context

↓

Retrieve Documentation

↓

Identify Tables

↓

Generate SQL

↓

Validate Results

↓

Interpret Findings

↓

Recommend Business Actions
```

---

# Related Documentation

- Analysis Prompt
- Business Rules
- Loan Lifecycle
- Business Glossary
- KPI Catalog
- SQL Cookbook
- Dashboard Ideas
- Executive Dashboard
- Database Schema

---

# Summary

This Prompt Library provides a comprehensive collection of reusable prompts for working with the Loan Management System. Covering database exploration, SQL generation, Business Intelligence, dashboard design, documentation, data quality, customer analytics, and RAG-based knowledge retrieval, it serves as a practical toolkit for analysts, developers, and AI assistants to produce consistent, explainable, and high-quality analytical outputs.
