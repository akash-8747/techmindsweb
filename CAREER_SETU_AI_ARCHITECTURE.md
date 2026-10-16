# Career Setu AI

*AI-Enabled Career Counselling and Family Decision-Support Platform for Vocational Education*

## System Architecture

```mermaid
---
title: Career Setu AI — System Architecture
---
flowchart LR
    subgraph L1["Layer 1 — Presentation"]
        direction TB
        Actors["Student · Parent / Guardian · Mentor / Counsellor"]
        UI["Responsive, mobile-friendly web frontend<br/>Accessible controls · voice input for parents · voice guidance"]
        Home["Home page<br/>AI career assessment · free learning planner · family decision support<br/>Student profile and interests · AI chatbot · course comparison · recommendations"]
        Family["Family dashboard<br/>Progress overview · comparison graphs · key insights · course details and costs<br/>Required skills · learning roadmap · percentages · visual reports"]
        AssessUI["Assessment and assignment module<br/>Career · skill · competency assessments<br/>Personal counselling and mentoring"]
        Schemes["Government schemes<br/>PMKVY — Pradhan Mantri Kaushal Vikas Yojana<br/>NAPS — National Apprenticeship Promotion Scheme<br/>ITI / CTS — Industrial Training Institute / Craftsmen Training Scheme<br/>SSP — State Scholarship Portal and fee support<br/>Self-employment and government support"]
        Access["Rural accessibility<br/>Simple-language explanations · voice guidance<br/>Green / yellow / red indicators · graphs and progress percentages"]
        ReportsUI["Accountability and reporting<br/>Monthly reports · monitoring · student / parent / mentor notifications<br/>Inactivity follow-up · updated plans · counselling reminders"]
        Actors --> UI
        UI --> Home
        UI --> Family
        UI --> AssessUI
        UI --> Schemes
        UI --> Access
        UI --> ReportsUI
    end

    subgraph L2["Layer 2 — Application and API"]
        direction TB
        API["Backend API"]
        Auth["Authentication and authorization<br/>Separate credentials · RBAC · role-scoped view / edit permissions"]
        FamilySvc["User and family management<br/>First-time student registration · optional parent / mentor invitations<br/>Link accounts to student / family · consent-based progress sharing"]
        AssessSvc["Assessment processing"]
        CompareSvc["Course comparison"]
        PlannerSvc["Planner management"]
        ProgressSvc["Progress tracking"]
        Auth --> FamilySvc
        API --> Auth
        API --> AssessSvc
        API --> CompareSvc
        API --> PlannerSvc
        API --> ProgressSvc
    end

    subgraph L3["Layer 3 — AI Services"]
        direction TB
        Reco["AI career recommendation engine"]
        AssessAI["Career, skill, and competency assessment engine"]
        Chat["AI chatbot"]
        Match["Course and skill matching"]
        Roadmap["Career roadmap generation"]
        Language["Simple-language response generation"]
        Voice["Voice-to-text and text-to-speech"]
        Provider["AI provider, e.g. Gemini API<br/>Recommendations are guidance, not guaranteed outcomes"]
        Provider --> Reco
        Provider --> AssessAI
        Provider --> Chat
        Provider --> Match
        Provider --> Roadmap
        Provider --> Language
        Provider --> Voice
    end

    subgraph L4["Layer 4 — Data and Integrations"]
        direction TB
        UserDB[("User and role database")]
        ProfileDB[("Student profile database")]
        AssessmentDB[("Assessment results database")]
        CourseDB[("Course information database")]
        SchemeDB[("Government schemes database")]
        PlannerDB[("Learning planner and progress database")]
        ReportDB[("Monthly reports database")]
        Official["Official information sources<br/>Course and scheme verification"]
        Gmail["Gmail notification integration"]
        Official --> CourseDB
        Official --> SchemeDB
    end

    subgraph L5["Layer 5 — Automation and Monitoring"]
        direction TB
        Scheduler["Scheduled progress checks"]
        Status["Progress status calculation<br/>Green: satisfactory · Yellow: improvement needed<br/>Red: urgent attention / additional support"]
        Inactivity["Inactivity detection<br/>15–30 days"]
        Monthly["Monthly report generation"]
        Notify["Gmail notification service"]
        Followup["Follow-up counselling reminders"]
        PlanUpdate["Learning plan updates"]
        Scheduler --> Status
        Scheduler --> Inactivity
        Scheduler --> Monthly
        Inactivity --> Notify
        Status --> Followup
        Status --> PlanUpdate
        Monthly --> Notify
    end

    UI -->|"Role-scoped requests and consent"| API
    API -->|"Chat requests"| Chat
    AssessSvc -->|"Assessment answers"| AssessAI
    AssessAI -->|"Strengths and skill-gap results"| Reco
    CompareSvc -->|"Course and skills matching"| Match
    PlannerSvc -->|"Learning goals and plan"| Roadmap
    CourseDB -->|"Verified course data"| Match
    Chat -->|"Accessible explanations"| Language
    API -->|"Voice input / response request"| Voice
    Voice -->|"Transcript / spoken response"| API
    API -->|"Read / write: roles, family links"| UserDB
    API -->|"Read / write: profile and interests"| ProfileDB
    API -->|"Read / write: assessments"| AssessmentDB
    API -->|"Read: courses and schemes"| CourseDB
    API -->|"Read: schemes"| SchemeDB
    API -->|"Read / write: plans and progress"| PlannerDB
    API -->|"Read / write: reports"| ReportDB
    PlannerDB -->|"Progress data"| Scheduler
    Scheduler -->|"Report records"| ReportDB
    Notify -->|"Preference- and permission-checked email"| Gmail
    Gmail -->|"Delivery status"| Notify
    Notify -->|"Authorized alerts"| API
    PlanUpdate -->|"Updated plan"| PlannerDB

    classDef user fill:#eaf4ff,stroke:#2563a6,color:#17324d,stroke-width:1.5px
    classDef app fill:#dff5f2,stroke:#168b83,color:#123d3a,stroke-width:1.5px
    classDef ai fill:#e9e5ff,stroke:#6750a4,color:#2d2450,stroke-width:1.5px
    classDef data fill:#f2f6fa,stroke:#627d98,color:#243b53,stroke-width:1.5px
    classDef automation fill:#fff3d6,stroke:#c18b22,color:#553b08,stroke-width:1.5px
    classDef legend fill:#ffffff,stroke:#627d98,color:#243b53
    class Actors,UI,Home,Family,AssessUI,Schemes,Access,ReportsUI user
    class API,Auth,FamilySvc,AssessSvc,CompareSvc,PlannerSvc,ProgressSvc app
    class Reco,AssessAI,Chat,Match,Roadmap,Language,Voice,Provider ai
    class UserDB,ProfileDB,AssessmentDB,CourseDB,SchemeDB,PlannerDB,ReportDB,Official,Gmail data
    class Scheduler,Status,Inactivity,Monthly,Notify,Followup,PlanUpdate automation
    LEGEND["Legend<br/>Blue: presentation · Teal: application · Purple: AI<br/>Slate: data / integrations · Amber: automation<br/>Green / yellow / red: progress status"]
    class LEGEND legend
```

