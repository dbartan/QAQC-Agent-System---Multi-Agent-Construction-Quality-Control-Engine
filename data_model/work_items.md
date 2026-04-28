# Work Items Register

## Structure

Each work item represents a discrete scope of work requiring QAQC control.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| work_item_id | string | Yes | Unique ID (e.g. WI-SC-CON-001) |
| description | string | Yes | Work description |
| phase | enum | Yes | P1–P8 (see context/phases.md) |
| wbs_code | string | Yes | Work Breakdown Structure code |
| trade | enum | Yes | Civil / Structural / MEP / Architectural / Landscape |
| spec_section | string | Yes | CSI MasterFormat section |
| drawing_refs | array | Yes | Related drawing numbers |
| status | enum | Yes | Not Started / In Progress / Completed / On Hold |
| required_submittals | array | Yes | List of MAR/MS/ITP IDs |
| scheduled_start | date | Yes | Planned execution start |
| scheduled_end | date | Yes | Planned execution end |
| actual_start | date | No | Actual execution start |
| actual_end | date | No | Actual completion |
| quality_tier | enum | Yes | Standard / Premium / Luxury / Ultra-Luxury |
| mockup_required | boolean | Yes | Mockup needed before mass production |
| mockup_status | enum | No | Not Started / In Progress / Approved / Rejected |
| linked_ncrs | array | No | Related NCR IDs |
| linked_inspections | array | No | Related inspection IDs |
