# Test & Inspection Register

## Structure

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| inspection_id | string | Yes | Unique ID (e.g. INS-FIN-001) |
| work_item_id | string | Yes | Linked work item |
| itp_ref | string | Yes | ITP document reference |
| mir_ref | string | No | MIR reference (if material inspection) |
| inspection_type | enum | Yes | Pre-Installation / In-Process / Post-Installation / Final |
| stage_type | enum | Yes | H (Hold) / W (Witness) / R (Review) / M (Monitor) |
| phase | enum | Yes | P1–P8 |
| location | string | Yes | Zone / level / grid reference |
| date | date | Yes | Inspection date |
| result | enum | Yes | PASS / FAIL / CONDITIONAL / PUNCH LIST |
| failed_items | array | No | List of failed check items |
| ncr_raised | boolean | No | NCR triggered? |
| ncr_id | string | No | Linked NCR if raised |
| reinspection_required | boolean | No | Follow-up needed? |
| reinspection_date | date | No | Scheduled re-inspection |
| inspector | string | Yes | QA/QC Engineer name |
| contractor_rep | string | No | Contractor representative present |
| photos_taken | boolean | No | Photo evidence attached |
| photo_ref | string | No | Photo log reference |
