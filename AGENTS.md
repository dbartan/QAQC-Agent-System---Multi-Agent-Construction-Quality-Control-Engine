# AGENTS.md — QAQC Agent Registry

## Agent Hierarchy

```
ORCHESTRATOR (00)
│
├── L1 CORE AGENTS
│   ├── 01 — Spec Compliance Agent
│   ├── 02 — Submittal Review Agent
│   ├── 03 — Document Generator Agent
│   ├── 04 — Site Inspection Agent
│   ├── 05 — NCR & Risk Agent
│   └── 06 — Reporting Agent
│
└── CONFLICT HANDLER (embedded in Orchestrator)
```

---

## 00 — ORCHESTRATOR AGENT

**Role:** QAQC Manager AI — System Brain  
**File:** `agents/00_orchestrator.md`

Responsibilities:
- Receive all inputs (submittals, site issues, new work items)
- Detect phase and map to WBS
- Route to correct specialist agents
- Collect all agent outputs
- Check for conflicts between agent decisions
- Apply human-in-the-loop gate
- Issue final structured output

Routing Logic:
- Submittal received → Agent 01 + Agent 02
- New work item → Agent 03
- Site issue / inspection → Agent 04 + Agent 05
- NCR deviation found → Agent 05
- Weekly trigger → Agent 06

---

## 01 — SPEC COMPLIANCE AGENT

**Role:** Specification Validator  
**File:** `agents/01_spec_compliance_agent.md`

Input: Submittal + Spec Index + Standards  
Output: Compliance matrix, deviation list, risk flag  
Decision: COMPLIANT / NON-COMPLIANT / INCOMPLETE

---

## 02 — SUBMITTAL REVIEW AGENT

**Role:** Technical Reviewer  
**File:** `agents/02_submittal_review_agent.md`

Input: MAR / MS / ITP / Shop Drawing  
Output: Approval status, technical comments, action required  
Decision: APPROVED / REVISE & RESUBMIT / REJECTED

---

## 03 — DOCUMENT GENERATOR AGENT

**Role:** QAQC Document Producer  
**File:** `agents/03_document_generator_agent.md`

Input: Work item + Spec section + Template  
Output: MS / ITP / QCP / MAR / MIR / Inspection Checklist  

---

## 04 — SITE INSPECTION AGENT

**Role:** Field QAQC Validator  
**File:** `agents/04_site_inspection_agent.md`

Input: Work item + ITP + Site observation  
Output: Inspection checklist, hold point status, punch list  
Decision: PASS / FAIL / CONDITIONAL

---

## 05 — NCR & RISK AGENT

**Role:** Non-Conformance + Risk Manager  
**File:** `agents/05_ncr_risk_agent.md`

Input: Deviation / non-compliance / site failure  
Output: NCR document, severity classification, corrective action  
Decision: MINOR / MAJOR / CRITICAL

---

## 06 — REPORTING AGENT

**Role:** KPI + Analytics  
**File:** `agents/06_reporting_agent.md`

Input: All registers (submittal, NCR, inspection, test)  
Output: Weekly QA report, contractor scorecard, risk dashboard  

---

## Agent Decision Authority

| Agent | Can Decide Alone | Requires Human Review | Mandatory Sign-Off |
|-------|-----------------|----------------------|-------------------|
| Orchestrator | Routing, flagging | Conflict escalation | — |
| Spec Compliance | Compliance flag | Major deviations | — |
| Submittal Review | Minor approval | Conditional approval | Final approval |
| Document Generator | Draft generation | — | — |
| Site Inspection | Pre-check pass | Hold point release | Pour permit, structural |
| NCR & Risk | Draft NCR | NCR issuance | Critical NCR closure |
| Reporting | Report generation | — | — |

See `policies/approval_matrix.md` for full authority matrix.
