# Data contracts and workflow states

Companion to [SPEC.md](SPEC.md). Business identity rules are confirmed; the names below are a proposed implementation contract for consistent downstream work. The physical database, worker transport, and inventory selectors are deferred. Any implementation change must preserve the semantics.

## Identity model

| Entity | Identifier and meaning | Cardinality / preservation |
| --- | --- | --- |
| Physical workbook revision | Drive file ID plus provider version/revision and captured file digest | Same file ID is retained; automation enrichment may change this revision without changing supplier facts. |
| Supplier content revision | Digest of original supplier values and original image-to-product associations, excluding automation columns/assets | Reviews bind this semantic input; a genuine supplier fact/image change invalidates affected output even if enrichment columns are unchanged. |
| Source row observation | Workbook revision + worksheet identity + row location + raw-value digest | Immutable observation. Row number alone is not stable across sorting or editing. |
| Original image asset | Source workbook revision, media digest and drawing relationship/anchor | A picture can be reused by several size rows; front/back and row associations are retained. |
| Variant | Original barcode as text within this catalogue's duplicate-check scope | One source barcode value per row. Repeated observations are investigated, not automatically counted twice. |
| Product family | Persistent internal design identity | Groups the same confirmed garment design across colours and observed sizes. |
| Parent SKU | Stable, unique code assigned once to the product family | Distinct from variant barcode and any target-generated barcode. Format remains an implementation proposal; uniqueness and persistence are required. |
| Colourway | Family identity + confirmed colour specification | A multi-colour garment such as yellow/white is one colourway, not two invented products. |
| Image gallery | Family + colourway + source/prompt/model/style revision | Shared across that colourway's sizes when faithful. Store individual front/back/side assets. |
| Import operation | Stable operation identity + family + intended variant set + approved payload revision | Used to reconcile retries and prevent repeated stock creation. |

One family has many colourways; each colourway has only its observed size variants. Two variants with the same apparent colour/size require conflict review if their relationship is not established. Do not collapse distinct designs merely because their barcodes or normalized names resemble each other.

## Canonical values

| Field | Contract |
| --- | --- |
| `barcode_raw`, `barcode` | Strings. Preserve original text, including meaningful leading zeroes. Trimming must be traceable. Never invent digits, pad an identifier, or derive a parent SKU by truncating a barcode. |
| `source_name_raw`, `size_raw`, `brand_raw`, `colour_raw` | Original values retained separately from normalization. |
| `size_normalized`, `size_system`, `age_range` | Fill only when interpretation is established. Ambiguous M/Y/numeric encodings retain raw values and issue references. |
| `colours` | Confirmed colourway names/codes with English/Arabic labels; distinguish observed colour from uncertain image interpretation. |
| `source_quantity` | Preserve the source value. Candidate integer/negative/blank anomalies are flagged under the source's real semantics; do not silently use zero. |
| `source_price` | Exact decimal value, represented without binary floating-point drift by the eventual implementation. |
| `currency` | `SAR`, confirmed. |
| `price_kind`, `tax_treatment` | Unknown until Q-01 is answered. An unknown value cannot populate a live selling-price control. |
| `weight_kg`, `dimensions_cm` | Nullable factual inputs with units/provenance. Missing required values are blockers, not AI-generated guesses. |
| `family_id`, `parent_sku`, `colourway_id` | Stable identity registry values. Corrected display titles do not change identity. |
| `product_title_en`, `product_title_ar` | Family-scoped titles; accurate across all included colours. |
| `variant_title_en`, `variant_title_ar` | Optional colour-specific titles; do not imply unobserved stock or unsupported sizes. |
| `description_en`, `description_ar` | Full descriptions from one shared fact record; preserve per-colour size availability and language parity. |
| `field_provenance` | Source cell/image reference or owner-supplied fact, normalization applied, uncertainty and decision reference. Store observable evidence rather than hidden reasoning. |
| `asset_refs` | Durable file identifier/location, view, digest, source inputs, prompt revision, displayed provider/model, generation attempt, and acceptance status. |

## Existence and duplicate outcomes

Before any row is cleared for enrichment, freeze the selected source manifest and complete its versioned barcode index, including every intended workbook/tab and prior import observations. The index records covered revisions and excludes nothing silently. An unreadable or partially listed source scope cannot establish uniqueness; it needs a recorded scope resolution or remains blocked. Production scope is the intended full folder; an explicitly bounded pilot records its narrower guarantee. Revalidate relevant scope/index freshness before external writes.

| Outcome | Meaning | Allowed next action |
| --- | --- | --- |
| `INVALID_BARCODE` | Missing, multiple, damaged, or uninterpretable barcode | Flag row; obtain corrected source evidence. |
| `DUPLICATE_SOURCE` | Barcode repeats within a workbook or across files | Flag every affected observation; inspect exact product and source history first. |
| `EXISTING_EXACT_VARIANT` | Reliable lookup establishes that this variant already exists | Link target identity and flag existing; no automatic stock/price update. |
| `CONFLICT` | Same barcode has inconsistent garment/facts/target relationships | Hold affected work for a recorded resolution. |
| `ABSENT_VERIFIED` | Lookup scope is sufficiently complete to establish absence | Continue grouping and preflight; recheck the parent/variant just before create. |
| `EXISTENCE_UNKNOWN` | Lookup unavailable, partial, stale, or ambiguous | Cannot authorize create. Record missing lookup evidence. |

Family matching is also required: a new barcode can belong to an existing parent product. If so, route to a separate confirmed variant-add/update path; do not create another parent. Actual update permissions and stock behaviour remain Q-06. “Not in the current search page” is not verified absence.

## Proposed appended workbook columns

