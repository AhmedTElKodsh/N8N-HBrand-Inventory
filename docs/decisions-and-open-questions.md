# Decisions and open questions

Baseline: 2026-10-27. This register records authority and uncertainty. The specification memlog records the same decisions for derivation; resolving a question requires an appended decision and a specification refresh.

## Confirmed by the owner

| ID | Decision | Source |
| --- | --- | --- |
| DEC-01 | A locally installed n8n engine orchestrates the complete import/enrichment workflow. | Initial requirements |
| DEC-02 | Process the Excel sheets in the specified Drive folder. | Initial requirements |
| DEC-03 | Every source row must have one barcode. Duplicate barcodes must be flagged; checking for an existing product or duplicate record is the first action. | Barcode clarification |
| DEC-04 | One confirmed design has one parent SKU across colours, each with its observed size variants. | Colour/SKU clarification |
| DEC-05 | Detecting design identity across colours/sizes is central; image evidence, barcode similarity, and nearby rows may help. These clues are not universally present. | Colour/SKU clarification |
| DEC-06 | Use original product information and pictures to improve titles and write full descriptions in English and Arabic. | Bilingual content requirement |
| DEC-07 | Generate photorealistic human models appropriate to the product audience, with front, back, and side views; aim for consistent style across colour versions. | Initial requirements and colour clarification |
| DEC-08 | Initially use Gemini/ChatGPT websites through the browser, compare results, and let the owner review and correct the first generated images. | Initial requirements |
| DEC-09 | Append the SKU, generated image references, and other required fields to the same Drive workbook. | Initial requirements |
| DEC-10 | Initially use the inventory browser form; the owner signs in and the automation fills the product and clicks حفظ المنتج. | Initial requirements |
| DEC-11 | The currency is Saudi riyals, SAR / ر.س. | Explicit currency answer |
| DEC-12 | Document the discussion and create the project and BMad documentation baseline. | Documentation request |

## Engineering proposals, not owner-approved selections

| ID | Proposal | Reason / revisit condition |
| --- | --- | --- |
| PROP-01 | Local n8n plus a separate browser/workbook worker and durable import ledger. | Isolates browser lifetime and large workbooks; verify during implementation design. |
| PROP-02 | Docker for local n8n; SQLite for a single-machine worker ledger. | Suggested operational starting point; versions and actual installation remain deferred. |
| PROP-03 | Review ambiguous grouping proposals with source-photo evidence; remember resolved families. | Prevents generic descriptions from collapsing distinct designs. |
| PROP-04 | Generate one image set per confirmed colour and reuse it across sizes. | Preserves consistency and limits repeated generation. |
| PROP-05 | Separate parent titles from colour-specific variant titles; preserve four primary bilingual title/description fields. | A parent spanning several colours should not be titled as one colour only. |
| PROP-06 | Store generated image files in Drive and append durable links to the workbook. | Avoids further inflating already large files; confirm link-versus-embedding preference in Q-10. |
| PROP-07 | Start with one multi-colour, multi-size family, then a representative set before a wider run. | Exercises the difficult grouping rule before scale. |
| PROP-08 | Use original source facts, never generated imagery, as the basis for factual copy. | Avoids amplifying hallucinated garment details. |
| PROP-09 | Never blindly repeat a possibly successful save; reconcile it by fresh inventory navigation. | Prevents duplicate products and opening-stock entries. |

## Open questions

| ID | Question / missing evidence | Owner | Blocks |
| --- | --- | --- | --- |
| Q-01 | Is السعر the final selling price, purchase cost, or another value? Is it tax-inclusive? | Owner | Filling the live variant price |
| Q-02 | What real weight should be used when absent? Which dimensions are required by the live form? | Owner / inventory inspection | Saving rows missing required facts |
| Q-03 | Where does the website accept parent SKU, variant barcodes, product images, and both descriptions? What are the current constraints? | Inventory inspection | Final target mapping |
| Q-04 | Which warehouse, categories, and brand records should be used? WH-001 is visible but is not a confirmed selection. | Owner / inventory inspection | Live stock placement and category mapping |
| Q-05 | Can inventory lookup reliably prove existing variants/parents, including hidden records and pagination? What target uniqueness/idempotency guarantees or enforceable exclusive writing window can cover other writers and uncertain saves? | Inventory inspection / owner | Safe create-versus-existing decisions and retry resolution |
| Q-06 | How should a confirmed duplicate or changed record be resolved when quantities/prices differ? No add/replace policy has been approved. | Owner | Updating an existing inventory record |
| Q-07 | Which image models are available in the owner's accounts, and which wins the source-product benchmark? | Owner / pilot | Selecting the production image route |
| Q-08 | After the first reviewed image set, which later outputs need owner review? No universal approval threshold is agreed. | Owner / pilot | Unattended image acceptance policy |
| Q-09 | What Drive editing permissions and concurrency controls are available for safe same-file write-back? | Owner / integration inspection | Production write-back |
| Q-10 | Are Drive links sufficient for generated image columns, or are embedded previews also required? | Owner | Final workbook enrichment layout |
| Q-11 | What do supplier size codes mean where ambiguous, including M/Y prefixes and numeric ranges? | Owner / supplier evidence | Ambiguous size and age normalization |
| Q-12 | Which local installation method, runtime versions, startup behaviour, and worker library will be used? | Implementer | Runtime installation |
| Q-13 | What batch limits, generation budget, schedule, retention, and recovery objectives are acceptable? | Owner / measured pilot | Wider unattended operation |
| Q-14 | Are dated workbooks historical snapshots, deliveries, or mixed? This remains unanswered; duplicate investigation is required regardless. | Owner / source reconciliation | Any stock update or aggregation across files |
| Q-15 | Do any tabs or subfolders need exclusion, and how are archived/unsupported files identified? | Owner / full source inventory | Final folder manifest |

Documentation is complete as a discussion baseline despite these open items. Live operation is not implementation-ready merely because the documents exist.
