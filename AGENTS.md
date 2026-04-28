# QAQC Agent System — Agent Definitions

---

## AGENT MAP

```
ORCHESTRATOR (L0 — Brain)
    │
    ├── L1 CORE AGENTS
    │   ├── Spec Compliance Agent
    │   ├── Submittal Review Agent
    │   ├── Document Generator Agent
    │   ├── Inspection Agent
    │   ├── NCR & Risk Agent
    │   ├── Schedule Agent
    │   └── Reporting Agent
    │
    └── L2 SUPPORT AGENTS
        ├── Spec Parser Agent
        └── Installation Checklist Agent
```

---

## ORCHESTRATOR AGENT

**Role:** QAQC System Brain  
**File:** agents/orchestrator.md

**Responsibilities:**
- Receive all inputs (submittals, site issues, new work items, queries)
- Detect: phase, WBS code, input type
- Route to correct agent(s)
- Collect agent outputs
- Detect conflicts between agent decisions
- Apply human gate rules
- Issue final decision or escalate

**Decision Logic:**
```
INPUT TYPE ROUTING:
- MAR / Material Submittal     → Spec Agent + Submittal Agent
- Method Statement             → Spec Agent + Submittal Agent + Document Agent
- ITP / QCP                    → Document Agent + Spec Agent
- Shop Drawing                 → Submittal Agent + Spec Agent
- Site Issue / Observation     → Inspection Agent + NCR Agent
- New Work Item                → Document Agent (MS + ITP + QCP)
- Test Report                  → Submittal Agent + NCR Agent (if fail)
- Schedule Query               → Schedule Agent
- Reporting Request            → Reporting Agent
```

**Conflict Rule:**
```
IF Agent_A.decision ≠ Agent_B.decision ON same item:
   → HOLD output
   → Log conflict
   → Flag: HUMAN REVIEW REQUIRED
   → No approval issued
```

---

## SPEC COMPLIANCE AGENT

**Role:** Specification & Standard Validator  
**File:** agents/spec_compliance_agent.md  
**Skill:** skills/spec_compliance_check.md

**Input:**
- Contractor submission (MAR / MS / test report)
- Parsed specification (from data/specs/parsed/)
- Applicable standards (ASTM / BS / EN / ISO)
- QMP / QCP

**Process:**
1. Identify applicable spec section via spec_index.md
2. Load relevant parsed spec clauses
3. Compare submission against each clause
4. Flag deviations with severity
5. Check standard references cited by contractor

**Output:**
- Compliance matrix (clause by clause)
- Deviation list with severity
- Missing document list
- Risk flag
- Recommended action: Approve / Conditional / Reject

**Rules:**
- Never assume. Missing data = flag as INCOMPLETE
- Always reference spec clause number
- Cross-check contractor's cited standards against project spec
- If spec clause is ambiguous → flag for RFI, do not assume

---

## SUBMITTAL REVIEW AGENT

**Role:** Technical Reviewer  
**File:** agents/submittal_review_agent.md  
**Skill:** skills/review_submittal.md

**Input:**
- Submittal package (MAR / MS / ITP / Shop Drawing)
- Compliance matrix from Spec Agent
- Previous revision comments (if resubmission)

**Process:**
1. Check completeness (all required docs present?)
2. Validate technical content
3. Review test certificates and their validity
4. Check revision cloud / response to previous comments (resubmissions)
5. Cross-reference with approved drawings

**Output:**
- Status: APPROVED / APPROVED WITH COMMENTS / REVISE & RESUBMIT / REJECTED
- Technical comment list (clause-referenced)
- Required actions list
- Missing documents list
- Revision response check result

**Approval Codes:**
```
A  = Approved → proceed
B  = Approved with comments → proceed, address comments
C  = Revise and resubmit → do not proceed
D  = Rejected → fundamental non-compliance
```

---

## DOCUMENT GENERATOR AGENT

**Role:** QAQC Document Producer  
**File:** agents/document_generator_agent.md  
**Skills:** skills/generate_ms.md, skills/generate_itp.md, skills/generate_qcp.md, skills/generate_ncr.md

**Input:**
- Work item description
- Applicable spec section
- Phase and WBS code
- Material type / trade

