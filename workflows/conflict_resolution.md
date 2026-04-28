# WF-10 — Conflict Resolution Workflow

**Trigger:** Two or more agents produce conflicting decisions on the same item  
**Output:** Resolved decision or human escalation

---

## CONFLICT DETECTION

```
IF Agent_A.decision ≠ Agent_B.decision ON same item:
   → Step 1: Log conflict in output
   → Step 2: HOLD final decision (do NOT issue approval)
   → Step 3: Re-run both agents with additional context
   → Step 4: IF still conflict → Escalate to Human QA Lead
   → Step 5: Contractor notified: "Submission Under Review — Decision Pending"
```

## ESCALATION MATRIX

| Level | Conflict Type | Resolution | Authority |
|-------|--------------|------------|-----------|
| 1 | Minor discrepancy (format, wording) | Agent re-run with additional context | Orchestrator |
| 2 | Major conflict (technical disagreement) | Human QA Engineer review | QA Engineer |
| 3 | Critical or safety-related | QAQC Manager sign-off mandatory | QAQC Manager |

## CONFIDENCE-BASED ESCALATION

```
IF confidence < 70%:
   → Flag for human review regardless of decision
   → Add note: "LOW CONFIDENCE — Verify before proceeding"

IF confidence 70-85%:
   → Flag for QA Engineer review
   → Decision advisory only

IF confidence > 85%:
   → Decision may be issued (subject to approval matrix)
```

## RULES

1. **No approval issued while conflict is open**
2. All conflicts must be logged in conflict register
3. Conflict resolution time: max 48 hours
4. Contractor must be notified of hold status within 24 hours
5. Agent cannot self-resolve a conflict — escalation required
