# Generated Scope — Lab 8

## Selected slice
- **Slice:** Slice A (Intake session → capture answers)
- **Short description:** A web form for the Transition Lead to register a stakeholder for an intake session, strictly enforcing GDPR data minimization rules.

## Actors / roles
- **Primary actor:** Transition Lead
- **Secondary actor (optional):** Privacy Officer (Auditor)

## Use Cases implemented
- **UC-01:** Register stakeholder details

## Requirements implemented (max 10)
- **REQ-001:** Restrict Stakeholder Data Collection
- **REQ-006:** AES-256 Encryption for Intake PII (Simulated at UI level for prototype)

## Variant constraints implemented (min. 2)
- **Constraint 1 (Data Minimization):** The system must not capture or allow the input of phone numbers; only Corporate Email and Role.
- **Constraint 2 (Privacy by Design):** The UI must immediately block submission and show a GDPR warning if a phone number format is detected via regex.

## Out of scope (explicit)
- Database backend deployment (using local browser memory for this prototype).
- Full decision engine evaluation.
- Authentication/Login screens.
