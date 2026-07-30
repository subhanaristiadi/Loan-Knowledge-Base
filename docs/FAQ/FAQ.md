# Frequently Asked Questions (FAQ)

> **Project:** Loan Knowledge Base
>
> **Module:** Documentation
>
> **Document:** Frequently Asked Questions (FAQ)
>
> **Version:** 2.0

---

# Overview

This document answers the most common questions about the **Loan Knowledge Base** repository.

It is intended for:

- Developers
- Data Analysts
- Business Analysts
- Data Engineers
- BI Developers
- Database Administrators
- AI Engineers
- New Contributors

---

# General Questions

## 1. What is the purpose of this repository?

This repository documents a complete **Loan Management relational database**.

It provides:

- Database documentation
- Entity Relationship Diagram (ERD)
- Business rules
- SQL examples
- Analytics documentation
- Dashboard references
- Prompt templates
- AI-friendly knowledge for Retrieval-Augmented Generation (RAG)

---

## 2. Who should use this repository?

This repository is useful for:

- SQL learners
- Data Analysts
- Backend Developers
- BI Developers
- Database Engineers
- AI Engineers
- Technical Writers
- Students building portfolio projects

---

## 3. Which database does this project use?

The examples are written primarily for **PostgreSQL**.

Most SQL examples can also be adapted to:

- MySQL
- SQL Server
- Oracle
- MariaDB
- SQLite

with only minor syntax changes.

---

## 4. Is this a production database?

No.

This repository is intended for:

- Learning
- Demonstration
- Portfolio projects
- Documentation
- AI experiments
- SQL practice

---

## Database Questions

## 5. How many tables are included?

The reference schema contains **12 normalized tables**.

### Master Tables

- provinces
- cities
- educations
- reason
- loan_status
- payment_status
- payment_methods

### Transaction Tables

- users
- application
- application_history
- loans
- payments

---

## 6. What normalization level is used?

The schema follows **Third Normal Form (3NF)**.

Goals include:

- Eliminating redundancy
- Maintaining referential integrity
- Improving maintainability
- Supporting scalable reporting

---

## 7. Where can I find the database schema?

See:

```
docs/schema/Database Schema.md
```

---

## 8. Where is the ERD located?

See:

```
docs/erd/Loan ERD.md
```

---

## 9. How are tables related?

Relationships are documented in:

- Database Schema
- Relationship Matrix
- ERD
- Individual Table Documentation

---

## SQL Questions

## 10. Where should beginners start?

Recommended learning order:

1. Basic SQL Queries
2. Intermediate SQL Queries
3. Advanced SQL Queries
4. Common Table Expressions (CTE)
5. Window Functions

---

## 11. Why are there multiple SQL documents?

Each document targets a different skill level.

| Document | Purpose |
|-----------|---------|
| Basic Queries | SQL fundamentals |
| Intermediate Queries | Business reporting |
| Advanced Queries | Analytical SQL |
| CTE | Multi-step queries |
| Window Functions | Advanced analytics |

---

## 12. Are all queries production-ready?

The examples demonstrate best practices and are suitable for learning and prototyping.

Before using them in production:

- Review execution plans.
- Verify indexes.
- Test with realistic datasets.
- Adjust for your database platform.

---

## 13. Which SQL dialect is used?

Primary dialect:

```
PostgreSQL
```

---

## 14. Can I use these queries in MySQL?

Yes.

Some functions require adjustment.

Examples include:

- `DATE_TRUNC()`
- Interval syntax
- Type casting
- Window function support (depending on version)

---

## Documentation Questions

## 15. Why is there so much documentation?

Comprehensive documentation helps:

- Developers understand the schema.
- Analysts write correct SQL.
- BI teams build dashboards.
- AI assistants retrieve accurate information.
- New contributors onboard quickly.

---

## 16. Why does every table have its own documentation?

Individual table documentation provides:

- Business meaning
- Technical metadata
- Relationships
- Constraints
- SQL examples
- Reporting usage
- Governance information

---

## 17. What is the Data Dictionary?

The Data Dictionary explains:

- Tables
- Columns
- Data types
- Business definitions
- Constraints
- Example values

---

## Analytics Questions

## 18. Which KPIs are included?

Examples include:

- Total Customers
- Approval Rate
- Loan Portfolio Value
- Average Loan Amount
- Collection Rate
- Active Loans
- Delinquency Rate
- Customer Growth
- Payment Performance

---

## 19. Does the repository include dashboard ideas?

Yes.

See:

```
docs/dashboards/
```

Topics include:

