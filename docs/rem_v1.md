# Requirements Evaluation Matrix (REM v1) — Lab 4

## Context
- **Project:** AMS Project Management Platform
- **Slice:** Intake & Discovery
- **Variant:** 9 (Privacy & Data Retention)

---

### REQ-001 — Restrict Stakeholder Data Collection
- **Stakeholder (Requisitante):** Privacy Officer
- **Description:** The system's intake form must actively restrict the capture of stakeholder contact details, allowing only the input of a 'Corporate Email Address' and 'System Role', while rejecting formatting that resembles phone numbers or physical addresses.
- **Objective (why/result):** To strictly enforce GDPR data minimization principles by preventing the ingestion of unnecessary personal identifiable information (PII) during the discovery phase.
- **Type:** FR
- **Priority:** H
- **Objective + CSF linkage:** OBJ-1 / CSF-1
- **Preconditions:** The user is authenticated and has initiated a new AMS transition intake session.
- **Postconditions:** A stakeholder profile is created containing only strictly necessary corporate identifiers, with no extraneous personal data stored in the database.
- **Acceptance criteria (draft):**
  - The UI does not render fields for personal phone numbers, home addresses, or alternative personal emails.
  - If a user inputs a string matching a standard phone number regex into any text field, the form displays a validation error and blocks submission.
- **Validation method:** Automated UI Testing / Regex Validation Check
- **Variant impact:** Yes

### REQ-002 — Automated 30-Day Purge for Abandoned Intake Sessions
- **Stakeholder (Requisitante):** Legal Representative
- **Description:** An automated background mechanism must permanently erase all structured data and uploaded evidence associated with an intake session that has registered no user activity for exactly 30 consecutive days.
- **Objective (why/result):** To eliminate legal exposure and comply with strict data retention policies by ensuring obsolete discovery data is not hoarded indefinitely.
- **Type:** NFR
- **Priority:** H
- **Objective + CSF linkage:** OBJ-2 / CSF-2
- **Acceptance criteria (draft):**
  - A scheduled job evaluates the `last_modified` timestamp of all draft intake sessions daily at 00:00 UTC.
  - Sessions exceeding the 30-day threshold are hard-deleted from the primary database and cloud storage, leaving zero recoverable artifacts.
- **Validation method:** Integration Test (Time-travel simulation)
- **Variant impact:** Yes

### REQ-003 — Immutable Audit Trail for Sensitive Evidence Access
- **Stakeholder (Requisitante):** Privacy Officer
- **Description:** The system must automatically generate a read-only audit log entry whenever a user views, downloads, or modifies any uploaded discovery evidence flagged as containing personal or sensitive organizational data.
- **Objective (why/result):** To provide a transparent and verifiable access history, ensuring accountability and supporting GDPR compliance audits.
- **Type:** FR
- **Priority:** H
- **Objective + CSF linkage:** OBJ-2 / CSF-2
- **Preconditions:** A user attempts to open an evidence file attached to an active intake session.
- **Postconditions:** The user gains access to the file, and a discrete log entry is successfully appended to the internal audit ledger.
- **Acceptance criteria (draft):**
  - The audit log captures the user's ID, the exact UTC timestamp, the file UUID, and the action type (VIEW/DOWNLOAD).
  - The `AuditLogs` database table structure prevents `UPDATE` and `DELETE` queries, even from system administrators.
- **Validation method:** Code Review / Automated API Test
- **Variant impact:** Yes

### REQ-004 — Intake Decision Engine Validation
- **Stakeholder (Requisitante):** Transition Lead
- **Description:** The system must process all submitted intake fields and uploaded evidence metadata against configured business rules to automatically output a transition status of either "Ready to Proceed" or "Need More Data".
- **Objective (why/result):** To eliminate manual bottlenecks in the transition pipeline by providing an immediate, objective assessment of discovery completeness.
- **Type:** FR
- **Priority:** H
- **Objective + CSF linkage:** OBJ-3 / CSF-3
- **Preconditions:** The user submits the completed intake package for formal evaluation.
- **Postconditions:** The intake session state is locked for editing, and the final decision outcome is recorded and displayed on the transition dashboard.
- **Acceptance criteria (draft):**
  - If all mandatory fields are populated and evidence files pass integrity checks, the status updates to "Ready to Proceed".
  - If any critical evidence is missing or corrupted, the status defaults to "Need More Data".
- **Validation method:** Unit Testing (Decision Logic)
- **Variant impact:** No

### REQ-005 — Discovery Deficit Reporting
- **Stakeholder (Requisitante):** AMS Engineer
- **Description:** When an intake session evaluates to "Need More Data", the system shall compile and display a diagnostic report explicitly listing which data points or evidence files are missing or invalid.
- **Objective (why/result):** To provide the client with clear, actionable feedback so they can rapidly rectify missing requirements without requiring back-and-forth emails.
- **Type:** FR
- **Priority:** M
- **Objective + CSF linkage:** OBJ-3 / CSF-3
- **Acceptance criteria (draft):**
  - The report bullet-points the exact names of the missing fields (e.g., "Missing SLA Matrix").
  - The report flags evidence that failed validation with a clear reason (e.g., "Uploaded Architecture Diagram is illegible").
- **Validation method:** Demonstration
- **Variant impact:** No

### REQ-006 — AES-256 Encryption for Intake PII
- **Stakeholder (Requisitante):** Privacy Officer
- **Description:** All structured personal data captured during the intake phase (such as corporate emails and role descriptions) must be encrypted at rest utilizing the AES-256 algorithm.
- **Objective (why/result):** To protect stakeholder privacy in the event of a database breach, aligning with best practices for GDPR data security.
- **Type:** NFR
- **Priority:** H
- **Objective + CSF linkage:** OBJ-1 / CSF-1
- **Acceptance criteria (draft):**
  - Direct SQL queries to the stakeholder table return ciphered text, not plain text.
  - Decryption keys are managed via a secure environment variable vault, physically separated from the database layer.
- **Validation method:** Architecture Review / Security Penetration Test
- **Variant impact:** Yes

### REQ-007 — Stale Evidence Rejection Rule
- **Stakeholder (Requisitante):** Transition Lead
- **Description:** The system must analyze the generation date metadata of uploaded infrastructure or licensing reports and block the upload if the document is older than 15 days.
- **Objective (why/result):** To ensure the AMS DevTeam is designing the transition plan based on fresh, highly accurate operational data rather than outdated legacy documents.
- **Type:** FR
- **Priority:** M
- **Objective + CSF linkage:** OBJ-3 / CSF-3
- **Acceptance criteria (draft):**
  - Upon file selection, the system parses the document's internal creation date.
  - If the delta between the current system date and the creation date exceeds 15 days, a warning is shown and the file is rejected from the payload.
- **Validation method:** Automated File Parsing Test
- **Variant impact:** No

### REQ-008 — Stakeholder Authority Consistency Check
- **Stakeholder (Requisitante):** Transition Lead
- **Description:** The system must cross-reference the stated 'System Role' of the stakeholder with the permissions outlined in the uploaded Authorization Evidence document.
- **Objective (why/result):** To ensure that the individual requesting the AMS transition actually possesses the legal or administrative authority to hand over the required architectural data.
- **Type:** FR
- **Priority:** M
- **Objective + CSF linkage:** OBJ-3 / CSF-3
- **Acceptance criteria (draft):**
  - The system triggers a flag if the user's role is listed as "Junior Analyst" but the requested action requires "Director" level authorization.
  - The consistency check result is logged as part of the Intake Decision Engine evaluation.
- **Validation method:** Unit Testing
- **Variant impact:** No
