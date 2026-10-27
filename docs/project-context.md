# Project context

Updated: 2026-10-27.

## Practical objective

The owner has Excel product workbooks in Drive with low-quality product photos, inconsistent headers, mixed product/size text, and a different barcode for each variant. The intended system converts those records into accurate inventory products with one parent SKU per design, observed colour/size variants, bilingual copy, and suitable AI-generated photographs of human models wearing the garments.

Local n8n must coordinate the complete process. The initial route uses the image-provider websites and the existing inventory website through authenticated browsers because inventory API access is currently difficult. The owner handles account sign-in and reviews the first generated images.

## Known current state

- The Git checkout had no commits or application files when documentation work began.
- A connected Drive tool listed 100 Excel files in its first bounded listing; total folder coverage was not established.
- Text from three sample workbooks and the original children’s workbook were inspected during this discussion.
- Inventory evidence consists of two owner-provided screenshots. No authenticated live form or product lookup was tested.
- BMad project setup was created using the supported installed setup script. Application infrastructure remains uninstalled/unverified.

## Confirmed inputs

- Source folder: [Drive](https://drive.google.com/drive/folders/1whVWEjIICuwnTSpgTtYTV4RZviUUWtnX).
- Target: [new product form](https://inventorysuite.neurix.uk/products/new).
- Currency: SAR.
- Every source row has one barcode; repeats require investigation first.
- The same confirmed design shares one parent SKU across colours and sizes.
- Improved titles and complete descriptions must be in English and Arabic.

## Important unresolved facts

The source price's commercial meaning, missing required weight, final category mappings, correct warehouse, actual SKU/image controls, available product lookup, Drive write permissions, provider/account availability, and later image-review policy remain open. The [question register](decisions-and-open-questions.md) owns these items and their blocking conditions.

## Proposed implementation direction

Local n8n coordinates bounded jobs; a separate local worker handles workbook processing and browser interactions; durable job records prevent duplicate imports and support recovery. Docker and SQLite were suggested, not installed or selected by the owner. Runtime versions and browser libraries are deferred until implementation verifies the actual environment.

The first meaningful pilot is one source-confirmed design with multiple colours and sizes, plus an intentional duplicate case. No arbitrary catalogue-wide accuracy, throughput, cost, or uptime target has been agreed.
