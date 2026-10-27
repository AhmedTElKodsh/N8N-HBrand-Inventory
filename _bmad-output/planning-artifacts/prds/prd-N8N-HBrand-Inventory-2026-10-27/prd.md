---
title: HBrand Inventory Automation — PRD
status: draft
created: 2026-10-27
updated: 2026-10-27
sources:
  - ../../../specs/spec-hbrand-inventory/SPEC.md
---

# Product requirements document

## Purpose and vision

This PRD organizes the recorded requirements for the owner and implementers. The [specification and companions](../../../specs/spec-hbrand-inventory/SPEC.md) own the full contract. FR identifiers below refer to the definitions in [requirements.md](../../../specs/spec-hbrand-inventory/requirements.md); this document groups them rather than creating another requirement set. Technical mechanisms belong in the architecture.

The product converts supplier Excel records and original garment pictures into grouped, bilingual, photographically usable inventory products. It reduces repeated manual work while preserving variant identity and stock accuracy. The first route uses local n8n, Drive/Excel, image-provider websites and the existing inventory browser form.

## Target user and jobs

The owner is the initial operator. They need to identify duplicate records first, recognize designs across colours/sizes, produce customer-facing English/Arabic copy and appropriate human-model photography, review first outputs, and trust that source enrichment and inventory entry match the original facts. Additional operator roles or a consumer-facing interface have not been defined.

### UJ-1 — Owner reviews a new product family

From selected source workbooks, the system shows flagged duplicates and candidate family evidence, separates supported attributes and drafts bilingual content. The owner resolves a genuinely ambiguous family and reviews the first provider images with correction feedback. The usable result is a confirmed family with accepted assets and complete factual inputs. This journey is distilled from the discussion; the exact review UI is a proposal.

### UJ-2 — Owner completes and checks an import

After owner login and verified prerequisites, the workflow enriches the same workbook, fills the inventory form and saves. Fresh navigation confirms the product and exact variants. A lost response produces an actionable unknown state rather than a second Save. This is intended behaviour, not an executed acceptance result.

## Glossary

| Term | Meaning |
| --- | --- |
| Source row | One original product/variant record with one barcode and source provenance. |
| Product family | One confirmed garment design across colours and sizes. |
| Parent SKU | Persistent unified code for a product family; distinct from each original barcode. |
| Colourway | Confirmed colour specification within a product family, including multi-colour garments. |
| Variant | An observed colourway/size combination retaining its original barcode and source facts. |
| Gallery | Versioned front/back/side image set for a confirmed colourway. |
| Verified import | A saved target record whose actual values and variants were checked through fresh navigation. |

## Features

### Source discovery and duplicate investigation

FR-1/FR-2 require complete scoped enumeration and cell/image extraction. FR-3/FR-4 require a barcode check and source/import/inventory duplicate investigation before enrichment. Partial target lookup cannot establish absence. These requirements support UJ-1 and prevent treating dated repeated observations as additive stock.

### Product identity and normalized attributes

FR-5/FR-6 establish one stable family SKU across confirmed colours/sizes while keeping different designs separate. FR-7/FR-8 separate mixed values and preserve missing or ambiguous facts. Only observed pairs are created; source sizes, barcodes, amounts and quantities remain attributable.

### English and Arabic content

FR-9/FR-10 require useful titles and full descriptions in both languages. Original source facts underpin copy; parent and colour-specific wording remain correctly scoped. Description sections follow the owner's example, including cautious care wording when instructions are unavailable. Generated photographs never establish new product facts.

### Provider comparison and consistent imagery

FR-11/FR-12 compare actual available Gemini and ChatGPT browser routes on the same references. FR-13/FR-14 require faithful human-model photographs with the requested views and consistency across colours. FR-15/FR-16 support the owner's initial review, corrections, version-bound acceptance and the unresolved later review policy. These realize the image-review part of UJ-1.

### Same-workbook enrichment

FR-17/FR-18 append the intended generated/required fields to the same Drive file, preserve original Excel content and drawings, prevent lost edits, and verify the updated file. Image-link storage is a proposal pending Q-10. Source updates must not cause a self-triggering import loop.

### Browser entry, save and verification

FR-19/FR-20 use actual authenticated target controls and known required facts. FR-21/FR-22 persist the submission operation and establish the real saved outcome before retrying. The correct warehouse and source price meaning are prerequisites. These realize UJ-2.

### Local orchestration and evidence

FR-23/FR-24 coordinate the full process in local n8n with persistent pauses/recovery. FR-25/FR-26 expose provenance and actionable issues without exposing account secrets. A running chat session is not the deployed automation engine, and this conversation's connected account is not a configured local credential.

## Quality requirements

NFR-1 through NFR-7 cover source/stock preservation, repeat-safe identity and external effects, bilingual parity, resumable operation, private credentials, bounded large-file processing, and inspectable evidence. Definitions are in the [requirements companion](../../../specs/spec-hbrand-inventory/requirements.md). No numerical SLA, processing-rate target, confidence threshold or correction budget has been approved.

## Scope and non-goals

The intended initial release includes all thirteen capabilities. A single-family pilot is a validation stage, not a reduction of the ultimate folder-wide objective. Website rebuilds, a customer storefront, guessed facts, automatic quantity aggregation, hidden repricing, and an unbenchmarked model winner are outside the recorded scope. API-based automation can be reconsidered later without weakening identity and verification rules.

## Success measures

- **SM-1:** The source-confirmed pilot family appears once in inventory with the exact observed variants and verified SAR amounts, quantities, copy and assets. Validates FR-5/FR-6 and FR-17 through FR-22.
- **SM-2:** The owner can review, correct and accept the first generated gallery with matching bilingual content and traceable original evidence. Validates FR-9 through FR-16.
- **SM-3:** Reprocessing and interrupted-save recovery do not create duplicate product/stock effects. Validates FR-3/FR-4 and FR-21 through FR-26.
- **Counter-metric:** Do not optimize row throughput or automatic acceptance by merging uncertain designs, skipping duplicate checks, fabricating missing facts, or hiding retries. Those would invalidate the success measures.

These are acceptance goals, not measured current results. The complete [acceptance suite](../../../specs/spec-hbrand-inventory/acceptance.md) adds representative failure and scale cases.

## Open questions and assumptions

All Q-01 through Q-15 remain indexed in the [decision register](../../../../docs/decisions-and-open-questions.md). Price meaning, required facts, actual target controls/lookup and write-back concurrency block the corresponding live paths. Proposed deployment, worker/ledger mechanism, review surfaces, image-link layout and rollout shape remain assumptions. The document is a discussion-derived draft ready for review and targeted discovery, not a declaration that implementation or live rollout is ready.