- Executive Dashboard
- Portfolio Dashboard
- Customer Dashboard
- Payment Dashboard
- Regional Dashboard

---

## 20. Can I use this project for BI tools?

Yes.

It is suitable for:

- Power BI
- Tableau
- Looker Studio
- Apache Superset
- Metabase
- Grafana

---

## AI Questions

## 21. Is this repository optimized for AI?

Yes.

The documentation is designed for:

- AI assistants
- RAG systems
- Semantic search
- SQL generation
- Documentation generation
- Knowledge retrieval

---

## 22. What is Retrieval-Augmented Generation (RAG)?

RAG combines an LLM with external knowledge.

Instead of relying only on model memory, the AI retrieves relevant documentation before generating a response.

This improves:

- Accuracy
- Consistency
- Explainability
- Domain-specific reasoning

---

## 23. Which AI models can use this repository?

Any modern LLM, including:

- GPT
- Claude
- Gemini
- Qwen
- Llama
- DeepSeek
- Mistral
- Command R

---

## 24. Why are prompt templates included?

Prompt templates help users:

- Generate SQL
- Produce documentation
- Design dashboards
- Analyze business problems
- Build reusable AI workflows

---

## Development Questions

## 25. How should I contribute?

Follow the contribution guidelines in:

```
CONTRIBUTING.md
```

General principles:

- Follow naming conventions.
- Maintain documentation quality.
- Keep SQL readable.
- Update version history.
- Submit clear pull requests.

---

## 26. How should I document a new table?

Use:

```
templates/Table Template.md
```

---

## 27. How should I document a business rule?

Use:

```
templates/Business Rule Template.md
```

---

## 28. How should I write SQL for this repository?

Follow:

```
templates/SQL Template.md
```

---

## 29. How should I create AI prompts?

Use:

```
templates/Prompt Template.md
```

---

## Repository Questions

## 30. What is the recommended reading order?

```text
README

↓

Database Overview

↓

Architecture

↓

Database Schema

↓

Relationship Matrix

↓

ERD

↓

Table Documentation

↓

Business Rules

↓

Basic SQL

↓

Intermediate SQL

↓

Advanced SQL

↓

CTE

↓

Window Functions

↓

Analytics

↓

Dashboards

↓

Prompt Library
```

---

## 31. Can I use this repository as a portfolio project?

Yes.

It demonstrates:

- Database design
- SQL skills
- Documentation
- Business analysis
- Business Intelligence
- AI-ready knowledge engineering

---

## 32. Is sample data included?

The repository is documentation-focused.

You may add sample datasets under:

```
datasets/
```

---

## 33. Can I extend the schema?

Yes.

Recommended additions include:

- Branches
- Employees
- Guarantors
- Credit Scores
- Documents
- Notifications
- Audit Logs
- Loan Products

---

## 34. Is versioning supported?

Yes.

Documentation should be versioned whenever:

- Schemas change.
- Business rules change.
- SQL examples are updated.
- New modules are introduced.

---

## Troubleshooting

## 35. My SQL query returns no results.

Check:

- JOIN conditions
- WHERE filters
- Foreign key relationships
- Sample data availability
- Date ranges

---

## 36. My JOIN returns duplicate rows.

Possible causes:

- One-to-many relationships
- Missing join conditions
- Incorrect aggregation
- Duplicate source data

Review the ERD and relationship documentation.

---

## 37. My dashboard numbers do not match.

Verify:

- Filters
- Date ranges
- Aggregation logic
- KPI definitions
- Business rules
- Source tables

---

## 38. AI generated incorrect SQL.

Ensure the AI has access to:

- Database Schema
- Relationship Matrix
- Data Dictionary
- Business Rules
- Table Documentation

Providing schema context significantly improves SQL accuracy.

---

## Best Practices

To get the most value from this repository:

- Read the schema before writing SQL.
- Use documented relationships.
- Avoid undocumented assumptions.
- Follow naming conventions.
- Keep documentation synchronized with schema changes.
- Use templates for consistency.
- Validate SQL against realistic datasets.

---

## Related Documentation

- README
- Database Overview
- Architecture
- Database Schema
- Relationship Matrix
- ERD
- SQL Cookbook
- Data Dictionary
- Business Rules
- Prompt Library

---

# Summary

This FAQ provides answers to the most common questions about the Loan Knowledge Base repository, covering database design, SQL usage, documentation standards, analytics, AI integration, contribution guidelines, and troubleshooting. It serves as a quick reference to help users navigate the repository, understand its structure, and apply its resources effectively for learning, development, business intelligence, and AI-assisted workflows.
