# Detailed requirements

Companion to [SPEC.md](SPEC.md). Owner-confirmed requirements and the minimum engineering consequences are distinguished from proposed operational choices. FR identifiers are stable; the PRD groups these requirements without redefining them.

## Functional requirements

| ID | Capability | Requirement and observable consequence |
| --- | --- | --- |
| FR-1 | CAP-1 | Enumerate the complete intended Drive scope with pagination and worksheet discovery; a bounded first listing must not be treated as the folder total. Preserve a manifest of processed, skipped, excluded, and failed items. |
| FR-2 | CAP-1 | Extract native Excel cell information and embedded image relationships. Preserve raw headers, original values, file identity/revision, worksheet, row location, and image anchors. |
| FR-3 | CAP-2 | Require one barcode value per product row. Complete a versioned index of the selected source scope before clearing any barcode; partial/unreadable scope remains unresolved. Blank, ambiguous, or repeated barcodes flag before expensive enrichment; retain barcode text without invented padding or digits. |
| FR-4 | CAP-2 | Check source duplicates, previous imports, and actual inventory existence. Match outcomes are existing exact variant, duplicate source, conflict, confirmed absent, or unresolved; unresolved lookup cannot justify create/update. |
| FR-5 | CAP-3 | Assign one persistent parent SKU to a confirmed design across its colours and sizes. Reprocessing, row reordering, or title corrections must reuse the known identity. |
| FR-6 | CAP-3 | Use original garment evidence and source attributes to distinguish styles. Barcode similarity and row proximity rank candidates but do not authorize a merge. Keep only observed colour/size variants; preserve their barcodes, prices, and quantities. |
| FR-7 | CAP-4 | Parse combined product/size text into separate fields while preserving the original. Support inconsistent headers, attached size suffixes, numeric sizes, letter sizes, and supplier age codes subject to verified meanings. |
| FR-8 | CAP-4 | Identify required but unsupported facts and conflicting source values. Preserve blank-versus-zero and source price meaning; do not fill weights, dimensions, quantities, or commercial prices by guess. |
| FR-9 | CAP-5 | Generate improved English and Arabic product titles, plus colour-specific titles where needed, using equivalent product identity and confirmed audience/attributes. |
| FR-10 | CAP-5 | Generate full English and Arabic descriptions with introduction, product details, styling, sizes/fit, and care. Preserve language parity and distinguish factual statements from styling suggestions. |
| FR-11 | CAP-6 | Submit the same real reference products and equivalent generation requirements to the available Gemini and ChatGPT browser routes; record provider/model as actually shown, inputs, prompt revision, outputs, time, failures and retries. |
| FR-12 | CAP-6 | Let owner feedback determine the initial selection. Compare garment fidelity, consistency, realism, usable resolution, operational effort, and account limits; do not convert documentation claims into a measured ranking. |
| FR-13 | CAP-7 | Generate photorealistic men/women/children appropriate to confirmed product audience, wearing the referenced garment in front/back/side views with faithful prints, construction, colour, and proportions. |
| FR-14 | CAP-7 | Keep style, model and photography consistent across confirmed colour versions. Proposed optimization: reuse one colour gallery across its sizes. Unknown source views remain interpretations requiring review rather than verified garment facts. |
| FR-15 | CAP-8 | Pause for the owner's first generated-image review; support approval, rejection, and requested correction while retaining the preceding versions and feedback. |
| FR-16 | CAP-8 | Record what evidence and versions were reviewed. Supplier-fact/original-image, garment, prompt and output changes invalidate affected acceptance; automation-only physical file revisions do not. Later automatic-versus-manual review policy must be established before unattended use. |
| FR-17 | CAP-9 | Append enriched values to the same Drive file, aligned to source row identity, preserving original sheets, values, formulas, images/drawings, and relevant layout. Generated image columns may use links subject to Q-10. |
| FR-18 | CAP-9 | Back up and verify the proposed update on a copy, coordinate source revisions/edits, and read back the final file. Track physical Drive revisions separately from supplier facts and original-image associations; automation enrichment neither self-triggers nor hides a real supplier change. |
| FR-19 | CAP-10 | Use owner-authenticated browser sessions to populate verified product/variant fields, selected categories/brands/warehouse, bilingual copy, SAR amounts, source quantities/barcodes, and intended images. |
| FR-20 | CAP-10 | Inspect live controls and constraints before binding mapping. A missing SKU field, unsupported variant shape, missing weight, inaccessible image control, or ambiguous price blocks the affected live import and records why. |
| FR-21 | CAP-11 | Persist submission identity and state before clicking حفظ المنتج. Prevent concurrent/repeated creation, including other inventory writers through verified target uniqueness/idempotency or an enforced exclusive writing window; local locks alone are insufficient. |
| FR-22 | CAP-11 | Verify the saved product through fresh navigation, including target identity, variants, prices/quantities/barcodes and images. Fence stale workers; a negative lookup alone cannot exclude a delayed server commit. Uncertain saves remain unknown without resubmission until definitive evidence or verified target guarantees establish a safe outcome. |
| FR-23 | CAP-12 | A local n8n workflow coordinates discovery, duplicate checks, grouping, copy, imagery/review, source write-back, inventory entry, and verification. The local installation receives its own configured integration credentials. |
| FR-24 | CAP-12 | Persist progress and pause for login, owner review, changed layouts, missing facts, and uncertain outcomes. Resume after restart without repeating completed external effects; batch and scheduling policies remain proposed until measured/selected. |
| FR-25 | CAP-13 | Retain source references, raw/normalized values, family decisions and observable evidence, content/prompt/asset versions, feedback, target identifiers, and verification outcomes. |
| FR-26 | CAP-13 | Show actionable unresolved/failed/unknown states and distinguish documented intent, local checks, browser execution, and verified live results. Keep account credentials and authentication state out of documentation/Git/log output. |

