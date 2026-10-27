---
id: SPEC-hbrand-inventory
status: draft
created: 2026-10-27
updated: 2026-10-27
companions:
  - requirements.md
  - data-contracts.md
  - content-and-imagery.md
  - acceptance.md
  - ../../../docs/decisions-and-open-questions.md
  - ../../planning-artifacts/architecture/architecture-N8N-HBrand-Inventory-2026-10-27/ARCHITECTURE-SPINE.md
  - ../../planning-artifacts/ux-designs/ux-N8N-HBrand-Inventory-2026-10-27/DESIGN.md
  - ../../planning-artifacts/ux-designs/ux-N8N-HBrand-Inventory-2026-10-27/EXPERIENCE.md
sources:
  - ../../../docs/references/bilingual-copy-example.md
---

# HBrand Inventory Automation Specification

This kernel and its listed companions are the requirements contract. It is derived from the append-only specification memlog and the recorded discussion. **Draft** means unresolved business inputs and proposed architecture remain; it does not negate the explicitly confirmed owner requirements. See the [decision register](../../../docs/decisions-and-open-questions.md) for authority and question owners.

## Why

The owner needs to turn inconsistent Excel product lists and low-quality garment photographs into usable inventory records without manually rewriting, grouping, photographing, and entering every variant. The system must recognize one design across colours and sizes, preserve the original variant barcodes and stock facts, produce bilingual product copy and reviewed model imagery, enrich the source workbook, and coordinate reliable browser entry through a local n8n engine.

## Capabilities

- **CAP-1**
  - **intent:** Discover and read the intended source workbooks, worksheets, rows, and original product pictures.
  - **success:** A complete scoped manifest accounts for every file and tab, and each extracted row and picture can be traced to its source; unreadable or excluded items are reported.
- **CAP-2**
  - **intent:** Identify invalid or repeated barcodes and establish whether each variant already exists before enrichment or creation.
  - **success:** A complete versioned source-barcode index precedes clearance; missing/multiple barcodes and source/inventory duplicates are flagged, and uncertain lookup cannot authorize creation or stock mutation.
- **CAP-3**
  - **intent:** Represent one confirmed design with one stable parent SKU across its colours and observed size variants.
  - **success:** A multi-colour/multi-size family receives one persistent SKU, retains its original variant barcodes, and stays separate from a different design with similar wording.
- **CAP-4**
  - **intent:** Separate product names, sizes, colours, and other attributes without losing source facts.
  - **success:** Merged text is split into attributable fields; ambiguous codes and missing facts stay visible; original values and observed colour/size relationships remain intact.
- **CAP-5**
  - **intent:** Provide improved English/Arabic titles and complete descriptions grounded in original product evidence.
  - **success:** Both languages describe the same product facts, follow the owner's structure, and contain no unsupported composition, measurement, care, or performance claims.
- **CAP-6**
  - **intent:** Establish which available Gemini or ChatGPT image route best serves the actual source garments.
  - **success:** The same reference products and requirements are compared, outputs/retries are retained, and the owner's review records the selection and its scope; no untested winner is asserted.
- **CAP-7**
  - **intent:** Produce faithful human-model product galleries with front, back, and side views and consistent styling across confirmed colours.
  - **success:** Accepted outputs preserve garment identity, observed colours and prints, use an appropriate model, and provide the agreed views without generating nonexistent variants.
- **CAP-8**
  - **intent:** Let the owner review first images, request corrections, and resolve uncertain product evidence.
  - **success:** The first image set pauses for review, rejected assets stay unusable, revisions retain their history, and approval remains tied to the reviewed assets or an explicitly defined later policy.
- **CAP-9**
  - **intent:** Add enriched fields to the same Drive workbook while retaining its existing information and pictures.
  - **success:** A verified same-file update adds the intended columns, preserves original data/drawings/layout, and avoids replacing concurrent human edits.
- **CAP-10**
  - **intent:** Enter complete products and observed variants through the owner's authenticated inventory browser form.
  - **success:** Verified target controls receive the intended bilingual values, SAR amounts, pictures, barcodes, and stock/warehouse values; missing required facts block the affected import.
- **CAP-11**
  - **intent:** Save each intended inventory product once and establish the actual outcome before retrying.
  - **success:** Fresh navigation verifies the saved record and variant details; interrupted or uncertain saves are reconciled without blindly repeating the final action.
- **CAP-12**
  - **intent:** Coordinate the complete process locally with resumable progress, login pauses, and review pauses.
  - **success:** A pilot completes under local n8n, survives a tested pause/restart, and resumes from persisted state without duplicate generation, write-back, or inventory creation.
- **CAP-13**
  - **intent:** Make source evidence, grouping decisions, content/image versions, unresolved issues, and external outcomes inspectable.
  - **success:** Each accepted output and import result has a source/revision trail, and each blocked/unknown outcome states the evidence needed to resolve it without exposing credentials.

## Constraints

- Use the specified Drive folder and local n8n; the initial image-provider and inventory routes are browser-based, with owner login.
- Every source row must have one barcode. Duplicate investigation comes first; repeated rows do not define an add/replace stock policy.
- One parent SKU identifies a confirmed design across colours and sizes. Original variant barcodes stay distinct from parent SKU.
- Similar barcodes, nearby rows, or generic product text alone are insufficient to merge designs.
- Currency is **SAR / ر.س**. The source price's commercial meaning is unresolved and must not be invented.
- English and Arabic titles/descriptions are required; original source information and photos are the factual basis.
- Preserve the same source workbook's existing content and embedded pictures when adding fields.
- The owner reviews the first generated images and can direct corrections. Later acceptance scope remains an open policy decision.
- Required factual fields and actual destination controls must be established before live save; a screenshot is not a verified integration schema.
- Documented plans, local fixtures, and optimistic browser messages do not establish live acceptance.

## Non-goals

- Rebuilding the inventory website or providing a new customer storefront.
- Replacing the requested local engine with a cloud-only orchestrator in the initial release.
- Treating a missing API as permission to invent an API contract or account entitlement.
- Automatically inventing product facts, sizes, colours, barcodes, stock aggregation, or missing required measurements.
- Selecting a universal image-model winner without a product-specific comparison.
- Completing runtime installation, account login, source mutation, or inventory publication as part of this documentation task.

## Success signal

The owner can inspect one source-confirmed design with multiple colours and sizes, review its bilingual content and first human-model images, then find the correctly saved product and exact variants in inventory with matching same-workbook enrichment. Re-running the same source and recovering a deliberately interrupted save must not create another product or duplicate stock. Wider release additionally requires the representative scenarios in [acceptance](acceptance.md), not just that first demonstration.

## Assumptions

- Proposed architecture uses a separate local worker and durable ledger; Docker, SQLite, image-link storage, and review of ambiguous groups are recommendations rather than approved stack/policy choices.
- The owner is the initial operator. Additional roles, a custom review application, schedules, and numeric service targets are not established.
- A suitable multi-colour/multi-size pilot family will be selected from inspected source evidence; none has been approved yet.

## Open Questions

- Q-01/Q-02: price meaning and missing required physical facts.
- Q-03/Q-04/Q-05: authenticated target fields, taxonomy, warehouse, and complete existence lookup.
- Q-06/Q-14: duplicate resolution and source stock semantics.
- Q-07/Q-08: provider benchmark and later image-review policy.
- Q-09/Q-10/Q-11: write-back permissions/concurrency, image columns, ambiguous size codes.
- Q-12/Q-13/Q-15: runtime, scale/retention/schedule, and final source exclusions.

Question wording, owners, and blocking effects are recorded in the [register](../../../docs/decisions-and-open-questions.md).
