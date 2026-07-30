# Prompt Template

> **Project:** Loan Knowledge Base
>
> **Module:** AI Prompt Library
>
> **Document:** Prompt Template
>
> **Version:** 2.0

---

# Overview

This template provides a standardized structure for creating high-quality prompts for Large Language Models (LLMs).

The template is designed to produce consistent, accurate, and reusable prompts for tasks such as:

- SQL Generation
- Data Analysis
- Business Intelligence
- Documentation
- Code Generation
- API Development
- Dashboard Design
- Database Exploration
- Knowledge Retrieval (RAG)

This format is vendor-neutral and can be adapted for GPT, Claude, Gemini, Llama, Mistral, Qwen, DeepSeek, and other LLMs.

---

# Prompt Metadata

| Field | Description |
|---------|-------------|
| Prompt ID | Unique identifier |
| Prompt Name | Short descriptive title |
| Category | SQL, Documentation, Analytics, API, etc. |
| Difficulty | Basic / Intermediate / Advanced |
| Target Model | Any LLM |
| Version | Prompt version |
| Author | Prompt creator |
| Last Updated | Last modification date |

---

# Prompt Template

## Prompt Title

```
Customer Loan Analysis
```

---

## Objective

Clearly describe the goal of the prompt.

Example:

> Generate an SQL query that analyzes customer loan performance by province.

---

## Role

Assign a role to the AI.

Example:

```
You are a Senior Data Analyst specializing in financial services and relational databases.
```

---

## Context

Provide the necessary business context.

Example:

```
The database belongs to a Loan Management System.

Tables include:

- users
- application
- loans
- payments
- cities
- provinces
- loan_status
- payment_status

The schema follows Third Normal Form (3NF).
```

---

## Input

Describe what information the AI will receive.

Example

```
Customer requests

Business questions

Database schema

Table documentation

ERD

Business rules
```

---

## Instructions

Clearly define the expected behavior.

Example

```
Generate valid PostgreSQL SQL.

Use explicit JOIN syntax.

Avoid SELECT *.

Use descriptive aliases.

Return readable SQL.

Include comments when appropriate.
```

---

## Constraints

Specify limitations.

Example

- Use ANSI SQL whenever possible.
- Do not invent columns.
- Use only documented tables.
- Do not assume missing relationships.
- Preserve referential integrity.
- Prefer readable queries over overly compact syntax.

---

## Expected Output

Describe the desired response format.

Example

````text
Explanation

SQL Query

Query Breakdown

Performance Tips
