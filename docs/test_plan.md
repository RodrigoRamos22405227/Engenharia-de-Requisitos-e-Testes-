# Test Plan — Lab 10

## 1) Scope

- Slice covered:
  - AMS Intake Platform — Intake & Discovery
  - GDPR Privacy & Data Retention Variant (Variant 9)
  - Structured intake validation
  - Evidence upload and freshness verification
  - Intake readiness evaluation
  - Audit logging and retention enforcement

- Out of scope:
  - External CRM integrations
  - Long-term archival management
  - Full legal workflow automation
  - Real encryption infrastructure implementation
  - Production cloud deployment

---

## 2) Test strategy (static + dynamic)

### Static testing (reviews)

- What we review:
  - Requirements clarity and consistency
  - Acceptance Criteria quality
  - Use Case completeness
  - BDD scenario readability
  - Traceability consistency
  - Definition of Done enforceability

- Review checklist:
  - Is the requirement testable?
  - Are edge cases defined?
  - Are expected results measurable?
  - Are variant constraints explicit?
  - Are AC linked to tests?
  - Are conflicting requirements resolved?

### Dynamic testing (planned execution)

| Level | What we test | Examples | Evidence |
|---|---|---|---|
| Unit | Small logic/validation rules | Phone regex validation, retention countdown, stale evidence validation | Unit test logs |
| Integration | Component interactions | Upload evidence → validate freshness → evaluation engine | Integration test report |
| System | End-to-end slice | Intake → Evidence Upload → Evaluation → Deficit Report | Manual execution screenshots |
| Acceptance (BDD) | Behavior vs AC | GDPR rejection, successful intake evaluation | Gherkin feature files |

---

## 3) TDD plan (at least 2 candidates)

- Candidate 1 (REQ-006 — Data Minimization Enforcement):
  - Develop regex validation tests before implementing stakeholder form validation.
  - Validate rejection of phone-number patterns inside email fields.

- Candidate 2 (REQ-010 — Evidence Freshness Rule):
  - Create failing tests for evidence older than 30 days before implementing freshness validation logic.

- Why TDD is suitable:
  - These requirements contain deterministic business rules.
  - Validation logic is isolated and highly testable.
  - Edge cases can be automated early.

---

## 4) BDD plan (what behaviors become scenarios)

- Feature(s):
  - Stakeholder Registration
  - Intake Evaluation
  - GDPR Retention Enforcement
  - Evidence Freshness Validation

- Scenarios:
  - Successful stakeholder registration
  - GDPR violation blocks submission
  - Stale evidence rejection
  - Successful intake evaluation
  - Retention purge warning after 25 inactive days

- Links to REQs:
  - REQ-001
  - REQ-002
  - REQ-006
  - REQ-008
  - REQ-010

---

## 5) Coverage goals

- Happy path:
  - Valid stakeholder registration
  - Successful evidence upload
  - Successful evaluation leading to “Ready to Proceed”

- Alternative flows:
  - Existing stakeholder linked to session
  - Missing role defaults to “Contributor”
  - Deficit report generation

- Negative/error tests:
  - Public email rejection
  - Phone number GDPR violation
  - Missing DR evidence
  - Unauthorized evaluation attempt
  - Stale evidence rejection

- Boundary tests:
  - Evidence exactly 30 days old
  - Session inactive for exactly 25 days
  - Session purge at exactly 30 days
  - Maximum supported concurrent users

---

## 6) NFR validation approach

- NFR-001 — Performance
  - How we verify:
    - Simulated load testing
    - Response-time measurements under concurrent usage

- NFR-003 — Encryption at Rest
  - How we verify:
    - Database inspection
    - Security review demonstrating encrypted stored values

- NFR-005 — Retention Enforcement Timing
  - How we verify:
    - Automated retention job logs
    - Time-based simulation tests

- NFR-006 — RBAC
  - How we verify:
    - Role-based access tests
    - Unauthorized access attempts

---

## 7) Evidence recording and responsibilities

- Where results are stored (repo paths):
  - `/docs/test_cases.md`
  - `/docs/test_plan.md`
  - `/docs/traceability_req_ac_tc.md`
  - `/bdd/features/lab9.feature`
  - `/evidence/screenshots/`

- Who maintains traceability:
  - DevTeam Tester + Reviewer

- How updates are tracked:
  - GitHub commits
  - Pull request reviews
  - Trello validation cards
