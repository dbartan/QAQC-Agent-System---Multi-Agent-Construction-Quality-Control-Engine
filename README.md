# QAQC Agent System — Multi-Agent Construction Quality Control Engine

This system encodes 20+ years of real construction QAQC practice into a structured, AI-driven multi-agent framework. It is not a chatbot. It is a **decision + validation engine** for luxury hospitality construction projects.

---

## System Purpose

- Contractor submission control (MAR, MS, ITP, Shop Drawing, test reports)
- Spec + standard compliance check (clause-by-clause)
- QA document generation (ITP, QCP, MS, NCR, Checklists)
- Site inspection management (hold points, witness points, sign-off)
- NCR lifecycle management (raise → corrective action → close)
- Schedule tracking (submittal due dates, overdue flags, critical path impact)
- KPI + reporting (contractor performance, risk trends, weekly QA report)

---

## System Architecture

```
INPUT (Submittal / Site Issue / New Work Item)
         ↓
  ORCHESTRATOR AGENT (L0 — Brain)
         ↓
    ┌──────────────────────────────────────┐
    │ PHASE DETECTION → WBS MAPPING        │
    │ → AGENT ROUTING → CONFLICT CHECK     │
    └──────────────────────────────────────┘
         ↓
  L1 SPECIALIST AGENTS (parallel or sequential)
    ├── 01 Spec Compliance Agent
    ├── 02 Submittal Review Agent
    ├── 03 Document Generator Agent
    ├── 04 Site Inspection Agent
    ├── 05 NCR & Risk Agent
    ├── 06 Schedule Agent
    └── 07 Reporting Agent
         ↓
  HUMAN-IN-THE-LOOP GATE (where required)
         ↓
  STRUCTURED OUTPUT + REGISTER UPDATE
```

---

## Folder Structure

```
/qaqc-agent-system/
│
├── README.md                          ← System overview
├── AGENTS.md                          ← Agent registry + map (L0/L1/L2)
├── CONTEXT.md                         ← System-wide rules & DNA
├── RULES.md                           ← 15 master rules (absolute)
├── WORKFLOWS.md                       ← Workflow index + routing logic
│
├── agents/                            ← Agent definitions
│   ├── 00_orchestrator.md
│   ├── 01_spec_compliance_agent.md
│   ├── 02_submittal_review_agent.md
│   ├── 03_document_generator_agent.md
│   ├── 04_site_inspection_agent.md
│   ├── 05_ncr_risk_agent.md
│   ├── 06_reporting_agent.md
│   ├── schedule_agent.md
│   ├── spec_parser_agent.md
│   └── installation_checklist_agent.md
│
├── context/                           ← Project context + standards
│   ├── project_context.md
│   ├── phases.md
│   ├── wbs_template.md
│   ├── quality_tier.md                ← Luxury/hospitality tier rules
│   ├── master_standards.md
│   ├── spec_index.md
│   └── schedule_logic.md              ← Lead time & tracking rules
│
├── skills/                            ← Reusable skill modules
│   ├── review_submittal.md
│   ├── spec_compliance_check.md
│   ├── generate_itp.md
│   ├── generate_ms.md
│   ├── generate_qcp.md
│   ├── generate_ncr.md
│   ├── inspection_checklist.md
│   ├── mockup_approval.md
│   └── reporting_kpi.md
│
├── workflows/                         ← Process flows
│   ├── material_approval_workflow.md  ← WF-01
│   ├── method_statement_workflow.md
│   ├── submittal_review_workflow.md
│   ├── itp_generation_workflow.md
│   ├── inspection_workflow.md
│   ├── ncr_workflow.md
│   ├── mockup_approval_workflow.md    ← Luxury mockup hierarchy
│   ├── test_workflow.md
│   ├── handover_workflow.md
│   ├── schedule_tracking.md           ← Daily/weekly tracking
│   └── conflict_resolution.md         ← Agent conflict handling
│
├── policies/                          ← Rules, approval matrix
│   ├── approval_matrix.md             ← Agent vs human authority
│   ├── qa_rules.md
│   ├── severity_matrix.md             ← NCR severity classification
│   └── decision_logic.md
│
├── data_model/                        ← Registers + data structures
│   ├── work_items.md
│   ├── submittal_register.md
│   ├── test_inspection_register.md
│   ├── ncr_register.md
│   └── document_register.md
│
├── templates/                         ← Output document templates
│   ├── itp_template.md
│   ├── ms_template.md
│   ├── qcp_template.md
│   ├── ncr_template.md
│   ├── inspection_checklist_template.md
│   ├── mar_template.md
│   └── submittal_cover_sheet.md
│
├── knowledge_base/                    ← Specs, standards, past projects
│   ├── specs/parsed/                  ← Structured spec sections
│   ├── standards_index.md
│   └── past_projects_index.md
│
└── data/past_projects/                ← Learning layer
    ├── approved/                      ← Best-performing documents
    ├── rejected/                      ← Failed approaches
    └── lessons_learned/               ← Project lessons
```

---

## How to Use

1. Load `context/project_context.md` first (project-specific)
2. Load `context/spec_index.md` (parsed spec clauses for this project)
3. Load `RULES.md` (15 master rules — always active)
4. Load `CONTEXT.md` (system-wide logic)
5. Activate Orchestrator Agent
6. Feed input (submittal / site issue / new work item)
7. Orchestrator routes → specialist agents process → output generated
8. Human sign-off gate applied where required (see `policies/approval_matrix.md`)

---

## Critical Rules (Summary — see RULES.md for full)

| Rule | Name | Summary |
|------|------|---------|
| R-01 | No Assumption | Missing info = INCOMPLETE flag, never assume |
| R-02 | Clause Reference | Every decision must cite spec clause |
| R-03 | Sequence | No work without approved MAR + MS + ITP |
| R-04 | Hold Point | H points = absolute, human sign-off only |
| R-05 | Test Failure | Failed test = immediate NCR, work suspended |
| R-06 | Conflict | Conflicting agents = HOLD + escalate |
| R-07 | Resubmission | Must address all previous comments |
| R-08 | Critical NCR | Immediate escalation, stop work |
| R-09 | Traceability | Every output carries ID, phase, ref, date |
| R-10 | Draft | Agent docs = DRAFT until human approved |
| R-11 | Mockup | No mass production without mockup sign-off |
| R-12 | Material On Site | No install without approved MAR + MIR |
| R-13 | Overdue Submittal | 7/14/21 day escalation triggers |
| R-14 | Standard Hierarchy | Stricter requirement always applies |
| R-15 | Learning Capture | Save best docs + lessons after phase handover |

---

**Version:** 1.0  
**Author:** QAQC System — Field-Encoded  
**Domain:** Luxury Hospitality Construction (5-star hotel / branded residence / villa)
