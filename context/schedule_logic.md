# Schedule Logic — Lead Time & Tracking Rules

## Lead Time Rules

| Submittal Type | Required Before Execution | Review Period | Total Lead Time |
|---------------|-------------------------|---------------|-----------------|
| Material Submittal (MAR) | 28 days | 14 days | 42 days |
| Method Statement (MS) | 21 days | 14 days | 35 days |
| Shop Drawing | 28 days | 21 days | 49 days |
| ITP | 14 days | 7 days | 21 days |
| Test Reports | Same day as test | — | N/A |

## Submittal Due Date Calculation

```
Submittal_Due = Execution_Start - Review_Period - Procurement_Lead_Time

Example:
  Execution Start: 2024-06-01
  Review Period: 14 days (MAR)
  Procurement Lead: 28 days
  Submittal Due: 2024-04-15
```

## Daily Tracking Logic

```
FOR each open submittal:
  IF today > due_date AND status ≠ Submitted:
     Flag: OVERDUE
     Calculate: days overdue
     Assess: execution impact (YES/NO)
     Notify: [Contractor + QA Lead]

  IF today = due_date - 7:
     Flag: AT RISK
     Notify: [Contractor]
```

## Weekly Summary Output

```
Weekly Submittal Status:
- Total open submittals: X
- Overdue: X (list with days overdue)
- At risk (due in 7 days): X
- Critical path impact: [list affected work items]
```

## Escalation Timeline

| Overdue Duration | Action |
|-----------------|--------|
| 1-7 days | Contractor reminder (automated) |
| 8-14 days | Escalation to PM + QA Lead |
| 15-21 days | Formal notice + schedule impact assessment |
| >21 days | Contractual notice trigger |
