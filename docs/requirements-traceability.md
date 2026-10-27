# Requirement coverage

Baseline: 2026-10-27. This mapping checks documentation coverage; it is not test execution or completion evidence. FR/AC definitions live in the [specification package](../_bmad-output/specs/spec-hbrand-inventory/SPEC.md); story definitions live in [epics](../_bmad-output/planning-artifacts/epics.md).

| Capability | Functional requirements | Backlog stories | Acceptance scenarios |
| --- | --- | --- | --- |
| CAP-1 | FR-1, FR-2 | 1.2 | AC-1, AC-2 |
| CAP-2 | FR-3, FR-4 | 1.3, 6.1 | AC-3, AC-4, AC-5 |
| CAP-3 | FR-5, FR-6 | 2.2, 2.3 | AC-6, AC-7, AC-8 |
| CAP-4 | FR-7, FR-8 | 2.1, 3.1 | AC-9, AC-10 |
| CAP-5 | FR-9, FR-10 | 3.2, 3.3 | AC-11, AC-12 |
| CAP-6 | FR-11, FR-12 | 4.1 | AC-13 |
| CAP-7 | FR-13, FR-14 | 4.2 | AC-14 |
| CAP-8 | FR-15, FR-16 | 4.3, 3.3 | AC-15 |
| CAP-9 | FR-17, FR-18 | 5.1, 5.2, 5.3 | AC-16, AC-17 |
| CAP-10 | FR-19, FR-20 | 6.1, 6.2 | AC-18 |
| CAP-11 | FR-21, FR-22 | 6.3, 7.3 | AC-19, AC-20 |
| CAP-12 | FR-23, FR-24 | 1.1, 7.1, 7.2 | AC-21 |
| CAP-13 | FR-25, FR-26 | 1.2, 2.3, 3.1, 3.3, 5.3, 7.2, 7.3 | AC-22 |

All NFR-1 through NFR-7 have verification routes in the acceptance companion: preservation AC-16/AC-17; repeat safety AC-8/AC-20/AC-21; bilingual quality AC-11/AC-12; resumability AC-21; account-state privacy AC-22; bounded scope/large-file processing AC-1 and the measured pilot; provenance AC-22.

## Owner-source preservation

| Source claim | Contract location |
| --- | --- |
| Local n8n and every intended Excel sheet | CAP-1/CAP-12; FR-1/FR-23 |
| Barcode uniqueness and existing/duplicate checks first | CAP-2; FR-3/FR-4 |
| One SKU across confirmed colours and sizes | CAP-3; FR-5/FR-6 |
| Separate mixed product and size values | CAP-4; FR-7 |
| Improved English/Arabic titles and full descriptions | CAP-5; FR-9/FR-10; content companion and preserved example |
| Compare Gemini/ChatGPT websites and review first outputs | CAP-6/CAP-8; FR-11/FR-12/FR-15 |
| Appropriate human model, requested views and style consistency | CAP-7; FR-13/FR-14 |
| Append outputs and missing required fields to same Drive workbook | CAP-9; FR-17/FR-18 |
| Owner login, browser fill and حفظ المنتج | CAP-10/CAP-11; FR-19/FR-21 |
| Saudi-riyal currency | Kernel constraint; data contract; FR-19 |
| Unanswered commercial price meaning | Q-01 and readiness R-1; no invented answer |
