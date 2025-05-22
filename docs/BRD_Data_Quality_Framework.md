# Business Requirement Document (BRD)
**Project:** Data Quality Framework POC  
**Date:** [Insert Date]  
**Author:** [Insert Author Name]

---

## 1. Document Purpose
This document defines the business requirements for a Data Quality (DQ) Framework Proof of Concept (POC) to be implemented in data engineering projects. The framework will standardize, automate, and monitor data quality checks, ensuring reliable and trustworthy data for downstream consumption.

---

## 2. Objective
- Establish a robust, reusable, and scalable data quality framework.
- Enable early detection and reporting of data quality issues.
- Provide transparency and traceability for data quality checks and failures.
- Facilitate compliance with data governance and regulatory requirements.

---

## 3. Approach
- Define and store data quality rules in a centralized repository.
- Apply rules to data pipelines and capture results in audit tables.
- Track and report on data quality failures, including detailed failure records.
- Maintain job run history and traceability for all data quality checks.
- Implement audit columns for traceability and compliance.

---

## 4. Key Data Governance Practices
- **Rule Centralization:** All DQ rules are defined and managed centrally.
- **Traceability:** Every DQ check and failure is auditable with job and user metadata.
- **Severity Classification:** DQ issues are classified by severity (Fatal, Warn, Informational) to guide remediation and process flow.
- **Transparency:** All DQ results and failures are logged and accessible for review.
- **Retention & Expiry:** Audit records include expiration dates for data lifecycle management.
- **Compliance:** Framework supports regulatory and internal compliance requirements.

---

## 5. Data Model

### 5.1. audit_dq_rule
| Column Name           | Data Type     | Constraints         | Description                                                                 |
|-----------------------|---------------|---------------------|-----------------------------------------------------------------------------|
| dq_rule_name          | VARCHAR(255)  | UNIQUE, NOT NULL    | Name of the data quality rule                                               |
| object_applied_to     | VARCHAR(255)  | NOT NULL            | Table or object to which the rule applies                                   |
| column_applied_to     | VARCHAR(255)  | NULLABLE            | Column to which the rule applies (if applicable)                            |
| rule_object_type      | VARCHAR(50)   | NOT NULL            | 'column' or 'table'                                                         |
| description           | TEXT          | NOT NULL            | Description of the rule                                                     |
| severity              | VARCHAR(20)   | NOT NULL            | 'Fatal', 'Warn', 'Informational'                                            |
| threshold             | FLOAT         | NULLABLE            | Threshold value for the rule                                                |
| upper_bound           | FLOAT         | NULLABLE            | Upper bound for the rule                                                    |
| lower_bound           | FLOAT         | NULLABLE            | Lower bound for the rule                                                    |
| created_by            | VARCHAR(255)  | NOT NULL            | User who created the rule                                                   |
| created_at            | DATETIME      | NOT NULL            | Timestamp when rule was created                                             |
| updated_by            | VARCHAR(255)  | NOT NULL            | User who last updated the rule                                              |
| updated_at            | DATETIME      | NOT NULL            | Timestamp when rule was last updated                                        |
| last_updated_timestamp| DATETIME      | NOT NULL            | Last update timestamp                                                       |
| job_run_id            | VARCHAR(255)  | NOT NULL            | Job run identifier                                                          |
| job_name              | VARCHAR(255)  | NOT NULL            | Job name                                                                    |

### 5.2. audit_dq_rule_failure
| Column Name           | Data Type     | Constraints         | Description                                                                 |
|-----------------------|---------------|---------------------|-----------------------------------------------------------------------------|
| dq_rule_name          | VARCHAR(255)  | NOT NULL            | Name of the failed rule                                                     |
| dq_rule_failure_count | INT           | NOT NULL            | Number of failures for this rule                                            |
| dq_rule_severity      | VARCHAR(20)   | NOT NULL            | Severity of the rule                                                        |
| object_applied_to     | VARCHAR(255)  | NOT NULL            | Object to which the rule was applied                                        |
| created_by            | VARCHAR(255)  | NOT NULL            | User who created the record                                                 |
| created_at            | DATETIME      | NOT NULL            | Timestamp when record was created                                           |
| updated_by            | VARCHAR(255)  | NOT NULL            | User who last updated the record                                            |
| updated_at            | DATETIME      | NOT NULL            | Timestamp when record was last updated                                      |
| last_updated_timestamp| DATETIME      | NOT NULL            | Last update timestamp                                                       |
| job_run_id            | VARCHAR(255)  | NOT NULL            | Job run identifier                                                          |
| job_name              | VARCHAR(255)  | NOT NULL            | Job name                                                                    |

