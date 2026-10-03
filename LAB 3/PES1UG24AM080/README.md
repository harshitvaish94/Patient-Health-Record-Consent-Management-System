# Lab 3: Component Modeling & Architectural Pattern Selection

**Name:** Devika N  
**SRN:** PES1UG24AM080  
**Section:** B  
**Course:** Software Engineering  
  

---
## Project
Patient Health Record Consent Management System (Problem Statement #13, Healthcare & Telemedicine).

A patient-centric health data gateway where patients grant time-bound consent for clinic doctors to access their diagnostic records. Patients can revoke consent at any time and view a full audit trail.

## Folder Contents

| File Name | Description |
| :--- | :--- |
| **`Lab3_Component_Diagram.png`** | UML Component Diagram illustrating the 3-Tier Layered Architecture and interfaces. |
| **`PES1UG24AM080_Justification.pdf`** | Detailed technical justification for selecting a Layered Architecture over Microservices and Client-Server models. |
| **`README.md`** | Overview and summary of component interactions and architectural reasoning. |

---

## Architectural Choice: 3-Tier Layered Architecture

The **Patient Health Record Consent Management System** implements a strict 3-tier layered architecture where each layer communicates exclusively with the layer directly beneath it through well-defined ball-and-socket interfaces:

1. **Presentation Layer:** Contains the `User Interface` accessible by Patients, Doctors, and Clinic Administrators.
2. **Business Layer:** Encapsulates business logic across four key components:
   * `Consent Manager` (handles grant, revoke, and expiry logic)
   * `Authentication` (enforces Multi-Factor Authentication checks)
   * `Notification Service` (dispatches alerts)
   * `Audit Logger` (records consent and access activities)
3. **Data Layer:** Maintains core persistent storage via:
   * `Consent & Health Record Database`
   * `Audit Log Database` (append-only write stream)

---

## Key Architectural Justifications

* **Single Enforcement Point for Consent Rules:** Every record request and consent evaluation (FR-001 to FR-003) is routed through the Business layer. The UI cannot access the Data layer directly, ensuring consent checks cannot be bypassed.
* **Strong Consistency & Low Latency:** Supports the 5-second revocation target (FR-002) and append-only auditing (NFR-001) by keeping state in an authoritative data layer without the network latency or eventual consistency issues of microservices.
* **Security & Clear Trust Boundaries:** Centralizes AES-256 encryption at rest and TLS 1.2+ in transit (NFR-002) at the data queries interface. Doctor MFA authentication sits in the Business layer, preventing password-only access.
* **Tamper-Evident Audit Protection:** The `Audit Log Database` exposes an append-only write API, preventing modification or deletion of log entries by high-privilege users.
