# Submittal Register

## Structure

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| submittal_id | string | Yes | Unique ID (e.g. S-STR-042) |
| submittal_type | enum | Yes | MAR / MS / ITP / SD / TR / QCP |
| work_item_id | string | Yes | Linked work item ID |
| contractor | string | Yes | Submitting contractor |
| discipline | enum | Yes | Architectural / Civil / MEP / Structural |
| title | string | Yes | Submittal title |
| revision | string | Yes | Rev A / B / C / ... |
| date_submitted | date | Yes | Date received |
| date_due | date | Yes | Required by (calculated from schedule_logic.md) |
| date_responded | date | No | Date of response |
| status_code | enum | Yes | A / B / C / D / I |
| status_text | string | Yes | Approved / Approved w/ Comments / Revise & Resubmit / Rejected / Incomplete |
| comments | array | No | Review comments |
| spec_refs | array | No | Referenced spec clauses |
| drawing_refs | array | No | Referenced drawings |
| overdue_days | integer | No | Days past due (calculated) |
| execution_impact | enum | No | None / At Risk / Delayed |
| linked_ncr_id | string | No | If rejection triggered NCR |
| previous_rev_id | string | No | Parent submittal ID (for revisions) |

## Status Codes

| Code | Meaning | Execution Allowed? |
|------|---------|-------------------|
| A | Approved | Yes |
| B | Approved with Comments | Yes (comments must be addressed) |
| C | Revise and Resubmit | No |
| D | Rejected | No |
| I | Incomplete | No (return to contractor) |
