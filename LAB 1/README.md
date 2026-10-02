# LAB 1 — Patient Health Record Consent Management System

## Team Details

 
**Course:** Software Engineering  
**Assignment:** Lab 1  
**Problem Statement:** 13 — Patient Health Record Consent Management System

### Team Members

| Sl. No. | SRN | Name |
|---|---|---|
| 1 | PES1UG24AM080 | Devika N |
| 2 | PES1UG24AM107 | Naka Goya |
| 3 | PES1UG24AM066 | Bhavya K |
| 4 | PES1UG24AM116 | Harshit Vaish |

---

## 1. Problem Statement

**Problem Statement 13: Patient Health Record Consent Management System**

The objective is to design a system that gives patients control over access to their diagnostic health records while allowing verified clinic doctors to access necessary information with appropriate authorization.

The system must support time-bound consent, immediate revocation, access requests with a stated purpose, notifications, audit trails, and emergency access when a patient cannot provide consent in time.

The solution focuses on patient control, secure sharing of sensitive medical information, transparency, and accountability.

## 2. Proposed Solution

We propose a **Patient Health Record Consent Management System** in which patients can manage permissions for individual diagnostic records and verified clinic doctors can request access for specific medical purposes.

The system uses a consent-based access model. Patients select which records to share, identify the verified doctor, and determine how long access should remain active. Permissions expire automatically, and patients can revoke them before expiry.

For medical emergencies, the system provides a separate emergency access override for records that patients have explicitly marked as eligible. Doctors must provide a justification, and the event is recorded for subsequent review.

The proposed solution consists of the following core capabilities:

- **Patient-controlled consent:** Patients decide which diagnostic records can be shared and with whom.
- **Time-bound permissions:** Access is granted for a defined duration, with 24 hours as the default.
- **Revocation:** Patients can withdraw previously granted permissions before their scheduled expiry.
- **Verified doctor access:** Only doctors with verified profiles can receive access.
- **Access transparency:** Patients can review a filterable history of consent and record-access events.
- **Emergency override:** Verified doctors can request temporary access to emergency-eligible records, subject to mandatory justification and audit logging.
- **Data protection:** Health records and consent information are protected through encryption and a tamper-evident audit trail.

## 3. Functional Requirements

The system is defined by six functional requirements.

### FR-001: Time-Bound Access Permissions

Patients shall be able to grant verified clinic doctors access to specific diagnostic records for a limited duration.

- The default access duration is 24 hours.
- The patient selects the record or records to share.
- The patient identifies the verified clinic doctor.
- The system creates a permission linked to the selected records, doctor, and expiry timestamp.
- Access must automatically stop when the permission expires.

**Acceptance criterion:** Clinic access is automatically revoked at the expiry timestamp. Access after expiry must be denied.

### FR-002: Access Revocation

Patients shall be able to revoke any previously granted permission before its scheduled expiry.

- Patients can revoke access without waiting for the expiry time.
- The system must update the permission's status.
- Subsequent clinic access attempts must be denied.

**Acceptance criterion:** A clinic's access attempt is denied within five seconds of the patient selecting "Revoke."

### FR-003: Doctor Access Requests

Clinic doctors shall submit access requests before patients grant consent.

Each request must specify:
- Patient ID
- Requested record type
- Reason for access

Requests without a reason must be rejected with an error message.

**Acceptance criterion:** A request without a reason field is rejected and is not forwarded to the patient.

### FR-004: Consent Expiry Notifications

The system shall notify patients before an active consent grant expires.

- Notifications may be delivered through the in-app notification service, SMS, or email.
- The reminder should be sent approximately one hour before expiry.
- Patients can use the reminder as an opportunity to extend access or let it expire.

**Acceptance criterion:** Notification logs show a reminder sent 55–65 minutes before every grant's expiry timestamp.

### FR-005: Audit Trail

Patients shall be able to view a complete, filterable history of consent-related activities.

The audit trail shall include:
- Consent grants
- Consent revocations
- Diagnostic record-access events

Patients must be able to filter the history by date range and retrieve matching events.

**Acceptance criterion:** A date-range filter returns all matching events within three seconds, without missing entries.

### FR-006: Emergency Access Override

Patients shall be able to designate specific diagnostic records as eligible for emergency access.

During a medical emergency:
- Any verified clinic doctor may request immediate break-glass access to eligible records.
- The doctor must provide a mandatory justification.
- The system must restrict the override to records marked as emergency-eligible.
- The override must be logged immediately with the doctor's ID, timestamp, and justification.
- The patient must be notified as soon as connectivity allows.

**Acceptance criterion:** An eligible emergency override is granted within 30 seconds, requires a justification note, and is immediately logged. Requests against records that are not emergency-eligible must be denied.

---

## 4. Non-Functional Requirements

### NFR-001: Append-Only Audit Trail

