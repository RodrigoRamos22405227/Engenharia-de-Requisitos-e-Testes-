# Test Cases — Lab 9

## TC-001 — Valid Stakeholder Registration (Happy Path)
- **Type:** Acceptance
- **Priority:** H
- **Related requirements:** REQ-001, REQ-006
- **Preconditions:** Transition Lead is logged into the Intake Dashboard.
- **Test data:** Email = "luis.almoster@company.com", Role = "Transition Lead".
- **Steps:**
  1. Navigate to the "Add Stakeholder" form.
  2. Input the valid Test data.
  3. Click "Save Stakeholder".
- **Expected results:**
  - Form submits successfully.
  - Success message "Stakeholder securely registered" is displayed.
  - Data is saved in the database in AES-256 encrypted format.

## TC-002 — Block Phone Number Input (Negative/Error)
- **Type:** System
- **Priority:** H
- **Related requirements:** REQ-001
- **Preconditions:** Form is open and ready for input.
- **Test data:** Email = "cristiano912345678@company.com", Role = "Contributor".
- **Steps:**
  1. Enter the test email containing a 9-digit number sequence.
  2. Click "Save Stakeholder".
- **Expected results:**
  - Submission is immediately blocked.
  - Red validation error "GDPR Violation: Personal phone numbers are prohibited" is displayed.
  - The input field is cleared.

## TC-003 — Existing Stakeholder Linking (Alternative Flow)
- **Type:** Integration
- **Priority:** M
- **Related requirements:** REQ-001
- **Preconditions:** "rodrigo@company.com" already exists in the system database.
- **Test data:** Email = "rodrigo@company.com", Role = "Director".
- **Steps:**
  1. Input the email of the existing user.
  2. Click "Save Stakeholder".
- **Expected results:**
  - System bypasses new user creation.
  - Existing profile is linked to the current intake session without duplicating database records.

## TC-004 — Stale Evidence Rejection (Boundary Test)
- **Type:** System
- **Priority:** H
- **Related requirements:** REQ-004, REQ-007
- **Preconditions:** User is uploading Architecture documents.
- **Test data:** Document A (Creation Date = 15 days ago), Document B (Creation Date = 16 days ago).
- **Steps:**
  1. Upload Document A and click evaluate.
  2. Clear session.
  3. Upload Document B and click evaluate.
- **Expected results:**
  - Document A is accepted (Boundary valid limit).
  - Document B is rejected (Boundary exceeded), triggering a "Stale Evidence" error.

## TC-005 — Immutable Audit Trail Generation (Integration)
- **Type:** Integration
- **Priority:** H
- **Related requirements:** REQ-003
- **Preconditions:** An uploaded evidence file is marked as "Confidential".
- **Steps:**
  1. Privacy Officer clicks "View" on the confidential file.
  2. Check the internal `AuditLogs` database table.
- **Expected results:**
  - A new row is appended to the `AuditLogs` table.
  - The row contains the exact UTC Timestamp, Action "VIEW", and the User ID.

## TC-006 — Missing Information Generates Deficit Report (Alternative)
- **Type:** Acceptance
- **Priority:** M
- **Related requirements:** REQ-004, REQ-005
- **Preconditions:** Intake session is submitted.
- **Test data:** Missing field "SLA Matrix".
- **Steps:**
  1. Leave "SLA Matrix" empty.
  2. Click "Submit Intake for Evaluation".
- **Expected results:**
  - Session status updates to "Need More Data".
  - A downloadable PDF Deficit Report is generated listing "SLA Matrix" as missing.

## TC-007 — 30-Day Abandoned Purge execution (Boundary/System)
- **Type:** System
- **Priority:** H
- **Related requirements:** REQ-002
- **Preconditions:** Cron Scheduler is triggered artificially via test script.
- **Test data:** Session A (Inactive 29 days, 23 hours), Session B (Inactive 30 days, 1 hour).
- **Steps:**
  1. Execute the nightly Cron job script.
  2. Query the database for Session A and Session B.
- **Expected results:**
  - Session A remains in the database.
  - Session B and all its attached evidence are hard-deleted.

## TC-008 — Unauthorized Authority Transition (Negative/Error)
- **Type:** System
- **Priority:** M
- **Related requirements:** REQ-008
- **Preconditions:** User attempts to approve architectural evidence.
- **Test data:** User Role = "Contributor". Required Role = "Director".
- **Steps:**
  1. Submit the evaluation payload.
- **Expected results:**
  - Evaluation fails immediately.
  - Error message "Insufficient Authority Level" is displayed.
