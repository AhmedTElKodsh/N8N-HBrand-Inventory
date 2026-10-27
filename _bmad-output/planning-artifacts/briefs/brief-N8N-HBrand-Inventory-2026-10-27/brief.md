---
title: HBrand Inventory Automation — Product Brief
status: draft
created: 2026-10-27
updated: 2026-10-27
sources:
  - ../../../../docs/discussion-record.md
---

# Product brief

## Problem and intended value

The owner needs to turn Excel garment catalogues in Drive into usable inventory products. Source descriptions combine product names and sizes, variant barcodes differ, colour/style relationships are difficult to identify, and product photographs are low quality. Manual grouping, bilingual writing, model photography and browser entry multiply the work and introduce catalogue/stock mistakes.

The intended result is a locally coordinated workflow that preserves source truth, identifies a design across colours and sizes, supplies useful English and Arabic copy and reviewed human-model photographs, enriches the same workbook, and enters a verified product into the existing inventory website.

## Initial operator and surfaces

The owner supplies access, signs into the image providers and inventory, resolves genuinely ambiguous facts, and reviews the first generated images. Drive/Excel, the image-provider websites, the inventory browser form, and local n8n are the initial surfaces. No new customer storefront or custom review application has been requested.

## Confirmed scope

- One barcode per source row; duplicates are flagged and investigated before enrichment/import.
- One stable parent SKU per confirmed design across colours and observed size variants.
- Separate useful attributes from merged supplier text without discarding original values.
- Improved titles and complete descriptions in English and Arabic.
- Faithful photorealistic human-model imagery, appropriate to the garment audience, with front/back/side views and consistent style across colours.
- Gemini-versus-ChatGPT comparison using the owner's first-image feedback.
- Added fields in the same Drive workbook and browser-based inventory save after owner login.
- Currency SAR; a local n8n engine coordinates the full workflow.

## Proposed first outcome

One source-confirmed multi-colour/multi-size family completes the path from original workbook to reviewed copy/images, preserved source enrichment and a freshly verified inventory record. Repeating the job or recovering an interrupted save must not duplicate product/stock. This is a proposed validation slice, not a completed demonstration.

## Differentiating difficulty

Generic titles, nearby rows and similar barcodes are insufficient to prove design identity. Source inspection found distinct shirt prints with the same generic wording, brand, colour and size. Faithful family matching and the preservation of exact variant stock matter more than the number of rows processed.

## Limits and unresolved inputs

The price's commercial meaning, required physical facts, target SKU/image/description controls, warehouse/taxonomy, lookup completeness, duplicate-resolution policy, provider winner and later image-review policy remain open. Runtime deployment, schedules, budgets and release thresholds have not been chosen. See the [decision register](../../../../docs/decisions-and-open-questions.md).

## Success evidence

The owner can inspect the source-to-target relationship, accept the initial images, and find the exact intended product/variants in inventory. Broader release requires the [acceptance scenarios](../../../specs/spec-hbrand-inventory/acceptance.md); documentation and a narrow pilot are separate evidence levels.
