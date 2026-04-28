# WF-01 — Material Approval Workflow (MAR)

**Trigger:** Contractor submits Material Approval Request  
**Output:** Approved / Conditional / Revise / Rejected MAR

---

## STAGE 1 — COMPLETENESS CHECK

Agent: Orchestrator + Submittal Review Agent

Check all required documents are present:
- MAR form complete and signed
- Product data sheet
- Compliance statement vs spec
- Test certificates
- Sample reference
- Manufacturer certification

```
IF any document missing:
 STATUS: INCOMPLETE (Code I)
 Return to contractor with missing items list
 Do NOT proceed to technical review
 Log in submittal register: Status = I, reason listed
```

---

## STAGE 2 — SPEC COMPLIANCE CHECK

Agent: Spec Compliance Agent

1. Identify applicable spec section via spec_index.md
2. Load parsed spec clauses
3. Compare each technical requirement:
   - Material type / grade / standard
   - Physical properties (strength, density, thermal, acoustic etc.)
   - Chemical properties (if applicable)
   - Dimensional requirements
   - Surface finish requirements
   - Country of origin (if restricted)
4. Check test certificates vs required test standards
5. Check test certificate dates (validity)
6. Check third-party lab accreditation

**Output:** Compliance matrix

| Spec Clause | Requirement | Submitted | Status | Comment |
|-------------|------------|----------|--------|---------|
| XX.XX.XX | Min 35 MPa | 40 MPa | PASS | |
| XX.XX.XX | ASTM C150 Type I | Submitted | PASS | |
| XX.XX.XX | Max w/c 0.45 | Not stated | FAIL | Missing |

---

## STAGE 3 — TECHNICAL REVIEW

Agent: Submittal Review Agent

1. Review product data sheet in detail
2. Verify manufacturer's stated properties match test results
3. Check if equal/substitute is proposed (spec may not allow substitution)
4. If substitution: check OR EQUAL clause in spec
5. Check compatibility with adjacent / interface materials
6. Cross-reference with approved shop drawings

---

## STAGE 4 — DECISION

Agent: Orchestrator (collects Stage 2 + 3 outputs)

```
ALL clauses PASS + complete docs:
 → CODE A — APPROVED
 → Proceed with procurement / delivery

MINOR deviations (cosmetic / administrative only):
 → CODE B — APPROVED WITH COMMENTS
 → Proceed + address comments before installation

1 or more MAJOR deviation:
 → CODE C — REVISE AND RESUBMIT
 → Do not procure
 → Issue comment sheet

CRITICAL deviation or fundamental spec non-compliance:
 → CODE D — REJECTED
 → Issue rejection letter with full reasoning
 → NCR raised if material already on site
```

---

## STAGE 5 — LOGGING

Update submittal_register.md:
- Status code (A/B/C/D/I)
- Date received
- Date responded
- Review duration
- Comments summary
- Next action

---

## STAGE 6 — DELIVERY INSPECTION (MIR)

When material arrives on site:
1. Trigger MIR (Material Inspection Report)
2. Check delivered material matches approved MAR:
   - Brand, model, grade
   - Batch/lot numbers
   - Quantity vs delivery note
   - Packaging condition
   - Storage requirements
3. Check delivery documents (COC — Certificate of Conformance)
4. Physical condition inspection
5. If matches → release for storage/use
6. If does not match → quarantine + NCR

**Hold Rule:** Material cannot be installed until MIR completed and signed.

---

## RESPONSE TIMELINE

| Action | Target Days |
|--------|------------|
| Completeness check | Day 1 |
| Spec compliance review | Days 2–5 |
| Technical review | Days 6–10 |
| Decision + response | Day 12 |
| Total review period | 14 days (standard contract) |

---

## ESCALATION

| Condition | Action |
|-----------|--------|
| No response within 14 days | Contractor reminder |
| No response within 21 days | Formal notice to PM |
| Revise & Resubmit not received by deadline | Schedule impact flag |
| Material on site without approved MAR | Quarantine + NCR |