### 5.3. audit_job_trace
| Column Name           | Data Type     | Constraints         | Description                                                                 |
|-----------------------|---------------|---------------------|-----------------------------------------------------------------------------|
| dq_rule_name          | VARCHAR(255)  | NOT NULL            | Name of the rule being traced                                               |
| source_object         | VARCHAR(255)  | NOT NULL            | Source object                                                               |
| target_object         | VARCHAR(255)  | NOT NULL            | Target object                                                               |
| source_count          | INT           | NULLABLE            | Row count in source                                                         |
| target_count          | INT           | NULLABLE            | Row count in target                                                         |
| difference            | INT           | NULLABLE            | Difference between source and target counts                                 |
| omitted               | INT           | NULLABLE            | Omitted row count                                                           |
| created_by            | VARCHAR(255)  | NOT NULL            | User who created the record                                                 |
| created_at            | DATETIME      | NOT NULL            | Timestamp when record was created                                           |
| updated_by            | VARCHAR(255)  | NOT NULL            | User who last updated the record                                            |
| updated_at            | DATETIME      | NOT NULL            | Timestamp when record was last updated                                      |
| last_updated_timestamp| DATETIME      | NOT NULL            | Last update timestamp                                                       |
| job_run_id            | VARCHAR(255)  | NOT NULL            | Job run identifier                                                          |
| job_name              | VARCHAR(255)  | NOT NULL            | Job name                                                                    |

### 5.4. audit_dq_rule_failure_details
| Column Name           | Data Type     | Constraints         | Description                                                                 |
|-----------------------|---------------|---------------------|-----------------------------------------------------------------------------|
| dq_rule_name          | VARCHAR(255)  | NOT NULL            | Name of the failed rule                                                     |
| source_record         | JSON          | NOT NULL            | Source record in JSON format                                                |
| created_by            | VARCHAR(255)  | NOT NULL            | User who created the record                                                 |
| created_at            | DATETIME      | NOT NULL            | Timestamp when record was created                                           |
| updated_by            | VARCHAR(255)  | NOT NULL            | User who last updated the record                                            |
| updated_at            | DATETIME      | NOT NULL            | Timestamp when record was last updated                                      |
| last_updated_timestamp| DATETIME      | NOT NULL            | Last update timestamp                                                       |
| job_run_id            | VARCHAR(255)  | NOT NULL            | Job run identifier                                                          |
| job_name              | VARCHAR(255)  | NOT NULL            | Job name                                                                    |

### 5.5. audit_job_run_history
| Column Name           | Data Type     | Constraints         | Description                                                                 |
|-----------------------|---------------|---------------------|-----------------------------------------------------------------------------|
| created_by            | VARCHAR(255)  | NOT NULL            | User who created the record                                                 |
| created_at            | DATETIME      | NOT NULL            | Timestamp when record was created                                           |
| updated_by            | VARCHAR(255)  | NOT NULL            | User who last updated the record                                            |
| updated_at            | DATETIME      | NOT NULL            | Timestamp when record was last updated                                      |
| last_updated_timestamp| DATETIME      | NOT NULL            | Last update timestamp                                                       |
| job_run_id            | VARCHAR(255)  | NOT NULL            | Job run identifier                                                          |
| job_name              | VARCHAR(255)  | NOT NULL            | Job name                                                                    |
| start_time            | DATETIME      | NOT NULL            | Job start time                                                              |
| end_time              | DATETIME      | NOT NULL            | Job end time                                                                |
| duration              | INT           | NOT NULL            | Duration in seconds or minutes                                              |
| source_row_count      | INT           | NULLABLE            | Source row count                                                            |
| target_row_count      | INT           | NULLABLE            | Target row count                                                            |
| omitted_row_count     | INT           | NULLABLE            | Omitted row count                                                           | 