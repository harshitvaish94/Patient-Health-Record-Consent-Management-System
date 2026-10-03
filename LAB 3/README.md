## LAB 3 — Component Modeling & Architectural Pattern Selection

> **Course:** Software Engineering  
> **Problem Statement:** #13 — Patient Health Record Consent Management System  
> **Submission Format:** Folder per student containing individual PDF and UML Component Diagram  

---

## Lab Overview & Objectives

Lab 3 focuses on defining the high-level structural breakdown and architectural pattern selection for the **Patient Health Record Consent Management System**. 

The main objectives of this deliverable include:
1. **Component Modeling:** Designing a detailed UML Component Diagram with clear interfaces (provided/required ball-and-socket notation) representing system components across all operational layers.
2. **Architectural Pattern Justification:** Selecting and justifying an appropriate system architecture (3-Tier Layered Architecture) over alternative paradigms (such as Microservices or Client-Server) based on functional and non-functional requirements (FR-001 to FR-003, NFR-001, NFR-002).
3. **Interface & Boundary Mapping:** Establishing clear trust boundaries, authentication flows (MFA), and data persistence abstractions (append-only audit logs and encrypted databases)[cite: 30, 31].

---

## Submission Directory Structure

Inside the `LAB 3` directory, each team member has a dedicated subfolder named after their respective **SRN**.

```text
LAB 3/
├── README.md                            
│
├── PES1UG24AM116/                       # Individual Submission Folder — Harshit Vaish
│   ├── README.md                        
│   ├── Lab3_Component_Diagram.png       
│   └── PES1UG24AM116_LAB3_Justification.pdf 
│
├── PES1UG24AM107/                       # Individual Submission Folder — Nakka Gopya
│   ├── README.md
│   ├── Lab3_Component_Diagram.png
│   └── PES1UG24AM107_LAB3_Justification.pdf
│
├── PES1UG24AM066/                       # Individual Submission Folder — Bhavya K
│   ├── README.md
│   ├── Lab3_Component_Diagram.png
│   └── PES1UG24AM066_LAB3_Justification.pdf
│
└── PES1UG24AM1080/                       # Individual Submission Folder — Devika N
    ├── README.md
    ├── Lab3_Component_Diagram.png
    └── PES1UG24AM080_Justification.pdf
