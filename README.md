# QAQC-Agent-System---Multi-Agent-Construction-Quality-Control-Engine
This system encodes 20+ years of real construction QAQC practice into a structured, AI-driven multi-agent framework. It is not a chatbot. It is a decision + validation engine for luxury hospitality construction projects.
# QAQC Agent System — Multi-Agent Construction Quality Control Engine

## System Purpose

This system encodes 20+ years of real construction QAQC practice into a structured, 
AI-driven multi-agent framework. It is not a chatbot. It is a **decision + validation engine** 
for luxury hospitality construction projects.

## What This System Does

- Contractor submission control (MAR, MS, ITP, Shop Drawing, test reports)
- Spec + standard compliance check (clause-by-clause)
- QA document generation (ITP, QCP, MS, NCR, Checklists)
- Site inspection management (hold points, witness points, sign-off)
- NCR lifecycle management (raise → corrective action → close)
- Schedule tracking (submittal due dates, overdue flags, critical path impact)
- KPI + reporting (contractor performance, risk trends, weekly QA report)

## System Architecture

```
INPUT (Submittal / Site Issue / New Work Item)
         ↓
  ORCHESTRATOR AGENT
         ↓
  ┌──────────────────────────────────────┐
  │  PHASE DETECTION → WBS MAPPING       │
  │  → AGENT ROUTING → CONFLICT CHECK   │
  └──────────────────────────────────────┘
         ↓
  SPECIALIST AGENTS (parallel or sequential)
  ├── Spec Compliance Agent
  ├── Submittal Review Agent
  ├── Document Generator Agent
  ├── Site Inspection Agent
  ├── NCR & Risk Agent
  └── Reporting Agent
         ↓
  HUMAN-IN-THE-LOOP GATE (where required)
         ↓
  STRUCTURED OUTPUT + REGISTER UPDATE
```

## Data Library (Project-Specific Inputs — changes per project)

Each project loads its own:
- Approved drawings (referenced, not stored in full)
- Project specifications (parsed into structured clause index)
- QMP / QCP
- Approved submittal list
- Project schedule (baseline)
- Brand standards (if applicable)

## Folder Structure

```
/qaqc-agent-system
├── README.md                        ← this file
├── AGENTS.md                        ← agent registry
├── CONTEXT.md                       ← system-wide rules
├── WORKFLOWS.md                     ← workflow index
│
├── agents/                          ← agent definitions
├── context/                         ← project context + standards
├── skills/                          ← reusable skill modules
├── workflows/                       ← process flows
├── policies/                        ← rules, approval matrix
├── data_model/                      ← registers + data structures
├── templates/                       ← output document templates
└── knowledge_base/                  ← specs, standards, past projects
```

## How to Use

1. Load `context/project_context.md` first (project-specific)
2. Load `context/spec_index.md` (parsed spec clauses for this project)
3. Activate Orchestrator Agent
4. Feed input (submittal / site issue / new work item)
5. Orchestrator routes → specialist agents process → output generated
6. Human sign-off gate applied where required (see `policies/approval_matrix.md`)

## Critical Rules

- Agent decisions are advisory except where explicitly marked [FINAL]
- All outputs must reference spec clause + drawing number
- No execution approval without all required submittals approved
- NCR cannot be closed without verified corrective action evidence
- Concrete pour / structural inspections = mandatory human sign-off, no exceptions

---
Version: 1.0
Author: QAQC System — Field-Encoded