| Group | Proposed columns |
| --- | --- |
| Source linkage | `Automation_Row_ID`, `Source_Revision`, `Source_Row_Digest` |
| Identity | `Parent_SKU`, `Family_ID`, `Colourway_ID`, `Barcode_Check_Status`, `Duplicate_Reference` |
| Parsed attributes | `Product_Name_Extracted`, `Size_Normalized`, `Size_System`, `Colour_EN`, `Colour_AR`, `Audience` |
| Bilingual copy | `Product_Title_EN`, `Product_Title_AR`, `Variant_Title_EN`, `Variant_Title_AR`, `Description_EN`, `Description_AR` |
| Required facts | `Currency`, `Price_Kind`, `Weight_kg`, `Length_cm`, `Width_cm`, `Height_cm`, `Category_Target`, `Brand_Target`, `Warehouse_Target` |
| Images | `Image_Front_URL`, `Image_Back_URL`, `Image_Side_Left_URL`, `Image_Side_Right_URL`, `Image_Provider`, `Image_Revision`, `Image_Review_Status` |
| Result | `Inventory_Product_ID`, `Inventory_Product_URL`, `Import_Status`, `Issue_Code`, `Issue_Detail`, `Verified_At` |

These names are a proposed layout, not already added columns. Keep original columns and sheets intact. Repeated parent-level values may appear on each source row for that family; the identity registry remains authoritative. Row matching uses immutable source observations and verified current content, not saved row numbers after a human sort. Links-versus-previews is Q-10.

## Write-back consistency

1. Retain an original source revision/backup and prepare the enriched workbook on a copy.
2. Confirm the exact intended Drive file ID, current revision, row identities, and unchanged supplier content.
3. Preserve formulas, media/drawings/anchors, tab structure and relevant formatting; do not rely on a text-only conversion to round-trip an Excel file.
4. Use a supported conditional write or an enforced exclusive editing window. A read-before-write check alone does not close the concurrent-edit race. If neither is available, hold write-back under Q-09.
5. Read back the updated same file, compare preservation invariants and appended values, then record the automation-produced physical revision and supplier-content digest separately.
6. Ignore an enrichment-only physical revision as a new supplier import or approval invalidation; recompute original supplier values/image associations to detect real changes. Sorting may change row locations without changing garment facts, but current row alignment must still be verified. A rollback reconciles inventory side effects separately; restoring a workbook does not undo stock.

## Proposed job states

| State | Required evidence / transition |
| --- | --- |
| `DISCOVERED` | Scoped source revision and row/image observations retained. |
| `CHECKING_EXISTENCE` | Barcode checks and complete target lookup in progress. |
| `BLOCKED_BARCODE`, `BLOCKED_GROUPING`, `BLOCKED_FACTS`, `BLOCKED_TARGET` | Specific unresolved issue and affected rows/family; resolved evidence is required to resume. |
| `GROUPED` | Established family and observed variant membership, stable SKU, source evidence. |
| `CONTENT_DRAFT` | Bilingual copy from the canonical original-source facts. |
| `IMAGES_DRAFT` | Provider attempts and actual downloaded assets retained. |
| `AWAITING_IMAGE_REVIEW` | The owner is reviewing the relevant version; no timeout counts as acceptance. |
| `READY_TO_WRITEBACK` | Applicable content/image acceptance and source facts are established. |
| `WRITEBACK_VERIFIED` | Same-file enrichment and source preservation verified. |
| `READY_TO_IMPORT` | Current approved payload, complete target mapping, source revision, absence/parent checks, factual inputs and warehouse selected. |
| `SUBMITTING` | Durable operation record written, family/variant reservation held and target uniqueness/idempotency or an enforced exclusive writing window established **before** Save. |
| `VERIFYING` | Final action may have succeeded; inspect the actual destination through fresh navigation. |
| `IMPORTED` | Target identity and full intended values/variants/assets verified. |
| `ALREADY_EXISTS` | Existing exact record linked and issue resolved without an unauthorized update. |
| `IMPORT_UNKNOWN` | Save outcome cannot be established. No automatic resubmission. |
| `RETRYABLE_FAILURE` | Failure is proven to precede any possible external effect, or an idempotent operation can safely be repeated. |

One durable mutation authority owns family assignment, source-write operations, submission reservations and final import outcomes. n8n executions and browser workers must not independently invent successful states. Persist the intended payload digest and target lookup evidence; a changed payload is not permission to repeat an unresolved operation.

Local reservations exclude this automation's workers, not human or external inventory writers. Verify target-enforced uniqueness/idempotency over the relevant identities or establish an exclusive writing window spanning lookup through confirmed outcome. If neither can be established, hold creation under Q-05 rather than claim duplicate prevention.

After an uncertain Save, fence stale worker/session attempts before recovery. Even a fenced or terminated worker cannot cancel a server request already in flight. A fresh negative lookup alone does not prove failure or release the reservation. Retain SUBMITTING/IMPORT_UNKNOWN until definitive target outcome evidence or a verified target guarantee makes resolution safe; otherwise escalate for target-side reconciliation without resubmission.

## Review and recovery records

Each review records reviewer, time, supplier-content/family membership revision, canonical-fact revision, content revision, prompt/model/style revision, asset digests, verdict, feedback, and scope. Physical Drive revision is retained for write safety but automation-only enrichment does not by itself invalidate unchanged fact/image acceptance. An asset approval does not automatically approve all future products. Proposed style-policy acceptance is separate and must be defined under Q-08. Preserve the authority to resume a particular job rather than accepting arbitrary job IDs or replayed review events.

UTC timestamps are offset-aware; local display/scheduling may use the host's Africa/Cairo timezone as an implementation default. The business currency SAR does not establish an operating timezone. Schedules remain Q-13.
