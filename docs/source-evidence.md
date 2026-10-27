# Source evidence and limits

Recorded: 2026-10-27. Evidence below comes from this discussion and the inspection performed within it. Source workbooks may change; recorded findings are not a fresh full-folder audit. The complete supplier workbooks and account state are intentionally not copied into the repository.

## Owner sources

| ID | Source | What it establishes |
| --- | --- | --- |
| SRC-01 | Initial requirements and [Drive folder](https://drive.google.com/drive/folders/1whVWEjIICuwnTSpgTtYTV4RZviUUWtnX) | Intended automation scope and source location. |
| SRC-02 | [General-form screenshot](references/inventory-general.png) | Visible product fields and Save action. |
| SRC-03 | [Variant-form screenshot](references/inventory-variants.png) | Visible colour/size combinations, price, quantity, barcode and warehouse selection. |
| SRC-04 | Barcode clarification | One barcode per row; flag and investigate repeated barcodes first. |
| SRC-05 | Colour/SKU clarification | One confirmed design across colours and sizes; relationship detection is central. |
| SRC-06 | [Bilingual example](references/bilingual-copy-example.md) | Required languages, description structure and editorial reference. |
| SRC-07 | Currency clarification | Saudi riyals, SAR. Does not establish selling price or tax treatment. |
| SRC-08 | Documentation request | Authority to create this baseline and BMad project documents. |

## Screenshot observations

The general screenshot shows required الاسم and التصنيف, a second الاسم بالعربية field, brand selection, product barcode, variant type, one description box, required weight in kg, optional-looking dimensions in cm, and حفظ المنتج. The product barcode hint says a blank may generate one automatically; this is a displayed hint, not a verified behaviour. It does not authorize replacing original variant barcodes or using a SKU as a barcode.

The second screenshot states that each size/colour combination represents a variant. It shows size, colour, required price and quantity, variant barcode, an add-variant action and warehouse WH-001. That visible warehouse is not a confirmed business selection.

Dedicated SKU controls and image-upload controls are not established by these cropped screenshots. The form may have other areas. Field limits, required validations, complete lookup coverage and post-save behaviour require authenticated inspection of [the target site](https://inventorysuite.neurix.uk/products/new).

## Workbook observations

- The first bounded listing returned **100 files, all `.xlsx`**, without establishing a total or complete pagination coverage. The largest listed file was 761,289,141 bytes; many others were tens of MB. This supports bounded processing rather than loading the folder at once.
- Text previews were inspected for men's shorts, children's garments, and women's dresses. Headers and size encodings differ, including الصنف والمقاس, الصنف, attached letter/numeric suffixes and M/Y codes.
- Original inspected children workbook: [اون لاين ولادي+بناتي 24-10 معاذ.xlsx](https://drive.google.com/file/d/1egFqMpkufaaSFfKJk05gTnXWSKxBoxgJ/view). Its downloaded inspection copy was 947,211 bytes, with worksheet ورقة1 and 51 embedded media files. These are original Excel drawing/media assets, not values returned in the text preview's picture cells.
- Rows 26, 28 and 47 have the same generic blue boys' T-shirt wording, size M6, brand CANADA, quantity 3 and price 19, but show different designs. This is evidence against text-only grouping; it does not establish a universal barcode pattern or size-code meaning.

| Excel row | Barcode | Original photo |
| --- | --- | --- |
| 26 | `2000227059216` | [Sports figure print](references/source-row-26-front.jpeg) |
| 28 | `2000229033078` | [Lettering print](references/source-row-28-front.jpeg) |
| 47 | `2000229020207` | [Shark print](references/source-row-47-front.jpeg) |

The example images are retained as small reference assets. No model-generated photographs were produced, compared, approved or uploaded during this discussion.

## Current technical references

These official pages were opened during this documentation work. They establish available mechanisms, not account-specific access, product fidelity, installed versions or verified automation.

- [n8n Docker Compose installation](https://docs.n8n.io/deploy/host-n8n/install-options/install-using-docker-compose.md): a documented local deployment route with persistent data. The older Docker page now redirects and labels its content outdated; do not copy its old launch commands as a current project configuration. The current Compose guide includes an n8n Assistant sandbox stack that is **not** a selected dependency for this project.
- [n8n Wait node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/): persisted waiting and resume conditions useful for login/review orchestration; project-level restart correctness still requires its own evidence.
- [Gemini image generation/editing](https://support.google.com/gemini/answer/14286560?hl=en): reference editing and consistency-related features; actual account availability and quality must be checked in the pilot.
- [Official OpenAI image documentation](https://learn.chatgpt.com/docs/image-generation): reference-based image editing, iterative feedback and account-dependent availability; not a measured comparison with Gemini or an API-to-website model equivalence claim.

## Unverified areas

No installed n8n service, worker implementation, application database, imported workflow, runtime pin, full-folder parse, provider login/generation/download, Drive write-back, authenticated inventory inspection, live save or release acceptance has been demonstrated by this documentation. BMad setup and documentation checks are recorded separately in [validation](DOCUMENTATION-VALIDATION.md).
