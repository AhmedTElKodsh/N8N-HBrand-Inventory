# HBrand Inventory Automation

Documentation baseline: **2026-10-27**. This project will use a local n8n engine to turn Excel workbooks in Google Drive into correctly grouped, bilingual inventory products with reviewed AI-generated model photography.

The repository currently contains requirements, planning documents, reference images, and BMad project tooling. The n8n runtime, browser worker, workflows, and live inventory integration have **not been implemented or verified**.

## Start here

1. Read the [canonical specification](_bmad-output/specs/spec-hbrand-inventory/SPEC.md) and every companion listed in its frontmatter.
2. Read the [confirmed decisions and open questions](docs/decisions-and-open-questions.md).
3. Use the [documentation index](docs/README.md) to find the PRD, architecture, UX, backlog, acceptance scenarios, and operational guidance.
4. Read the [implementation readiness assessment](_bmad-output/planning-artifacts/implementation-readiness.md) before treating a story as ready for live execution.

## Confirmed business rules

- Every source row must have one barcode; duplicate barcodes are flagged and checked for an existing product or duplicate record first.
- One confirmed garment design has one stable parent SKU across its colours and sizes. Each observed colour/size variant retains its original barcode, quantity, and price.
- Titles and full descriptions are required in English and Arabic.
- Prices use **Saudi riyals: SAR / ر.س**. Whether the source price is a selling price or purchase cost is still unanswered.
- Initial image generation and inventory entry use the websites through a browser. The owner signs in and reviews the first generated images.
- Generated fields are appended to the same Drive workbook; the original product data and images must be preserved.

## Project locations

| Location | Purpose |
| --- | --- |
| `_bmad-output/specs/spec-hbrand-inventory/` | Canonical capability contract and detailed companions |
| `_bmad-output/planning-artifacts/` | Brief, PRD, architecture, UX, epics, roadmap, readiness |
| `_bmad-output/implementation-artifacts/` | Future implementation evidence; no completed sprint is claimed |
| `docs/` | Decisions, discussion record, evidence, operations, BMad guide |
| `_bmad/` | Supported BMad configuration and helper scripts |

The actual Git checkout is the nested `N8N-HBrand-Inventory` directory. Paths in these documents are relative to that checkout, so the package remains portable.

## External systems

- [Source Drive folder](https://drive.google.com/drive/folders/1whVWEjIICuwnTSpgTtYTV4RZviUUWtnX)
- [Inventory product creation](https://inventorysuite.neurix.uk/products/new)

These links identify the intended integrations. Access through this conversation does not configure credentials for a future local n8n installation.

## Documentation status

The discussion has been captured. Technical choices that were suggested rather than confirmed remain labelled as proposals. Readiness blockers are recorded rather than filled with invented business values. No application tests or live import acceptance results are claimed by this documentation baseline.
