---
title: HBrand Inventory Automation — Epic Backlog
status: draft
created: 2026-10-27
updated: 2026-10-27
inputDocuments:
  - ../specs/spec-hbrand-inventory/SPEC.md
  - prds/prd-N8N-HBrand-Inventory-2026-10-27/prd.md
  - architecture/architecture-N8N-HBrand-Inventory-2026-10-27/ARCHITECTURE-SPINE.md
---

# Epic and story backlog

All **21 stories are backlog**, not ready-for-dev or completed. The sequence is proposed and has no estimates or dates. Dependencies refer only to earlier work; each story produces a separately inspectable outcome. Unresolved inputs become explicit prerequisites rather than invented acceptance results. FR and AC definitions live in the [specification companions](../specs/spec-hbrand-inventory/SPEC.md).

## Requirements inventory

FR-1 through FR-26 and NFR-1 through NFR-7 are covered by the stories below. The [coverage map](../../docs/requirements-traceability.md) links each capability and FR pair to stories and acceptance scenarios. Visual behaviour inherits the existing host surfaces; proposed review interactions are recorded in EXPERIENCE.md.

## Epic list

1. Auditable source catalogue and duplicate investigation.
2. Correct product families and normalized variants.
3. Useful English and Arabic catalogue content.
4. Reviewed, consistent human-model photography.
5. Source-preserving workbook enrichment.
6. Verified inventory entry and save reconciliation.
7. Resumable local end-to-end operation.

## Epic 1: Auditable source catalogue and duplicate investigation

Goal: the owner can inspect source coverage and duplicate issues before enrichment.

### Story 1.1: Establish the local orchestration and source-access foundation

As the owner, I want the selected local runtime and its own Drive connection documented and running, so source access does not depend on an open chat session.

**Requirements:** FR-23, FR-24. **Dependencies:** none. **Prerequisites:** Q-12 installation choice; owner sign-in/configuration for the selected connection.

**Acceptance Criteria:** Given the selected environment, when local n8n is installed and restarted, then its configured workflows/state persist and an explicit read-only Drive access check works; credentials are not exposed. Given no runtime has yet been installed, documentation must not mark this story done.

### Story 1.2: Inventory and extract workbook rows and original images

As the owner, I want a complete scoped manifest and attributable row/image observations, so missing tabs or blank image-preview cells do not hide products.

**Requirements:** FR-1, FR-2, FR-25. **Dependencies:** 1.1. **Prerequisites:** Q-15 scope/exclusions recorded.

**Acceptance Criteria:** Given paginated files and multiple worksheets, when discovery/extraction runs, then every intended item is accounted for with explicit errors/exclusions and original image anchors; verify AC-1/AC-2. Large file processing is bounded and measured.

### Story 1.3: Investigate barcodes and existing inventory before enrichment

As the owner, I want repeated/invalid barcodes and target matches flagged first, so import never double-counts an unresolved source observation.

**Requirements:** FR-3, FR-4, FR-26. **Dependencies:** 1.2. **Prerequisites:** Q-05 lookup capability inspected; Q-06/Q-14 needed for any existing-record update.

**Acceptance Criteria:** Given source repeats, target exact/conflicting matches or partial lookup, when checks run, then outcomes follow the data contract and no uncertain record creates/updates stock; verify AC-3/AC-4/AC-5. Read-only inventory lookup can be delivered independently of create-form automation.

## Epic 2: Correct product families and normalized variants

Goal: the owner can recognize a design across colours/sizes without merging different garments.

### Story 2.1: Separate mixed attributes and expose unsupported facts

As the owner, I want product names, colours and sizes separated with original values retained, so malformed text does not corrupt inventory variants.

**Requirements:** FR-7, FR-8. **Dependencies:** 1.2, 1.3. **Prerequisites:** Q-11 for ambiguous supplier codes.

**Acceptance Criteria:** Given mixed letter/numeric/age suffixes and missing physical facts, when normalization runs, then supported fields split correctly, raw text survives and ambiguous facts remain blocked; verify AC-9/AC-10.

### Story 2.2: Establish design identity across colours and sizes

As the owner, I want garment evidence to establish family membership, so generic names or nearby rows do not collapse different designs.

**Requirements:** FR-5, FR-6. **Dependencies:** 2.1.

**Acceptance Criteria:** Given the same design in different colours plus a same-name/different-print counterexample, when grouping proposes membership, then confirmed matches share a family and distinct designs stay separate; only observed colour/size pairs are retained. Verify AC-6/AC-7; uncertain matches expose original evidence.