All consent grants, revocations, and record-access events shall be permanently written to an append-only audit trail.

The audit trail is intended to provide a tamper-evident record of actions for compliance, accountability, and dispute resolution.

**Acceptance criterion:** Benchmarking tests confirm that the system meets its target latency and security standards under simulated peak load.

### NFR-002: Encryption and Data Security

All patient health records and consent data shall be encrypted:

- **At rest:** AES-256
- **In transit:** TLS 1.2 or higher

The system must prevent health information and consent data from being stored or transmitted in plaintext.

**Acceptance criterion:** A security scan confirms that no record is stored or transmitted unencrypted.

---

## 5. Use Cases

The solution defines two main workflows: giving access permission and emergency access override.

### UC-01: Authenticate User

**Purpose:** Authenticate users before they perform consent-management or record-access operations.

Authentication is included in both the patient consent-grant workflow and the emergency access workflow.

### UC-02: Give Access Permission

**Primary actor:** Patient  
**Supporting actors:** System, Notification Service, Audit Trail Service, Clinic Doctor

**Preconditions:**
1. The patient has a registered account and completed identity verification.
2. The clinic doctor has an active, verified profile.
3. The patient's diagnostic records already exist in the system.

**Main success scenario:**

1. The patient logs in and selects "Manage Consent" from the dashboard.
2. The system displays the patient's diagnostic records and a "Grant Access" option.
3. The patient selects the records to share and searches for the verified clinic doctor by name or clinic ID.
4. The system displays the doctor's verified profile for confirmation.
5. The patient sets the access duration, with 24 hours as the default, or chooses a custom expiry duration.
6. The patient confirms the grant.
7. The system validates the request, creates the time-bound permission, and records the event in the audit trail.
8. The system confirms the grant to the patient and notifies the clinic doctor.
9. The use case ends successfully.

**Alternate flow — Doctor not verified:**

- If the system cannot find a verified doctor matching the search, it displays a "Doctor not verified / not found" message.
- The system prevents the patient from granting access to that profile.
- The patient can search again or cancel.

**Alternate flow — Validation failure:**

- If the input is invalid, such as an expiry duration exceeding the permitted maximum, the system identifies the invalid field.
- The patient corrects the input and resubmits the request.

**Postconditions:**

- A time-bound access grant is linked to the specified records and clinic doctor.
- The grant and expiry timestamp are recorded in the append-only audit trail.
- The doctor can access the specified records until expiry or revocation.

### UC-03: Emergency Access Override

**Primary actor:** Clinic Doctor  
**Supporting actors:** System, Audit Trail Service, Notification Service, Patient

**Preconditions:**

1. The doctor has an active, verified profile.
2. The patient's diagnostic records already exist in the system.
3. At least one requested record is flagged as emergency-access eligible.

**Main success scenario:**

1. The clinic doctor logs in and selects "Request Emergency Access."
2. The system prompts the doctor to enter the patient identifier and a mandatory justification note describing the emergency.
3. The system verifies the doctor's credentials and checks whether the specified records are emergency-eligible.
4. The system grants temporary override access to eligible records and immediately records the event, including the justification, in the audit trail.
5. The system displays the records to the doctor and confirms the grant and its automatic expiry, such as four hours or until manually closed.
6. The system notifies the patient of the emergency access grant, including the doctor's identity and justification, through the preferred channel.
7. The use case ends successfully.

**Alternate flow — Record not emergency-eligible:**

- If none of the requested records are flagged as emergency-eligible, the system denies the override.
- The doctor is directed to the standard access-request flow.

**Alternate flow — Missing justification:**

- If the doctor attempts to submit without a justification note, the system rejects the request.
- The justification field is highlighted as required.
- The doctor enters the justification and resubmits.

**Postconditions:**

- A temporary emergency grant is created for the requesting doctor, limited to emergency-eligible records.
- The override event, doctor ID, timestamp, and justification are written to the audit trail.
- The patient is notified as soon as they are reachable.

---

## 6. System Workflow

### Standard Consent Workflow

The standard workflow gives the patient control over the entire sharing process.

1. **Authentication:** The patient logs into the system.
2. **Record selection:** The patient chooses the diagnostic records they want to share.
3. **Doctor verification:** The patient searches for and confirms the verified doctor.
4. **Duration selection:** The patient chooses the access duration.
5. **Consent confirmation:** The patient approves the permission.
6. **Permission creation:** The system creates the grant and stores its expiry timestamp.
7. **Audit logging:** The grant is written to the append-only audit trail.
8. **Notification:** The doctor is notified that access has been granted.
9. **Permission lifecycle:** Access remains available until expiry or revocation.
10. **Expiry reminder:** The patient receives a notification before the grant expires.

### Emergency Access Workflow

The emergency workflow allows temporary access when standard patient consent cannot be obtained in time.

