# QAQC System — Master Workflow Index

---

## WORKFLOW LIST

| ID | Workflow | File | Trigger |
|----|---------|------|---------|
| WF-01 | Material Approval (MAR) | workflows/material_approval_workflow.md | Contractor submits MAR |
| WF-02 | Method Statement Review | workflows/method_statement_workflow.md | Contractor submits MS |
| WF-03 | Shop Drawing Review | workflows/submittal_review_workflow.md | Contractor submits SD |
| WF-04 | ITP Generation | workflows/itp_generation_workflow.md | New work item starts |
| WF-05 | Site Inspection | workflows/inspection_workflow.md | Inspection request received |
| WF-06 | NCR Lifecycle | workflows/ncr_workflow.md | Non-conformance detected |
| WF-07 | Mockup Approval | workflows/mockup_approval_workflow.md | Mockup ready for review |
| WF-08 | Test Management | workflows/test_workflow.md | Test scheduled or report received |
| WF-09 | Handover / Snagging | workflows/handover_workflow.md | Phase completion or final handover |

---

## MASTER ROUTING LOGIC

```
INPUT RECEIVED
    ↓
    Is it a SUBMITTAL?
        → MAR  → WF-01
        → MS   → WF-02
        → SD   → WF-03
        → ITP / QCP → Document Agent review
    
    Is it a NEW WORK ITEM?
        → Document Agent (MS + ITP + QCP generation)
    
    Is it a SITE ISSUE / OBSERVATION?
        → WF-06 (NCR) + WF-05 (Inspection follow-up)
    
    Is it a TEST?
        → WF-08
    
    Is it a MOCKUP?
        → WF-07
    
    Is it a REPORT REQUEST?
        → Reporting Agent
```

---

## QUICK REFERENCE: REQUIRED DOCS PER SUBMITTAL TYPE

### MAR — Material Approval Request
Required documents in package:
- [ ] MAR form (completed, signed by contractor)
- [ ] Product data sheet (manufacturer)
- [ ] Compliance statement vs spec
- [ ] Test certificates / third-party test reports
- [ ] Sample (physical or photos)
- [ ] Country of origin declaration
- [ ] ISO / quality certification of manufacturer
- [ ] Previously approved submittals for same material (if revision)

### MS — Method Statement
Required:
- [ ] Scope of work
- [ ] Reference drawings (rev and date)
- [ ] Materials list (all with valid MAR references)
- [ ] Equipment list
- [ ] Step-by-step execution sequence
- [ ] QA/QC controls (what, who, when, how)
- [ ] Hold points and witness points identified
- [ ] Safety and environmental controls
- [ ] Risk assessment

### Shop Drawing
Required:
- [ ] Drawing number, revision, date
- [ ] Reference specification section
- [ ] Material callouts with MAR numbers
- [ ] Dimensions, tolerances
- [ ] Connection details
- [ ] Deviation cloud (if differs from design intent)
- [ ] Contractor engineer stamp (if required)

### ITP — Inspection Test Plan
Required:
- [ ] Work item and WBS code
- [ ] Reference specification
- [ ] All inspection stages
- [ ] Type for each stage (H / W / R)
- [ ] Responsibility matrix (Contractor / QA / Consultant)
- [ ] Acceptance criteria for each stage
- [ ] Test frequency and method
- [ ] Record format reference

### Test Report
Required:
- [ ] Test date, location, reference number
- [ ] Specification requirement (what value is required)
- [ ] Test result (actual value)
- [ ] Pass / Fail status
- [ ] Test lab accreditation reference
- [ ] Witness confirmation (QA signature)
- [ ] Equipment calibration certificate ref