## Non-functional requirements

| ID | Requirement | Evidence needed |
| --- | --- | --- |
| NFR-1 | Preserve original source records, source-to-image alignment, and external stock integrity. | Workbook preservation comparison, duplicate cases, read-back checks. |
| NFR-2 | Stable identities and repeat-safe external operations across process interruption. | Restart, parallel-run, duplicate-save and unknown-save recovery scenarios. |
| NFR-3 | English/Arabic content is readable, equivalent, and correctly scoped to parent/colour/size. | Bilingual human review and canonical-fact comparison. |
| NFR-4 | Local operation survives human pauses and makes uncertainty visible. | Persisted pause/resume and actionable issue demonstrations. |
| NFR-5 | Protect credentials/session state; obtain them through the selected application's intended local sign-in/configuration flow. | Private storage/config inspection without revealing secret values. |
| NFR-6 | Bound workbook and image processing rather than loading the folder into one large execution. | Measured large-file pilot; no throughput or latency target is agreed yet. |
| NFR-7 | Retain the evidence needed to explain a grouping, asset acceptance, write-back, or import outcome. | Provenance records and retained revision references; retention period remains Q-13. |

## Source and target scope

The source is [Drive folder 1whVWEjIICuwnTSpgTtYTV4RZviUUWtnX](https://drive.google.com/drive/folders/1whVWEjIICuwnTSpgTtYTV4RZviUUWtnX). The target create page is [inventorysuite.neurix.uk/products/new](https://inventorysuite.neurix.uk/products/new), with the final action حفظ المنتج. Complete enumeration includes all intended workbook tabs and reports unsupported/hidden/excluded items; final exclusions and recursive folder policy are Q-15. Existing catalogue records are inspected for duplication; their deletion, repricing, or stock mutation is not implied by a create workflow and requires the unresolved Q-06/Q-14 policy.

Required image views include front, back, and sides. Whether the final gallery requires distinct left and right files is confirmed during the pilot, without dropping the required side coverage. No batch can substitute generic high-quality imagery for the actual supplied garment.