1. The verified doctor authenticates.
2. The doctor enters the patient's identifier.
3. The doctor provides a mandatory emergency justification.
4. The system verifies the doctor and checks the emergency eligibility of the requested records.
5. If eligible, temporary override access is granted.
6. The system immediately records the event in the audit trail.
7. The system confirms the grant and its expiry.
8. The patient is notified as soon as connectivity allows.

If eligibility checks fail or the justification is missing, the system rejects the request.

---

## 7. Use-Case Diagram

The use-case diagram represents the interactions among three actors:

- **Patient:** Gives access permission, revokes access, views the audit trail, and participates in emergency-related consent management.
- **Clinic Doctor:** Requests access through the standard workflow or emergency override.
- **System:** Supports the authentication, notification, and audit functions.

The diagram includes the following use cases:

| Use Case ID | Use Case |
|---|---|
| UC-01 | Authenticate User |
| UC-02 | Give Access Permission |
| UC-03 | Revoke Access Permission |
| UC-04 | View Audit Trail |
| UC-05 | Emergency Access Override |
| UC-06 | Set Custom Expiry Duration |

Authentication is included in the relevant operations, custom expiry extends the standard grant workflow, and emergency override provides a separate path when standard consent cannot be obtained in time.

---

## 8. Security, Privacy, and Accountability

The proposed system treats patient consent and access history as essential parts of health-record protection.

**Patient control**
- Patients decide which diagnostic records to share.
- Patients authorize a particular verified doctor.
- Patients specify the permission duration.
- Patients can revoke permission before expiry.
- Patients can view their access history.

**Doctor verification**
- Only verified clinic doctors can receive standard access grants.
- Doctor verification is checked before access is granted.
- Emergency override requests also require verified doctor credentials.

**Auditability**
- Grants, revocations, and access events are recorded.
- Emergency overrides include the doctor's ID, timestamp, and mandatory justification.
- The append-only audit trail is intended to preserve a tamper-evident record.

**Data protection**
- AES-256 encryption is required for stored records and consent data.
- TLS 1.2 or higher is required for data in transit.
- Plaintext storage or transmission of patient records is not permitted.

---

## 9. Expected System Behavior

The following scenarios summarize the behavior expected from the proposed solution.

| Scenario | Expected Behavior |
|---|---|
| Patient grants access | Create a time-bound permission for the selected records and verified doctor. |
| Permission expires | Automatically deny further access after the expiry timestamp. |
| Patient revokes access | Deny the clinic's access attempt within five seconds of revocation. |
| Doctor submits request without a reason | Reject the request and display an error. |
| Consent is approaching expiry | Send a reminder 55–65 minutes before expiry. |
| Patient filters audit history | Return matching events within three seconds. |
| Doctor requests emergency access to an eligible record | Grant temporary access within 30 seconds, with justification and immediate logging. |
| Doctor requests an ineligible record | Deny the override and direct the doctor to the standard access-request flow. |
| Doctor omits emergency justification | Reject the submission and require a justification note. |
| Data is stored or transmitted | Apply the specified encryption requirements. |

---

## 10. Scope of the Proposed Solution

The Lab 1 solution specifies the system requirements, use cases, actors, workflows, acceptance criteria, and non-functional requirements for the Patient Health Record Consent Management System.

The principal scope includes:

- Patient-controlled sharing of diagnostic records.
- Verified clinic doctor access.
- Time-limited consent and automatic expiry.
- Early revocation.
- Purpose-specific access requests.
- Expiry notifications.
- Filterable audit history.
- Emergency access for eligible records.
- Encryption and append-only audit logging.

The requirements and workflows establish the expected behavior against which a future implementation can be designed and tested.

---

## 11. Individual Submissions

Each team member has submitted an individual PDF solution. All four submissions are maintained in this `LAB 1` folder.

| Team Member | SRN | PDF |
|---|---|---|
| Devika N | PES1UG24AM080 | `PES1UG24AM080.pdf` |
| Naka Goya | PES1UG24AM107 | `PES1UG24AM107.pdf` |
| Bhavya K | PES1UG24AM066 | `PES1UG24AM066.pdf` |
| Harshit Vaish | PES1UG24AM116 | `PES1UG24AM116.pdf` |

Each individual PDF should be retained as submitted. This README serves as the combined overview of the team's problem statement and proposed solution.

---

## 12. Repository Structure

```text
Patient-Health-Record-Consent-Management-System/
│
├── README.md
│
└── LAB 1/
    ├── README.md
    ├── PES1UG24AM080.pdf
    ├── PES1UG24AM107.pdf
    ├── PES1UG24AM066.pdf
    └── PES1UG24AM116.pdf
```

**Note:** The combined README documents the team's shared problem statement and solution concept. The individual PDFs contain each member's own submission.

---

**Course:** Software Engineering  
**Lab:** Lab 1  
**Team Size:** 4  
**Problem Statement:** 13 — Patient Health Record Consent Management System
