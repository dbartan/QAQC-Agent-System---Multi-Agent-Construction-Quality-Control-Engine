# QAQC System — Master Rules

> These rules are absolute. No agent overrides them.

---

## R-01 — NO ASSUMPTION RULE
If any required information is missing, flag as INCOMPLETE.
Never fill gaps with assumptions.
Always state: "Missing: [item]. Required before proceeding."

## R-02 — CLAUSE REFERENCE RULE
Every compliance decision must reference a specific spec clause or standard clause.
Format: [Spec Section XX.XX.XX] or [ASTM CXXX / BS XXXX]
Output without clause reference is invalid.

## R-03 — SEQUENCE RULE
No work proceeds without:
- Approved MAR (material on site)
- Approved MS (method approved)
- Approved ITP (inspection plan in place)
If any is missing — FLAG. Do not approve execution start.

## R-04 — HOLD POINT RULE
Hold Points (H) are absolute.
Work CANNOT proceed past a hold point without physical sign-off.
Agent cannot clear a hold point. Human QA sign-off mandatory.

## R-05 — TEST FAILURE RULE
Any failed test result — immediate NCR generation.
Work in affected area — SUSPENDED until NCR closed.
Contractor cannot self-certify re-test without QA supervision.

## R-06 — CONFLICT RULE
If two agents produce conflicting decisions:
- HOLD all output
- Escalate to Human QA Lead
- Log conflict in register
- No approval issued while conflict is open

## R-07 — RESUBMISSION RULE
Every resubmission must include:
- Revision cloud on changed items
- Response matrix addressing each previous comment
- Revision number updated
Resubmission without response to previous comments = return without review.

## R-08 — CRITICAL NCR RULE
Critical NCR — immediate escalation to QAQC Manager
- Stop work instruction issued
- Cannot be closed without root cause analysis + corrective action verification

## R-09 — TRACEABILITY RULE
Every output must carry:
- Submittal ID or NCR ID or Inspection ID
- Phase + WBS code
- Spec reference
- Drawing reference (if applicable)
- Date
- Status

## R-10 — DRAFT RULE
All agent-generated documents carry status: DRAFT
DRAFT documents are NOT valid for execution.
Human review + approval required before status changes to ISSUED FOR CONSTRUCTION.

## R-11 — MOCKUP RULE (Luxury Projects)
No mass production / bulk installation without:
- Workshop sample approved
- Site mockup approved
- All approving parties signed off (Consultant + Client + Brand Rep if applicable)

## R-12 — MATERIAL ON SITE RULE
No material installed without:
- Valid approved MAR
- MIR (Material Inspection Report) confirming delivery matches approval
- Storage condition check

## R-13 — OVERDUE SUBMITTAL RULE
Submittal overdue by >7 days — automatic flag + contractor notification
Overdue by >14 days — escalation to PM + potential schedule impact assessment
Overdue by >21 days — formal letter / contractual notice trigger

## R-14 — STANDARD HIERARCHY RULE
If project spec is more stringent than standard — apply spec
If standard is more stringent than spec — flag, apply standard, notify consultant via RFI
Never apply the less stringent requirement without documented consultant approval

## R-15 — LEARNING CAPTURE RULE
After project completion or phase handover:
- Best-performing ITP, MS, QCP — saved to data/past_projects/approved/
- Lessons learned — documented in data/past_projects/lessons_learned/
- NCR patterns — analyzed for next project risk pre-loading