## End-to-End User Workflow

```mermaid
---
title: Career Setu AI — End-to-End User Workflow
---
flowchart LR
    subgraph START["Registration and setup"]
        direction LR
        N1["1. Student registers<br/>on Career Setu AI"]
        N2["2. Creates profile<br/>Interests · education · location · goals"]
        N3["3. Optionally invites<br/>parent and mentor"]
        N4["4. Each user signs in<br/>separate credentials · linked family accounts<br/>role-scoped access · consent-based sharing"]
        N1 --> N2 --> N3 --> N4
    end

    subgraph ASSESS["Assess and recommend"]
        direction LR
        N5["5. Student completes<br/>career, skill, and competency assessments"]
        D1{"Assessment<br/>complete?"}
        N6["6. Assessment engine evaluates<br/>strengths and skill gaps"]
        N7["7. AI suggests careers,<br/>courses, and learning paths"]
        N8["8. Compare courses<br/>fees · duration · skills · eligibility · opportunities"]
        N9["9. Identify relevant opportunities<br/>training · apprenticeships · scholarships · self-employment"]
        N5 --> D1
        D1 -->|"No: complete remaining assessments"| N5
        D1 -->|"Yes"| N6 --> N7 --> N8 --> N9
    end

    subgraph DECIDE["Family decision and planning"]
        direction LR
        N10["10. Student and family review<br/>recommendations on Family Dashboard"]
        D2{"Counselling<br/>needed?"}
        N11["11. Mentor provides<br/>personalized counselling"]
        N12["12. Student follows<br/>Free Learning Planner and roadmap"]
        N10 --> D2
        D2 -->|"Yes"| N11 --> N12
        D2 -->|"No"| N12
    end

    subgraph MONITOR["Progress monitoring and follow-up"]
        direction LR
        N13["13. Track progress<br/>percentages · graphs · green / yellow / red status"]
        N14["14. Generate monthly reports<br/>for authorized users when due"]
        N15["15. Scheduled check<br/>inactivity 15–30 days or progress concern"]
        D4{"Inactive<br/>15–30 days?"}
        D3{"Sufficient<br/>progress?"}
        N16["16. Send Gmail alerts<br/>to relevant users, subject to preferences and permissions"]
        N17["17. Student resumes learning,<br/>gets support, and updates plan"]
        N18["18. Repeat progress-monitoring cycle"]
        N13 --> N14 --> N15 --> D4
        D4 -->|"Yes"| N16 --> N17 --> N18
        D4 -->|"No"| D3
        D3 -->|"Yes"| N18
        D3 -->|"No: support needed"| N16
        N18 --> N13
    end

    N4 --> N5
    N9 --> N10
    N12 --> N13

    LEGEND["Legend: rounded boxes = user or system action · diamonds = decisions<br/>Green = satisfactory · Yellow = improvement needed · Red = urgent attention / support"]
    classDef action fill:#eaf4ff,stroke:#2563a6,color:#17324d,stroke-width:1.5px
    classDef decision fill:#fff3d6,stroke:#c18b22,color:#553b08,stroke-width:1.5px
    classDef progress fill:#dff5f2,stroke:#168b83,color:#123d3a,stroke-width:1.5px
    classDef legend fill:#dff5f2,stroke:#168b83,color:#123d3a
    class N1,N2,N3,N4,N5,N6,N7,N8,N9,N10,N11,N12,N13,N14,N15,N16,N17,N18 action
    class D1,D2,D3,D4 decision
    class N13 progress
    class LEGEND legend
```

## Legend

- **Blue:** people-facing interfaces and workflow actions.
- **Teal:** application services and the legend callout.
- **Purple:** AI capabilities.
- **Slate:** databases and external information / email integrations.
- **Amber:** automation, monitoring, and decision points.
- **Progress status:** green = satisfactory, yellow = improvement needed, red = urgent attention or additional support.

See [`docs/README.md`](docs/README.md) for module explanations, data-flow notes, technology choices, and preview/export instructions.
