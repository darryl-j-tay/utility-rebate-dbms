# Business Rules and Governance: ERMS

## Project Scope and Intent
The Energy Rebate Management System (ERMS) functions as a governance tool for state and utility audits. These rules ensure data integrity and audit readiness for Hawaii Energy and GRF funding requirements.

---

## Business Rules Matrix

| Ref ID | Rule Name | Technical Logic | Enforcement | Rationale |
|:---|:---|:---|:---|:---|
| **BR-01** | **Record Identity** | PK; Update Restricted | Database (PK) | Ensures audit traceability across multi-year cycles. |
| **BR-02** | **Project Linkage** | Foreign Key; NOT NULL | Database (FK) | Prevents orphaned records; enables campus-wide reporting. |
| **BR-03** | **Utility Sync** | Immutable after submission | Database Trigger | Prevents reconciliation errors post-utility filing. |
| **BR-04** | **Baseline Integrity**| NOT NULL @ Approval | Workflow Trigger | Prevents unauthorized modification of baseline estimates. |
| **BR-05** | **Zero-Rebate Check** | Conditional Default (0.00)| Database Trigger | Prevents double-counting if third parties secure funds. |
| **BR-06** | **System XOR** | XOR Constraint | Check Constraint | Prevents duplicate funding across E-Builder and SuperQuote. |

---

## Enforcement Methodology

### 1. Database Layer Constraints
Integrity is maintained via PK/FK relationships and Check Constraints. Rule [BR-06] specifically prevents records from existing simultaneously in construction (E-Builder) and procurement (SuperQuote) systems.

### 2. Audit Traceability
Every record modification is tracked via `DATE_ADDED` and `ADDED_BY_ID`, ensuring accountability for all system state changes.