### Story 2.3: Persist family identity and one parent SKU

As the owner, I want known families and their original variants remembered, so row movement or title correction does not create another product.

**Requirements:** FR-5, FR-6, FR-25. **Dependencies:** 2.2.

**Acceptance Criteria:** Given established families, when sources repeat/reorder or wording improves, then parent SKU remains stable and barcodes/source facts remain attributable; an existing parent with a new barcode is routed separately from parent creation. Verify AC-8.

## Epic 3: Useful English and Arabic catalogue content

Goal: the owner obtains readable bilingual copy from one supported fact record.

### Story 3.1: Establish canonical facts and commercial field meanings

As the owner, I want explicit required facts and price semantics, so an unknown cost cannot silently become a selling price.

**Requirements:** FR-8, FR-25. **Dependencies:** 2.1, 2.3. **Prerequisites:** Q-01/Q-02 for live-ready factual completion.

**Acceptance Criteria:** Given supplied and missing facts, when the fact record is built, then every value has provenance, currency is SAR, unknown price kind/weight blocks the affected live action, and proposed editorial details remain distinct from facts. Verify AC-10/AC-12.

### Story 3.2: Generate bilingual titles and complete descriptions

As the owner, I want improved English/Arabic titles and full structured descriptions, so the catalogue communicates the product consistently.

**Requirements:** FR-9, FR-10. **Dependencies:** 3.1.

**Acceptance Criteria:** Given canonical facts and confirmed family membership, when copy is generated, then both languages follow the owner's example and correctly distinguish family versus colour-specific scope; no unsupported material/care/fit claim is added. Verify AC-11/AC-12.

### Story 3.3: Correct facts and maintain translation parity

As the owner, I want a correction to remain consistent in both languages and downstream assets, so stale copy does not survive a source change.

**Requirements:** FR-10, FR-16, FR-25, FR-26. **Dependencies:** 3.2.

**Acceptance Criteria:** Given a corrected audience, size or colour, when the fact revision changes, then affected language outputs and image inputs are flagged/regenerated/rechecked and prior acceptance is not silently reused. Verify AC-11/AC-15/AC-22.

## Epic 4: Reviewed, consistent human-model photography

Goal: the owner can compare providers and obtain faithful colourway galleries.

### Story 4.1: Compare the available provider browser routes

As the owner, I want the same real products tested in Gemini and ChatGPT, so provider selection rests on my actual garments.

**Requirements:** FR-11, FR-12. **Dependencies:** 2.3, 3.1. **Prerequisites:** Q-07 account access and displayed model availability.

**Acceptance Criteria:** Given owner-authenticated websites, when equivalent requests are submitted, then all attempts/downloads/retries and actual model labels are retained and owner-reviewed comparison reasons are recorded. Verify AC-13. Account/API equivalence is not assumed.

### Story 4.2: Produce consistent galleries for confirmed colourways

As the owner, I want front/back/side photos with an appropriate model and stable treatment, so each colour looks like the same product family.

**Requirements:** FR-13, FR-14. **Dependencies:** 4.1, 3.2.

**Acceptance Criteria:** Given actual source colourway references, when a gallery is generated, then garment details match, views stay consistent and only confirmed colours appear; one accepted colour gallery can serve its sizes. Verify AC-14. Missing-view interpretations stay reviewable.

### Story 4.3: Review, correct and accept specific image revisions

As the owner, I want to reject or correct the first images, so accepted assets reflect my feedback.

**Requirements:** FR-15, FR-16. **Dependencies:** 4.2. **Prerequisites:** Q-08 for later unattended acceptance policy.

**Acceptance Criteria:** Given initial outputs, when review is pending or a version is rejected/changed, then it cannot be used as accepted imagery; a recorded verdict binds the exact relevant versions and scope. Verify AC-15.

## Epic 5: Source-preserving workbook enrichment

Goal: the owner can inspect enriched columns in the original Drive workbook without losing supplier data or photos.

### Story 5.1: Verify preservation on a workbook copy

As the owner, I want an enriched copy checked first, so the writer's limitations do not destroy embedded pictures or formulas.

**Requirements:** FR-17, FR-18. **Dependencies:** 3.3, 4.3. **Prerequisites:** Q-10 final image-column representation.

**Acceptance Criteria:** Given the original image-bearing file, when enrichment is staged, then source cells, formulas, tab structure, media/drawing relationships and relevant formatting are compared and preserved. Verify AC-16 before same-file mutation.

