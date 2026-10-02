# Lab 3: Component Modelling & Architectural Pattern Selection

**Course:** Software Engineering | PES University, Dept. of CSE
**Name:** Harshit Vaish
**SRN:** PES1UG24AM116
**Section:** B
**Date:** 02 October 2026

---

## 1. Project

**Patient Health Record Consent Management System** (Problem Statement #13, Healthcare & Telemedicine).

A patient-centric health data gateway where patients grant granular, time-bound consent for clinic doctors to access their diagnostic records. Patients can revoke consent at any time and view a full audit trail. Doctors can use a break-glass emergency override on records the patient has flagged as emergency-eligible.

This lab builds on my earlier labs:

| Lab | Work | Used in Lab 3 |
|-----|------|---------------|
| Lab 1 | Requirements table (FR-001 to FR-006, NFR-001, NFR-002), use-case diagram (UC-01 to UC-06), use-case flow specification | Requirement IDs, use cases, and the numbers in the justification (24-hour grant, 5 s revoke, 3 s audit filter, 30 s emergency grant, AES-256, TLS 1.2+) |
| Lab 2 | Jira backlog: 5 Epics (SCRUM-11 to SCRUM-15), 14 user stories (SCRUM-16 to SCRUM-29), 68 story points, 2 sprints | Every Epic and story is mapped to a component |

---

## 2. Deliverables

| File | Description |
|------|-------------|
| `Lab3_Component_Diagram.png` | UML component diagram (image) |
| `Lab3_Component_Diagram.pdf` | UML component diagram (vector PDF) |
| `Lab3_Justification.pdf` | One-page written justification of the architecture choice |
| `Lab3_Justification.docx` | Editable Word version of the justification |

---

## 3. Architecture Chosen: Layered Architecture

I compared Layered, Microservices and Client-Server, and chose **Layered Architecture** with three layers:

- **Presentation Layer:** Patient & Doctor Portal
- **Business Layer:** Authentication Service, Consent Manager, Emergency Access Service, Notification Service, Audit Trail Service
- **Data Layer:** Encrypted Data Store

Requests flow from the Portal down through the Business Layer to the Data Layer.

### Why Layered
1. **One enforcement path for consent and audit.** Every grant, revoke and emergency override passes through the Consent Manager, which logs it via the Audit Trail Service. Emergency overrides reuse the Consent Manager's grant path, so they cannot skip the audit entry (FR-006, NFR-001).
2. **Components map directly onto the Lab 2 backlog.** All 5 Epics and all 14 stories have a clear home, and a system of this size does not need more than three layers.

### Security advantage
The Portal reaches health data only through the Business Layer, with authentication in front of every request. All records, grants and audit entries live in one Encrypted Data Store, so AES-256 at rest and TLS 1.2+ in transit (NFR-002) are enforced at one boundary. Audit entries are written only through the Audit Trail Service, keeping the trail append-only (NFR-001).

### Performance benefit
Grants, revocations and emergency flags sit in a single Data Layer, so a revoke is visible to the very next access check with no cross-service synchronisation. This supports the 5-second revocation target (FR-002), the 30-second emergency grant (FR-006) and the 3-second audit filter (FR-005).

### Why not the other styles
- **Microservices:** adds network latency, operational complexity and data-consistency risk between the grant store and audit trail. That is too costly for a system this size.
- **Client-Server:** only separates clients from one server and does not separate consent logic, audit and storage inside it. A single server block is also a bottleneck for emergency access.
- **Trade-off accepted:** with Layered, components cannot be scaled independently, which is acceptable for this scope.

---

## 4. Components

| Component | Layer | Responsibility | Use cases | Epics | Stories |
|-----------|-------|----------------|-----------|-------|---------|
| Patient & Doctor Portal | Presentation | Front end for patients and clinic doctors | UC-02 to UC-06 | SCRUM-11 to 15 | All (front end) |
| Authentication Service | Business | Login and verification of clinic doctors | UC-01 | SCRUM-11, 15 | SCRUM-17, 28 |
| Consent Manager | Business | Grant, revoke, custom expiry, access requests (adapted from the handout's *Order Manager*) | UC-02, 03, 06 | SCRUM-11, 12 | SCRUM-16, 18, 19, 20 |
| Emergency Access Service | Business | Emergency-eligible flags and break-glass override with justification | UC-05 | SCRUM-14 | SCRUM-25, 26 |
| Notification Service | Business | Doctor grant/revoke notices, expiry reminders, post-emergency patient notice | n/a (supporting) | SCRUM-12, 14 | SCRUM-21, 22, 27 |
| Audit Trail Service | Business | Append-only audit logging and filterable audit trail | UC-04 | SCRUM-13 | SCRUM-23, 24 |
| Encrypted Data Store | Data | Stores records, grants, flags and audit entries, encrypted with AES-256 | n/a | SCRUM-15 | SCRUM-29 |

The handout's *Payment Service* is adapted into the **Authentication Service**, which the Consent Manager calls to verify doctors.

---

## 5. Interfaces (11)

Each interface uses UML ball (provided) and socket (required) notation. The socket sits on the consumer and cups the ball on the provider.

| # | Interface | Provider (ball) | Consumer (socket) | Technology | Data flow |
|---|-----------|-----------------|-------------------|------------|-----------|
| 1 | IAuthentication | Authentication Service | Portal | API call | login request |
| 2 | IConsentService | Consent Manager | Portal | API call | grant / revoke / flag |
| 3 | IEmergencyAccess | Emergency Access Service | Portal | API call | break-glass request |
| 4 | IAuditQuery | Audit Trail Service | Portal | API call | audit trail query |
| 5 | IDoctorVerification | Authentication Service | Consent Manager | API call | doctor lookup |
| 6 | IGrantProcessing | Consent Manager | Emergency Access Service | API call | emergency grant |
| 7 | INotification | Notification Service | Consent Manager | API call | grant / revoke / reminder |
| 8 | IAuditLog | Audit Trail Service | Consent Manager | API call | log events |
| 9 | IProfileData | Encrypted Data Store | Authentication Service | database query | profile lookup |
| 10 | IConsentData | Encrypted Data Store | Consent Manager | database query | grants, records, flags |
| 11 | IAuditData | Encrypted Data Store | Audit Trail Service | database query | append-only entries |

---

## 6. Requirements Traceability

| Requirement | Covered by |
|-------------|-----------|
| FR-001 Time-bound access, auto-revoke at expiry | Consent Manager |
| FR-002 Revoke any time | Consent Manager |
| FR-003 Access request with reason | Consent Manager, Authentication Service |
| FR-004 Expiry reminder notification | Notification Service |
| FR-005 Filterable audit trail | Audit Trail Service |
| FR-006 Emergency break-glass access | Emergency Access Service, Notification Service |
| NFR-001 Append-only audit trail | Audit Trail Service, Encrypted Data Store |
| NFR-002 AES-256 at rest, TLS 1.2+ in transit | Encrypted Data Store, all interfaces |

---

## 7. How the diagram was made

The diagram is generated with Python and Matplotlib. It uses `<<component>>` stereotypes with the component icon, layer frames, and provided and required interface notation.

---

## 8. Author

**Harshit Vaish** | SRN: **PES1UG24AM116** | Section: **B**
