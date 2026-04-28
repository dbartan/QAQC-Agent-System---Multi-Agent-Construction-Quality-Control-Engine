# NCR Register

## Structure

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| ncr_id | string | Yes | Unique ID (e.g. NCR-STR-001) |
| work_item_id | string | Yes | Linked work item |
| phase | enum | Yes | P1–P8 |
| severity | enum | Yes | CRITICAL / MAJOR / MINOR |
| category | enum | Yes | Structural / MEP / Finishes / Waterproofing / Fire / Safety / Documentation |
| description | string | Yes | Non-conformance description |
| spec_clause_ref | string | Yes | Violated spec clause |
| raised_by | string | Yes | Inspector/Agent name |
| date_raised | date | Yes | Date NCR opened |
| status | enum | Yes | Open / Under Corrective Action / Closed / Rejected |
| root_cause | string | No | Determined root cause |
| corrective_action | string | No | Required corrective action |
| responsible_party | string | Yes | Contractor responsible for fix |
| due_date | date | Yes | Deadline for corrective action |
| date_closed | date | No | Date NCR closed |
| closed_by | string | No | Person who verified closure |
| reinspection_id | string | No | Linked re-inspection ID |
| escalation_level | enum | No | NONE / Level 1 / Level 2 / Level 3 |
| linked_submittal_id | string | No | Related submittal if applicable |

## NCR Lifecycle

```
RAISED → UNDER CORRECTIVE ACTION → CORRECTIVE ACTION COMPLETE → 
  REINSPECTION → CLOSED (if pass) / REOPENED (if fail)
```
