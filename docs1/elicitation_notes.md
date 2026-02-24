# Elicitation Notes — Lab 2 (AMS)

## Interview setup
- Date: 2026-02-XX
- Client team: AMS Transition Lead
- DevTeam: RDLC
- Slice discussed: Intake & Discovery (AMS)
- Variant: 9 — Privacy & Data Retention (GDPR Persona)

---

## Context anchors (AMS)

- Sector: Healthcare
- Solution type: Custom + CRM integration
- Support model: L1/L2/L3, 24/7 support, English + Portuguese
- Key transition pain points:
  - Missing DR test evidence
  - Unclear ownership of dashboards
  - Inconsistent access control records
  - No structured retention tracking for personal data

---

## Questions & Answers (min. 10)

1. Q: What information must be collected during Intake?
   A: System inventory, integrations, access roles, DR/BCP details, monitoring dashboards, support contacts.

2. [Evidence] Q: What evidence proves that Disaster Recovery testing was performed?
   A: A dated DR test report signed by the infrastructure owner.

3. Q: Who is responsible for providing integration documentation?
   A: The Application Owner or Technical Lead.

4. [Variant] Q: What personal data is collected during the transition process?
   A: Contact names, emails, phone numbers, and access credentials.

5. [Variant] Q: Is there a defined retention period for collected transition data?
   A: Currently, no formal retention period is enforced.

6. [Evidence] Q: How fresh must monitoring evidence be?
   A: Monitoring dashboards must show activity within the last 30 days.

7. Q: What happens when required information is missing?
   A: The transition is delayed until the missing data is provided.

8. [Evidence] Q: Who owns the evidence provided during Intake?
   A: The stakeholder submitting the documentation remains the source of truth.

9. [Variant] Q: Is there a mechanism to delete or anonymize personal data after transition completion?
   A: No automated mechanism exists today.

10. Q: Are access roles formally documented?
    A: Partially, but not always updated.

11. [Evidence] Q: How is access validation verified?
    A: Through screenshots or exported access control lists.

12. Q: What are common failure points in transitions?
    A: Missing monitoring configuration and undocumented integrations.

---

## Raw Needs (derived from interview)

1. We need a structured intake form for transition data.
2. We need to record system owners and contacts.
3. We need to capture integration dependencies.
4. We need to validate completeness before proceeding.
5. We need to detect missing DR test documentation.
6. We need to track monitoring dashboard ownership.
7. We need to verify access role documentation.
8. We need to store evidence links.
9. We need to know the freshness of submitted evidence.
10. We need to flag incomplete submissions.
11. We need to record personal data categories collected.
12. We need to enforce data minimization during intake.  [Variant]
13. We need to define a retention policy for transition data.  [Variant]
14. We need to anonymize personal data after retention expires.  [Variant]
15. We need an audit trail for data changes.

---

## Assumptions (min. 3)

- A1: All stakeholders are willing to provide required documentation.
- A2: Monitoring dashboards are accessible at the time of transition.
- A3: Personal data collected is limited to business contacts only.
- A4: Retention rules will be defined by the Privacy Officer.

---

## Open questions (min. 3)

- Q1: What is the legally required retention period for transition-related personal data?  [Variant]
- Q2: Should personal data be anonymized or permanently deleted after retention?  [Variant]
- Q3: Who is responsible for approving data deletion?
- Q4: Is encryption required for stored intake documentation?
- Q5: Should audit logs be immutable?

---

## Variant notes (required)

- The GDPR/privacy focus shifted our elicitation toward:
  - Data minimization during intake
  - Retention period definition
  - Personal data anonymization
  - Auditability of data changes
  - Ownership and freshness of evidence
