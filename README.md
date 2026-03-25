🚀 Enterprise Rebate Management System (ERMS)

Data Model & Workflow Architecture for Institutional Energy Finance

📌 Project Overview

The Enterprise Rebate Management System (ERMS) is a high-integrity DBMS framework designed to synchronize physical University of Hawaii (UH) assets with utility rebate workflows. This system bridges the "Reconciliation Gap" between construction management, energy engineering, and final financial deposit.

Unlike fragmented spreadsheets, ERMS provides a single source of truth for multi-year project lifecycles, ensuring that energy savings and financial incentives are tracked, validated, and audited with 100% accuracy.

🛠️ The Seven Pillars of ERMS

The system is built on a professional architecture to ensure data longevity and institutional memory:

Requirements Traceability (RTM): The authoritative source for every business rule and stage gate.

Normalized Data Dictionary: Strict schema definitions (PKs/FKs) to prevent data duplication.

Relational Mapping (ERD): Complex 1:M and M:M logic linking payments, applications, and buildings.

Application Logic (AL): A state-machine governing 8 stages of the rebate lifecycle.

Integrity Constraints (IC): Technical enforcement of XOR logic (e.g., E-Builder vs. Service Queue).

Role-Based Governance: Tiered access control to protect sensitive financial and audit fields.

Performance Reporting: Standardized metrics for Variance, SLA, and GRF reconciliation.

🏗️ Core Functional Features

1. Workflow-Driven Lifecycle

The system tracks applications through a strict 8-stage progression:

Potential Lead → Commitment Submitted → Commitment Approved → Rebate Submitted → Rebate Approved → Rebate Received → Closed/Deposited → Rejected.

2. Financial & Energy Metric Tracking

ERMS captures four critical dimensions of project success:

Rebate Amount ($): Tracking from initial estimate to final check deposit.

Energy Saved (kWh/Year): Annual efficiency gains.

Lifetime Savings (kWh): Total projected impact over asset life.

Demand Savings (kW): Peak load reduction for grid stability.

3. Advanced Data Governance

XOR ID Constraints: Enforces a project is tracked in either E-Builder/UHM or Service Queue—never both.

Immutability Locks: Financial fields are automatically locked upon reaching terminal stages to prevent retroactive data "cooking."

Audit Trail: Standardized Date_Added, Added_By, Date_Modified, and Modified_By fields on every table.

4. Collaborative Asset Mapping

Junction Table Logic: Handles real-world complexity where one rebate check may cover multiple projects (SOPs), and one project may span multiple physical buildings.

Document Repository: A centralized home for applications, invoices, and proof of deposits.

📂 Repository Structure

/docs/requirements: The RTM (Requirements Traceability Matrix).

/docs/data_model: The Data Dictionary (DD) and ERD.

/docs/governance: Integrity Constraints (IC) and Application Logic (AL).
