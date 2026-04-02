# Master Data Dictionary: ERMS

## Nullability and Requirement Definitions
* **NOT NULL**: System-enforced requirement at the database level.
* **NULL**: Optional field.
* **COND**: Required based on workflow stage or business logic.

---

## Governance Framework
This dictionary is governed by established Business Rules to ensure data integrity through the rebate lifecycle. Fields marked with a **Reference** are subject to specific logic and immutability constraints defined in the [Business Rules](./Business_Rules.md).

---

## 1. REBATE_APPLICATION
| Column | Data Type | Key | Null | Description | Reference |
|:---|:---|:---:|:---:|:---|:---|
| **SOP_NUM** | VARCHAR(15) | PK | NOT NULL | Unique 10-character identifier (YYMM-N) | [[BR-01]](./Business_Rules.md#br-01) |
| **PROJECT_ID** | INT | FK | NULL | Parent Project Group association | [[BR-02]](./Business_Rules.md#br-02) |
| **STAGE_ID** | INT | FK | NOT NULL | Current workflow stage ID | RTM-P1.2 |
| **HE_OPPORTUNITY_NUM**| VARCHAR(20) | UI | COND | Hawaii Energy utility tracking ID | [[BR-03]](./Business_Rules.md#br-03) |
| **TYPE_ID** | INT | FK | COND | Rebate measure classification | RTM-P1.4 |
| **FUNDING_ID** | INT | FK | NULL | Financial source (e.g., GRF, ARRA) | RTM-P1.5 |
| **PROJECT_MANAGER_ID**| INT | FK | NULL | Assigned Project Manager (Personnel) | FK → PERSONNEL |
| **EST_TOTAL_COST** | DECIMAL(18,2) | — | COND | Baseline project cost for audit | [[BR-04]](./Business_Rules.md#br-04) |
| **EST_KWH_SAVINGS** | DECIMAL(18,2) | — | COND | Estimated annual energy savings | [[BR-04]](./Business_Rules.md#br-04) |
| **ACTUAL_REBATE_AMT**| DECIMAL(18,2) | — | NULL | Verified rebate value received | [[BR-05]](./Business_Rules.md#br-05) |
| **PO_NUM** | VARCHAR(50) | — | COND | SuperQuote Purchase Order Number | [[BR-06]](./Business_Rules.md#br-06) |
| **DATE_ADDED** | DATETIME | — | NOT NULL | System-generated creation timestamp | Audit |
| **ADDED_BY_ID** | INT | FK | NOT NULL | User ID of record creator | FK → PERSONNEL |

---

## 2. PROJECT_GROUP
| Column | Data Type | Key | Null | Description | Reference |
|:---|:---|:---:|:---:|:---|:---|
| **PROJECT_ID** | INT | PK | NOT NULL | Internal unique identifier | System |
| **PROJECT_NAME** | VARCHAR(255) | UI | NOT NULL | Unique project designation | RTM-P3.2 |
| **GROUP_STATUS_ID** | INT | FK | NOT NULL | High-level project status | FK → STATUS |
| **E_BUILDER_NUM** | VARCHAR(50) | — | NULL | External Construction ID (E-Builder) | [[BR-06]](./Business_Rules.md#br-06) |
| **UHM_NUM** | VARCHAR(50) | — | NULL | University of Hawaii ID | [[BR-06]](./Business_Rules.md#br-06) |
| **SQ_NUM** | VARCHAR(50) | — | NULL | External Procurement ID (SuperQuote) | [[BR-06]](./Business_Rules.md#br-06) |

---

## 3. JUNCTION ENTITIES

### SOP_BUILDING_JUNCTION
| Column | Key | Description |
|:---|:---:|:---|
| **SOP_NUM** | PK, FK | Foreign Key to REBATE_APPLICATION |
| **BUILDING_ID** | PK, FK | Foreign Key to BUILDING |

### SOP_DOCUMENT_JUNCTION
| Column | Key | Description |
|:---|:---:|:---|
| **SOP_NUM** | PK, FK | Foreign Key to REBATE_APPLICATION |
| **DOCUMENT_ID** | PK, FK | Foreign Key to DOCUMENT |
