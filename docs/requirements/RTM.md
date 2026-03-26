# Requirements Traceability Matrix (RTM)
**Project:** Enterprise Rebate Management System (ERMS)  
**Phase:** 1 (Core Data Foundation)  
**Status:** Authoritative Baseline

| ID | Phase / Topic | Requirement / Question | Status | Decision / Rationale | Technical Artifact / DD Fields |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **P1.1** | Core Data | What is the primary goal? | **Complete** | **Workflow → Reporting.** Design must manage transitions first to ensure data quality for financial/kWh reporting. | N/A (Conceptual) |
| **P1.2** | Core Data | List all possible application stages. | **Complete** | 8 stages defined (POTENTIAL LEAD to B00H00). Stage logic controlled by Application Logic (AL). | `STAGE_LOOKUP`; `STAGE_ID` |
| **P1.3** | Core Data | User roles and security needs? | **Complete** | Defined Tiered access (Controller to Viewer). Audit fields (P4.1) provide foundation for accountability. | `PERSONNEL_LOOKUP`; `USER_TYPE_LOOKUP` |
| **P1.4** | Core Data | Critical reports/metrics needed? | **Complete** | Support for classified reporting via Category, Type, and FICM code lookups. | `REBATE_CATEGORY_LOOKUP`; `REBATE_TYPE_LOOKUP`; `BUILDING_TYPE_LOOKUP` |
| **P1.5** | Core Data | Financial funding source tracking? | **Complete** | Create `FUNDING_LOOKUP`. FK is nullable initially, enforced at Commitment Approval (Q-Sub). | `FUNDING_LOOKUP`; `Funding_ID` |
| **P2.5** | Integration | Universally unique identifier (PK)? | **Complete** | SOP # is PK. HE Opportunity # is a Unique Index/External ID. | `SOP_NUM` (PK); `HE_OPPORTUNITY_NUM` (UI) |
| **P2.6** | Integration | Personnel/Vendor structure? | **Complete** | Use robust lookups for PM, CM, Consultants, and Contractors. | `PERSONNEL_LOOKUP`; `USER_TYPE_LOOKUP` |
| **P2.7** | Integration | Actual vs. Estimated timing? | **Complete** | Separate, distinct data sets tied to different stages. Versioning history not required for Phase 1. | Traced via P5.1 and P5.2 |
| **P2.8** | Integration | Key personnel roles to link? | **Complete** | Implement six FKs on `REBATE_APPLICATION` (PM, CM, Consultant, Contractor, HE Rep, Funding). | `Project_Manager_ID`; `Consultant_ID`; etc. |
| **P3.1** | Assets | Linking granular SOPs to one project? | **Complete** | Create `PROJECT_GROUP`. PK uses "-G" suffix. Includes separate `GROUP_STATUS_LOOKUP`. | `PROJECT_GROUP`; `GROUP_STATUS_LOOKUP` |
| **P3.2** | Assets | Project Name location? | **Complete** | Lives ONLY in `PROJECT_GROUP` (Normalization). Constraint: NOT NULL and unique. | `Project_Name` |
| **P3.3** | Assets | Mutually exclusive External IDs? | **Complete** | Enforce **XOR rule**: Must have (E-Builder + UHM) OR (SQ #), but never both. | `E_Builder_Num`; `UHM_Num`; `SQ_Num` |
| **P3.4** | Assets | Financial Timing (PO #)? | **Complete** | Nullable field. Immutability Lock and Mandatory check applied at REBATE RECEIVED (AL-6.5). | `PO_Num` |
| **P3.6** | Assets | Structural Granularity (Buildings)? | **Complete** | Implemented via M:M Junction Table. Links SOP measures to physical building assets. | `BUILDING`; `SOP_BUILDING_JUNCTION` |
| **P4.1** | Governance | Standard audit columns? | **Complete** | Implement 4-column audit system (Date_Added, Added_By, Date_Mod, Modified_By) on all primary tables. | `Date_Added`; `Added_By_ID`; etc. |
| **P4.2** | Governance | Terminal Stage Lock? | **Complete** | Apply Application Lock on terminal records. Only Internal Admin (T1/T2) can override (AL-9.1). | `FINAL_CLOSEOUT_STATUS` |
| **P5.1** | Financials | Estimation Fields? | **Complete** | Track 4 fields (Cost, kWh, Lifetime kWh, Rebate). Mandatory at COMMITMENT APPROVED. | `ESTIMATED_4_Fields` |
| **P5.2** | Financials | Actual Fields? | **Complete** | Track 4 fields. Mandatory at REBATE RECEIVED. If 'Secured by Others', Rebate = 0.00. | `ACTUAL_4_Fields` |
| **P5.3** | Financials | P5.1 Immutability? | **Complete** | Lock Estimated fields upon transition to REBATE SUBMITTED (AL-4.3). | Traced via P5.1 |
| **P6.1** | Documents | Document Management/Evidence? | **Complete** | External storage via URL/Path. Use `DOCUMENT_TYPE_LOOKUP` and Junction table for M:M links. | `DOCUMENT`; `SOP_DOCUMENT_JUNCTION` |
| **P7.1** | Workflow | Milestone Date tracking? | **Complete** | Implement 4 DATE fields. Each is Conditional NOT NULL upon reaching specific workflow stages. | `COMMITMENT_SUBMITTED_DATE`; etc. |
| **P8.1** | Payments | Check/Payment Granularity (M:M)? | **Complete** | One check can cover many SOPs. Requires Payment entity and Junction table. | `PAYMENT`; `PAYMENT_SOP_JUNCTION` |
| **P9.1** | GRF | GRF Funding Milestones? | **Complete** | Track Encumbered and Withdrawn dates specifically when `Funding_ID` = 'GRF'. | `GRF_FUNDS_ENCUMBERED_DATE`; etc. |
| **P9.2** | GRF | Repayment Commitment Audit? | **Complete** | Implement audit fields for repayment memo process. Simple governance (nullable). | `RECOLLECTION_MEMO_DATE` |
| **P9.3** | Rejection | Rejection Date Tracking? | **Complete** | Dedicated date stamp applied automatically upon transition to B00H00 stage. | `REJECTION_DATE` |
