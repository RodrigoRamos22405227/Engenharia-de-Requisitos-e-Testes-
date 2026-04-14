# Acceptance Criteria — Lab 7

## REQ-001 — Restrict Stakeholder Data Collection (Given/When/Then)
- **Given** a user is filling out the "Add Stakeholder" form.
- **When** the user attempts to enter a string matching a phone number format (e.g., "+351 912 345 678") into the email or role field.
- **Then** the system immediately displays a GDPR validation error ("Personal phone numbers are prohibited") and disables the submit button.
- **AC-Variant:** The database schema for `Stakeholder` shall not contain columns for `FirstName`, `LastName`, or `PhoneNumber`.

## REQ-002 — Automated 30-Day Purge for Abandoned Sessions (Given/When/Then)
- **Given** an Intake Session has a `last_activity_date` exactly 30 days in the past.
- **When** the nightly midnight Cron Scheduler job executes.
- **Then** the session record and all associated PII and uploaded files are permanently hard-deleted from the database and storage.
- **AC-Variant:** The system logs a generic "Session Purged" metric for statistical purposes, containing zero identifiable user data.

## REQ-003 — Immutable Audit Trail for Sensitive Evidence
- **AC-1:** Every time a file tagged as 'Confidential' is opened, a log entry must be created within 1 second.
- **AC-2:** The log entry must contain: User ID, IP Address, UTC Timestamp, and Action Type (VIEW/DOWNLOAD).
- **AC-3:** If a database administrator attempts to execute a `DELETE` or `UPDATE` SQL statement on the `AuditLogs` table, the database engine must reject the transaction.

## REQ-004 — Intake Decision Engine Validation
- **AC-1:** The status changes to "Ready to Proceed" only if `missing_fields_count == 0` and all evidence files have a `valid == true` flag.
- **AC-2:** The system must lock all text inputs on the Intake form the moment the evaluation begins.
- **AC-3:** If the stakeholder's role does not equal "Director" or "C-Level" when submitting architectural evidence, the evaluation must fail.

## REQ-005 — Discovery Deficit Reporting
- **AC-1:** The report must explicitly list the exact UI label names of any missing mandatory fields.
- **AC-2:** The report must provide a "Download as PDF" button.
- **AC-3:** The generated PDF must include the timestamp of the evaluation and the name of the Transition Lead who triggered it.

## REQ-006 — AES-256 Encryption for Intake PII
- **AC-1:** Data extracted directly from the `CorporateEmail` column via raw SQL must appear as an undecipherable AES-256 encrypted string.
- **AC-2:** The system must decrypt the data on-the-fly at the application layer only when an authorized user views the dashboard.
- **AC-3:** The encryption keys must be stored in a separate environment variables vault, not in the primary database.
