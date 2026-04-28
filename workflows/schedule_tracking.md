# WF-11 — Schedule Tracking Workflow

**Trigger:** Daily automated check / Manual query  
**Output:** Overdue report, risk assessment, weekly summary

---

## DAILY CHECK

```
FOR each open submittal in submittal_register.md:
  IF today > due_date AND status ≠ Submitted:
     Flag: OVERDUE
     Calculate: days overdue
     Assess: execution impact (YES/NO)
     IF days overdue > 7:
        Notify: [Contractor + QA Lead]
     IF days overdue > 14:
        Escalate: PM notification
     IF days overdue > 21:
        Trigger: Contractual notice
```

## EXECUTION IMPACT ASSESSMENT

```
IF submittal overdue:
  Check: Is this item on critical path?
  Check: Is procurement lead time affected?
  Check: Are dependent work items delayed?
  
  IF YES to any → Flag: POTENTIAL DELAY
  Calculate: estimated delay in days
  Report: affected downstream activities
```

## WEEKLY SUMMARY

```
Week of: [DD-MMM-YYYY]

Total Open Submittals: X
  - Approved: X
  - Under Review: X
  - Overdue: X (list with days)
  - At Risk (due in 7 days): X

Critical Path Impact:
  - [Work item] — [delay in days] — [affected trades]

Top 5 Overdue:
  1. [ID] — [Type] — [X days overdue] — [Contractor]
  2. ...
```