### Story 5.2: Protect same-file write-back against conflicts

As the owner, I want edits/sorts detected and protected, so enrichment does not overwrite my concurrent changes.

**Requirements:** FR-18, FR-24. **Dependencies:** 5.1. **Prerequisites:** Q-09 supported conditional write or enforced exclusive editing window.

**Acceptance Criteria:** Given a competing source change, when write-back runs, then the guarded operation preserves the human edit or blocks; a read-before-write race is not accepted. Automation revisions are distinguished from supplier changes. Verify AC-17.

### Story 5.3: Publish and read back enriched source columns

As the owner, I want SKU, copy, image references and results aligned with original rows, so the source workbook becomes a usable catalogue record.

**Requirements:** FR-17, FR-18, FR-25. **Dependencies:** 5.2.

**Acceptance Criteria:** Given a guarded current source, when the same Drive file is enriched, then intended fields and image references read back correctly, source identity is retained and the operation revision is recorded. Verify AC-16/AC-17/AC-22.

## Epic 6: Verified inventory entry and save reconciliation

Goal: the owner can find the exact intended product and variants after browser entry.

### Story 6.1: Establish the authenticated destination mapping

As the owner, I want actual SKU/image/language/variant controls and business selections inspected, so screenshot assumptions do not determine live payloads.

**Requirements:** FR-4, FR-19, FR-20. **Dependencies:** 1.3, 3.1. **Prerequisites:** Q-03/Q-04/Q-05; Q-01/Q-02 for affected payload facts.

**Acceptance Criteria:** Given owner login, when the live form/lookup is inspected without creating products, then selectors/limits/lookup coverage and the selected warehouse/taxonomy are recorded; unsupported requirements are explicit blockers. Verify AC-18.

### Story 6.2: Populate exact product and observed variant values

As the owner, I want a complete prepared form, so every size/colour barcode, quantity, SAR selling price and accepted gallery is attached correctly.

**Requirements:** FR-19, FR-20. **Dependencies:** 5.3, 6.1.

**Acceptance Criteria:** Given a current complete payload, when browser fill completes, then form read-back matches the intended family and only its observed variants; missing facts or changed controls block Save. Verify AC-18 before submission.

### Story 6.3: Save once and reconcile the actual outcome

As the owner, I want verified results and safe recovery from a lost response, so rerunning does not add product or stock twice.

**Requirements:** FR-21, FR-22. **Dependencies:** 6.2.

**Acceptance Criteria:** Given durable reservations and SUBMITTING before Save, when the outcome is normal or interrupted, then fresh navigation verifies all intended target values or retains IMPORT_UNKNOWN; concurrent/resumed jobs cannot blindly repeat the final action. Verify AC-19/AC-20.

## Epic 7: Resumable local end-to-end operation

Goal: the owner can run and recover the complete workflow without losing review or external-effect evidence.

### Story 7.1: Coordinate the full local n8n workflow

As the owner, I want source-to-inventory stages connected under local n8n, so the process runs independently of this discussion.

**Requirements:** FR-23, FR-24. **Dependencies:** 1.1 and Epics 2–6.

**Acceptance Criteria:** Given the selected runtime, when a bounded job starts, then stage state/identity references persist, review/login pauses resume correctly and completed effects are not repeated. Verify AC-21.

### Story 7.2: Expose issues and prove restart/concurrency recovery

As the owner, I want actionable recovery records, so I can resume a session or inspect an unknown save safely.

**Requirements:** FR-24, FR-25, FR-26. **Dependencies:** 7.1.

**Acceptance Criteria:** Given expiration, worker loss, restart and parallel attempts, when recovery runs, then reservations/version checks preserve correctness and each issue states the affected scope and evidence needed; no secrets appear in logs. Verify AC-20/AC-21/AC-22.

### Story 7.3: Demonstrate the pilot and assess wider operation

As the owner, I want a complete multi-colour/multi-size demonstration and representative checks, so rollout decisions are supported by actual results.

**Requirements:** FR-22, FR-25, FR-26 and acceptance coverage for all capabilities. **Dependencies:** 7.2. **Prerequisites:** relevant Q-01 through Q-15 resolved or explicitly scoped out with reason; Q-13 measured limits for wider operation.

**Acceptance Criteria:** Given the established pilot, when the complete path and repeat/interruption cases run, then source enrichment and actual target values are verified without duplicates. Record all AC outcomes separately; unresolved representative cases or missing scale/review policy remain rollout blockers rather than a claimed release.
