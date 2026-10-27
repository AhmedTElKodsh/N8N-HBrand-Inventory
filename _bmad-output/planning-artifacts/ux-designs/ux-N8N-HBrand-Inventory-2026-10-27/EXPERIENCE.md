---
title: HBrand Inventory Automation — Operator Experience
status: draft
created: 2026-10-27
updated: 2026-10-27
sources:
  - ../../../specs/spec-hbrand-inventory/SPEC.md
---

# Operator experience

## Foundation

The initial operator is the owner using local n8n and authenticated desktop browser surfaces. [DESIGN.md](DESIGN.md) owns visual boundaries; inherited text is referenced by `{typography.body.note}`. Review may use a suitable existing n8n/browser surface; a custom review app is not selected. Proposed interactions below describe required information and behaviour, not already implemented screens.

## Information Architecture

| Surface / information view | Existing or proposed | Operator purpose |
| --- | --- | --- |
| Source/issue manifest | Proposed workflow output | See processed, excluded, failed and pending files/tabs/rows. |
| Duplicate and grouping evidence | Proposed review view | Compare exact barcode matches and original garment evidence before a merge/create decision. |
| Bilingual content | Proposed review view | Inspect equivalent titles/descriptions and correct unsupported/missing facts. |
| Provider image comparison | Existing provider websites plus proposed comparison record | Review the first generated outputs and direct corrections. |
| Login handoff | Existing provider/inventory login pages | Let the owner authenticate without pasting credentials into content or logs. |
| Enriched source workbook | Existing Drive/Excel file | Inspect added fields alongside original supplier data/pictures. |
| Saved inventory record / unknown outcome | Existing inventory plus proposed job record | Establish actual external outcome and recover without duplicate stock. |

## Voice and Tone

Product copy follows the owner's bilingual example. Operator messages name the affected file/row/family and a concrete action, for example “Weight is required for this product; enter the measured value” or “This barcode already exists; inspect the linked record.” Avoid declaring success until verification finishes. Distinguish “generated”, “reviewed”, “submitted”, “verified”, and “unknown”.

## Component Patterns

Image review shows original references, provider/model as displayed, requested view, output revision and approve/reject/request-changes actions. Grouping review shows raw and normalized attributes, candidate relationships and observable garment evidence. Content correction changes canonical facts or clearly editorial text; affected translations/assets are regenerated or rechecked. A review result is bound to a particular job and revision, not merely a product title.

## State Patterns

Use the shared states in the [data contract](../../../specs/spec-hbrand-inventory/data-contracts.md). Login/review pauses preserve work. A blocked fact states the missing input. IMPORT_UNKNOWN exposes the last possible side effect and the evidence needed to reconcile it; its primary action is inspection/reconciliation, not another Save.

An absence of owner response is still pending. A source or output change invalidates affected acceptance. An accepted pilot photo set is not an unspecified catalogue-wide review policy.

## Interaction Primitives

- Select a bounded source scope and inspect its manifest.
- Inspect a duplicate or group proposal, retain separate designs, or record an evidence-backed resolution.
- Correct product facts and inspect both languages together.
- Review the first provider outputs, request corrections, and accept a specific version.
- Complete sign-in in the actual account surface, then resume the waiting job.
- Inspect enriched source data and freshly reopened inventory records.
- Reconcile uncertain operations using preserved target/source evidence; never repeat an uncertain save merely to clear an issue.

These actions are proposed interaction requirements. Exact controls, navigation and notification channels remain implementation choices.

## Accessibility Floor

For any review controls the project authors, provide keyboard access, visible focus, readable labels, a textual state and correct Arabic/English direction isolation. Barcodes and size codes remain intact in mixed-direction text. A third-party page's accessibility has not been audited; browser automation must not hide a required control or depend on a colour cue alone.

## Key Flows

### UJ-1 — Owner establishes a usable product family

1. The owner identifies the source scope; the workflow lists files/tabs and flags invalid/repeated barcodes before enrichment.
2. The owner is shown any uncertain family proposal with original pictures and row evidence. Similar wording is not sufficient to accept it.
3. Confirmed family facts produce improved English/Arabic copy and provider comparison inputs.
4. The owner signs into the chosen provider website when needed and reviews the first generated images, requesting corrections as necessary.
5. **Value delivered:** one specific family has established identity, known factual fields, usable bilingual content and accepted image evidence.

Failure paths: missing physical facts, ambiguous size codes, different prints hidden behind the same title, provider failure, or an unreviewed missing-back interpretation remain actionable issues.

### UJ-2 — Owner obtains and verifies a saved product

1. The workflow verifies source preservation on a copy and safely enriches the same Drive file.
2. The owner signs into inventory; the verified mapping fills known product/variant fields and the intended images.
3. The operation is durably recorded before حفظ المنتج.
4. Fresh navigation inspects the saved record, exact variants, SAR values, warehouse and gallery.
5. **Value delivered:** a linked verified inventory record and matching source enrichment, with enough evidence to rerun safely.

Failure path: a lost browser response after Save leaves an unknown result. Resumption first checks the actual target record; another submission is unavailable until the ambiguity is resolved.

## Surface and mock coverage

All seven information views above participate in UJ-1 or UJ-2. Inventory general/variant forms have supplied screenshot references in [source evidence](../../../../docs/source-evidence.md). Other views are spine-only proposed interactions. No custom mocks, new palette, notification channel or mobile interface is implied by this documentation pass.

## Open items

Actual target controls and language rendering are Q-03; existence lookup Q-05; later review policy Q-08; model/account availability Q-07; schedule and notifications Q-13. Resolve these through evidence or owner direction rather than inventing finished screen specifications.
