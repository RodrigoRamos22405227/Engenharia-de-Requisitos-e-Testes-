# Traceability — Requirements ↔ Test Cases (Lab 9)

## Selected requirements (8)
- **REQ-001** (FR): Restrict Stakeholder Data Collection
- **REQ-002** (NFR): Automated 30-Day Purge for Abandoned Sessions
- **REQ-003** (FR): Immutable Audit Trail for Sensitive Evidence
- **REQ-004** (FR): Intake Decision Engine Validation
- **REQ-005** (FR): Discovery Deficit Reporting
- **REQ-006** (NFR): AES-256 Encryption for Intake PII
- **REQ-007** (FR): Stale Evidence Rejection Rule
- **REQ-008** (FR): Stakeholder Authority Consistency Check

## Mapping (REQ → TC)

| Requirement (REQ-###) | Test Cases (TC-###) | Notes |
|---|---|---|
| REQ-001 | TC-001, TC-002, TC-003 | Covers happy path, duplicate variation, and GDPR negative block. |
| REQ-002 | TC-007 | System test for the 30-day cron boundary limit. |
| REQ-003 | TC-005 | Validates the immutable log creation. |
| REQ-004 | TC-004, TC-006 | Core decision engine tested via stale boundary and deficit alternatives. |
| REQ-005 | TC-006 | Evaluates the report generation output. |
| REQ-006 | TC-001 | Validates that data is stored encrypted upon registration. |
| REQ-007 | TC-004 | Boundary test for the 15-day document freshness rule. |
| REQ-008 | TC-008 | Negative test for insufficient role permissions. |
