# Acceptance scenarios

Companion to [SPEC.md](SPEC.md). These are required checks and demonstrations, **not executed results**. Use representative original-source evidence and controlled duplicates; avoid modifying live stock to run a synthetic test unless separately authorized for that pilot.

| ID | Capability | Scenario and expected evidence |
| --- | --- | --- |
| AC-1 | CAP-1 | Enumerate a scope larger than one provider page and a workbook with multiple tabs. The manifest accounts for every intended item and explicit exclusion/error; the first 100 results are not a completion claim. |
| AC-2 | CAP-1 | Extract original Excel images, including one media asset reused across size rows. Verify the front/back/row associations against the workbook rather than assuming blank image cells mean no pictures. |
| AC-3 | CAP-2 | Supply blank, multiple and text-preserved barcodes, including a leading-zero case. Invalid rows flag before enrichment and valid identifiers retain their exact meaning. |
| AC-4 | CAP-2 | Repeat a barcode within a sheet and across dated files, including a duplicate in the last discovered workbook. No row clears until the selected manifest's barcode index is complete/versioned; partial scope remains unresolved. Flag affected observations and do not add or replace stock automatically. |
| AC-5 | CAP-2 | Lookup an exact existing variant, a conflicting barcode and an unavailable/partial search. Link the existing record, flag the conflict and block creation on uncertainty. |
| AC-6 | CAP-3 | Establish one real multi-colour/multi-size design. Assign one stable SKU and only the observed pairs; retain each original barcode/quantity/price. |
| AC-7 | CAP-3 | Present distinct designs with the same normalized title, brand, colour and size, including the documented CANADA example. Keep them separate; barcode prefix and row proximity alone cannot override different garment details. |
| AC-8 | CAP-3 | Reorder source rows and improve a product title. Previously established families and SKUs remain stable; new barcodes belonging to an existing family do not create another parent. |
| AC-9 | CAP-4 | Parse attached suffixes, letter/numeric sizes and ambiguous infant/child codes. Preserve raw text, split supported fields correctly and flag meanings that lack evidence. |
| AC-10 | CAP-4 | Remove a required weight, leave price kind unknown or introduce conflicting source facts. The affected live save is blocked with an actionable issue, rather than guessed values or a healthy zero. |
| AC-11 | CAP-5 | Review English/Arabic parent and colour-specific titles plus all description sections. Both languages share the facts, preserve brand/audience/size meaning and avoid unobserved colour-size claims. |
| AC-12 | CAP-5 | Give low-detail source photos and no composition/care label. Generated copy avoids unsupported material/performance/washing claims, while styling advice stays clearly editorial. |
| AC-13 | CAP-6 | Compare both available browser image routes on identical real references and equivalent requirements. Retain all attempts, exact model labels/prompts, actual downloaded files and the owner's selection reasons. |
| AC-14 | CAP-7 | Generate front/back/side views and a second confirmed colourway. Check garment print, structure and colour against sources and model/style consistency across views; do not accept an attractive but different garment. |
| AC-15 | CAP-8 | Reject the first output, request a correction, then approve a specific revision. The rejected asset stays unusable, history is retained and only the reviewed scope is accepted. Changed inputs/assets invalidate affected acceptance. |
| AC-16 | CAP-9 | Add fields to an image-bearing workbook copy, then the same Drive file through the approved write mechanism. Compare source cells/formulas/tabs, media/drawings/anchors, layout and appended values after read-back. |
| AC-17 | CAP-9 | Sort/edit a row or change the Drive revision during write-back. A conditional write or enforced exclusive window prevents lost edits. Track physical and supplier-content revisions separately: own enrichment neither endlessly reimports nor invalidates unchanged approvals, while real source/image changes are detected. |
| AC-18 | CAP-10 | Inspect the authenticated target form, field limits, SKU/image controls and lookup completeness. With known SAR selling-price mapping, physical facts, category/brand and warehouse, populate exactly the intended product and variants. |
| AC-19 | CAP-11 | Save the pilot and reopen it through fresh navigation. Verify target identity, bilingual content, every original barcode, observed colour/size, quantity, price, warehouse and gallery. |
| AC-20 | CAP-11 | Interrupt after Save may have reached the server, delay its commit and temporarily return a negative lookup. Fence stale workers, retain SUBMITTING/unknown and its reservation, and do not resubmit without definitive outcome evidence or verified target guarantees. |
| AC-21 | CAP-12 | Pause for login/review, expire a session, restart n8n/worker and run concurrent automation plus human/external creation attempts. Persisted state/reservations cover local jobs; verified target uniqueness/idempotency or an enforced exclusive writing window covers other writers. |
| AC-22 | CAP-13 | Trace one imported value/asset and one blocked/unknown issue to original rows/images, transformations, reviewed revisions and verification evidence. Logs/repository contain no credentials or reusable session state. |

## Pilot acceptance

1. Select and confirm a real family spanning multiple colours and sizes; record its exact source revisions and original images.
2. Resolve the pilot's price meaning, required facts, target controls, warehouse, lookup and write-back method.
3. Run duplicate/grouping checks and bilingual copy review; compare the first provider outputs and record owner-directed corrections.
4. Verify source preservation on a copy, then same-file enrichment using the established concurrency controls.
5. Execute the live import once and verify by fresh navigation, retaining target identity and evidence.
6. Re-run the same source and test an interruption without creating duplicate products, variants or stock.

A successful pilot establishes that narrow route. Broader acceptance additionally covers representative garment types, ambiguous rows, large workbooks, genuine duplicate conflicts, colour/size gaps, and operator recovery. No percentage accuracy, throughput, correction budget or unattended review policy has been agreed; measure and select those rather than inventing a release threshold.