**Produces:**
- Method Statement (MS)
- Inspection Test Plan (ITP)
- Quality Control Plan (QCP)
- Material Approval Request (MAR) draft
- Non-Conformance Report (NCR)
- Inspection Checklist

**Rules:**
- Always base on approved template from /templates/
- Always reference spec clause in every section
- Hold points (H) require mandatory human sign-off
- Witness points (W) require QA presence
- Draft docs carry status: DRAFT — NOT FOR EXECUTION until approved

---

## INSPECTION AGENT

**Role:** Site QAQC Validator  
**File:** agents/inspection_agent.md  
**Skill:** skills/inspection_checklist.md

**Input:**
- Work type / trade
- Phase / WBS code
- Approved ITP for the work item
- Previous inspection records

**Process:**
1. Load relevant ITP
2. Generate pre-inspection checklist
3. Verify pre-conditions (prior work approved, materials approved, MS approved)
4. List all inspection stages with type (H/W/R)
5. Flag open items from previous inspection

**Output:**
- Pre-inspection checklist
- Stage-by-stage inspection record
- Observations list
- NCR trigger (if deviation found)
- Sign-off sheet

**Inspection Types:**
```
H = HOLD POINT — work cannot proceed without QA/Consultant sign-off
W = WITNESS POINT — QA must be present, can proceed if not available (after notice)
R = REVIEW POINT — document review only, no site attendance required
```

---

## NCR & RISK AGENT

**Role:** Non-Conformance and Risk Manager  
**File:** agents/ncr_risk_agent.md  
**Skill:** skills/generate_ncr.md

**Input:**
- Non-conformance description
- Inspection observation
- Failed test report
- Spec deviation from Compliance Agent

**Process:**
1. Classify severity (Minor / Major / Critical)
2. Identify root cause category
3. Generate NCR with full traceability
4. Assign corrective action deadline
5. Update NCR register
6. Trigger escalation if Critical

**Severity Classification:**
```
CRITICAL:
- Structural integrity risk
- Safety hazard
- Waterproofing failure
- Fire system non-compliance
→ STOP WORK on affected area. Immediate escalation.

MAJOR:
- Spec deviation affecting performance
- Material substitution without approval
- Failed pressure / strength test
- Missing approved MS before execution
→ REJECT. Corrective action mandatory before proceeding.

MINOR:
- Documentation gap (minor)
- Cosmetic deviation within tolerance
- Administrative non-compliance
→ CONDITIONAL. Address before final inspection.
```

**Output:**
- NCR document (from template)
- Severity classification
- Root cause category
- Corrective action required
- Closure deadline
- NCR register entry

---

## SCHEDULE AGENT

**Role:** Submittal & Inspection Schedule Tracker  
**File:** agents/schedule_agent.md

**Input:**
- Submittal register
- Execution program (planned start dates)
- Lead time rules from context/schedule_logic.md

**Process:**
1. Calculate required submittal dates from execution start
2. Track actual submission vs required
3. Flag overdue items
4. Assess execution impact
5. Generate overdue report

**Lead Time Rules:**
```
Material Submittal (MAR):     Submit 28 days before installation
Method Statement (MS):        Submit 21 days before work start
Shop Drawing:                 Submit 28 days before fabrication
ITP:                          Submit 14 days before first inspection
Test Reports:                 Submit same day as test
```

---

## REPORTING AGENT

**Role:** KPI, Analytics, Weekly Report  
**File:** agents/reporting_agent.md  
**Skill:** skills/reporting.md

**Input:**
- Submittal register (current status)
- NCR register (open / closed)
- Inspection register
- Test register

**Output:**
- Weekly QA Summary Report
- Contractor performance score
- NCR trend analysis
- Open items dashboard
- Risk heatmap by phase/trade

---

## SPEC PARSER AGENT (Support)

**Role:** Specification Pre-Processor  
**File:** agents/spec_parser_agent.md

**Input:** Raw specification PDF / document  
**Output:** Structured markdown in data/specs/parsed/

**This agent requires human validation before output is used.**

---

## INSTALLATION CHECKLIST AGENT (Support)

**Role:** Trade-Specific Checklist Generator  
**File:** agents/installation_checklist_agent.md  
**Skill:** skills/inspection_checklist.md

**Input:** Trade / work type  
**Output:** Pre-installation, during-installation, post-installation checklist
