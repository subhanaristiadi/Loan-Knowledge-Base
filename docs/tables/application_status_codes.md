# Application Status Codes

This document explains the application status codes used in the dataset.

---

## Table Information

| Property | Value |
|----------|-------|
| Table Name | `application_status_codes` |
| Primary Key | `applications_codes` |
| Description | Lookup table containing the application lifecycle status codes and their business meaning. |

---

## Table Columns

| Column | Data Type | Description |
|--------|-----------|-------------|
| `applications_codes` | INTEGER | Numeric application status code |
| `status_name` | STRING | Human-readable status name |
| `stage_order` | INTEGER | Sequence order in the application lifecycle |
| `outcome_category` | STRING | High-level application outcome category |
| `is_terminal` | STRING | Indicates whether the status is a terminal stage |
| `description` | STRING | Business description of the status |

---

## Status Codes

| Code | Status Name | Stage | Outcome Category | Terminal | Description |
|-----:|-------------|------:|------------------|----------|-------------|
| 200 | Application Submitted | 1 | In Progress | No | First stage for every application; appears in every application journey. |
| 205 | Verification / Document Check | 2 | In Progress | No | Applicant passed initial screening and entered document verification. |
| 206 | Rejected - Initial Screening | 2 | Rejected | Yes | Application rejected immediately after submission. |
| 220 | Underwriting / Credit Review Started | 3 | In Progress | No | Application entered credit assessment. |
| 221 | Rejected - Verification Stage | 3 | Rejected | Yes | Application rejected during document verification. |
| 222 | Underwriting In Progress | 4 | In Progress | No | Deeper underwriting and risk assessment. |
| 223 | Rejected - Underwriting Stage | 4 | Rejected | Yes | Application rejected during underwriting. |
| 224 | Final Risk Review | 5 | In Progress | No | Final review before approval decision. |
| 225 | Rejected - Underwriting Stage 2 | 5 | Rejected | Yes | Application rejected during final underwriting review. |
| 250 | Approved | 6 | Approved | No | Application approved but not yet disbursed. |
| 251 | Rejected - Final Review | 6 | Rejected | Yes | Application rejected during final risk review. |
| 280 | Disbursed | 7 | Disbursed | Yes | Loan successfully disbursed. |
| 281 | Approved but Not Disbursed (Cancelled) | 7 | Approved-NotDisbursed | Yes | Loan approved but cancelled before disbursement. |
| 282 | Approved but Not Disbursed (Expired/Other) | 7 | Approved-NotDisbursed | Yes | Loan approved but never disbursed due to expiration or other reasons. |

---

## Business Rules

- Every application starts with status **200 (Application Submitted)**.
- Applications normally progress according to `stage_order`.
- Any status where `is_terminal = Yes` represents the end of the application journey.
- Applications may end as:
  - **Rejected**
  - **Approved but Not Disbursed**
  - **Disbursed**

---

## Typical Application Flow

```text
200 → 205 → 220 → 222 → 224 → 250 → 280
```

Possible rejection paths:

```text
200 → 206

200 → 205 → 221

200 → 205 → 220 → 223

200 → 205 → 220 → 222 → 225

200 → 205 → 220 → 222 → 224 → 251
```

Approved but not disbursed:

```text
200 → 205 → 220 → 222 → 224 → 250 → 281

200 → 205 → 220 → 222 → 224 → 250 → 282
```

---

## Analytical Use Cases

This lookup table is commonly joined with:

- `application_history`
- `application`

Typical analyses include:

- Application funnel conversion
- Drop-off analysis by stage
- Approval rate
- Rejection reason by stage
- Average processing time between stages
- Stage-to-stage conversion analysis
