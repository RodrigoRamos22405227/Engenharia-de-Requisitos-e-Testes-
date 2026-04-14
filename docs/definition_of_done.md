# Definition of Done (DoD) — Lab 7

## DoD — Requirement (REQ-###)
A requirement is considered "Done" when:
1. The REQ-### has a stable ID, clear title, and is categorized as FR, NFR, or Constraint.
2. The Primary Stakeholder (persona) and source of the requirement are explicitly recorded.
3. The description is unambiguous, focuses on user value, and avoids technical implementation leakage (the "how").
4. Acceptance criteria exist (minimum 2–4 bullets) and are independently testable/verifiable.
5. Variant impact (e.g., GDPR, Privacy, Audit) is stated (Yes/No) and justified where applicable.
6. Traceability links exist mapping the requirement to related Use Cases (UC-###) or Objectives.
7. Conflicts or duplicates found during validation have been resolved or documented.
8. The validation method (Automated Test, Code Review, Demo, Measurement) is explicitly defined.

## DoD — User Story (US-###)
A user story is considered "Done" when:
1. The story follows the standard Agile format (As a [role], I want [action], so that [value]) and is small enough to complete in one sprint.
2. Acceptance criteria are agreed upon by the DevTeam and the Product Owner, and are verifiable.
3. The implementation meets all AC perfectly (demonstrated in a staging environment).
4. Automated tests exist and pass successfully (Unit Tests and BDD integration tests where applicable).
5. No critical or high-priority defects remain open related to the story.
6. The codebase has been peer-reviewed and merged into the main branch.
7. Any necessary system documentation or API specifications have been updated.
8. The Client/Stakeholder accepts the outcome via a formal sprint validation demo.
