# Approval Authority Matrix

## Decision Authority Levels

| Level | Description | Examples |
|-------|-------------|----------|
| AGENT | Fully automated, no human needed | Completeness check, draft generation, alerts |
| HUMAN REVIEW | Agent recommends, human confirms | Submittal approval, NCR issuance |
| MANDATORY SIGN-OFF | Agent cannot decide, human only | Pour permits, structural release, critical NCR |

---

## AGENT CAN DECIDE (no human required)

- Document completeness check (INCOMPLETE flag)
- Initial compliance flag (pass/fail per clause)
- Generating draft ITP/MS/NCR/QCP
- Schedule delay alerts and overdue flags
- Register updates (logging)
- Submittal status updates (A/B/C/D/I codes)
- Weekly report generation
- Conflict detection and logging

---

## HUMAN REVIEW REQUIRED (agent recommends, human confirms)

- Final submittal approval/rejection (Code A/B/C/D)
- NCR issuance (Minor and Major severity)
- Conditional approval with special clauses
- Submittal review comments issuance
- Inspection pre-check release (non-critical)
- Test result acceptance (non-structural)
- Material release after MIR (non-critical materials)

---

## MANDATORY HUMAN SIGN-OFF (agent cannot override)

- Concrete pour permit (any structural element)
- Structural element inspection release
- Waterproofing before concealment
- MEP before casting / closing walls
- Final acceptance / handover sign-off
- Critical NCR closure
- Any safety-related hold point release
- Mockup final approval (luxury projects)
- Fire rating compliance sign-off
- First delivery material acceptance (critical materials)

---

## OUTPUT FOOTER (mandatory for every agent output)

```
Decision Type:      [AGENT DECISION / REQUIRES HUMAN REVIEW / MANDATORY SIGN-OFF]
Action Required:    [e.g. QA Engineer to review and sign]
Hold Status:        [NONE / ACTIVE — execution cannot proceed]
Escalation Level:   [NONE / Level 1 / Level 2 / Level 3]
```

---

## Escalation Levels

| Level | Trigger | Response |
|-------|---------|----------|
| 0 | Normal operation | No escalation |
| 1 | Minor conflict or low confidence (<85%) | Agent re-run or QA Engineer flag |
| 2 | Major decision or conflicting agent outputs | QA Engineer review required |
| 3 | Critical/safety issue or Critical NCR | QAQC Manager sign-off mandatory |
