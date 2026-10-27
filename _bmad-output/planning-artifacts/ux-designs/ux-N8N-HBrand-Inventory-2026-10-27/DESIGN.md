---
name: HBrand Inventory Automation
description: Visual boundaries for existing workflow surfaces and faithful catalogue photography.
status: draft
created: 2026-10-27
updated: 2026-10-27
colors: {}
typography:
  body:
    note: Inherit the active host application; Arabic and English must remain legible.
rounded: {}
spacing: {}
components: {}
sources:
  - ../../../specs/spec-hbrand-inventory/content-and-imagery.md
---

# Visual design boundaries

## Brand & Style

The owner requested professional, photorealistic product photography comparable in presentation quality to established clothing brands. The garment's actual design, colour and print remain the subject. No specific campaign, model identity, background palette, logo treatment, or website redesign was selected.

Initial operation inherits the existing inventory, n8n, Drive and image-provider interfaces. This document adds no new storefront or custom dashboard. Proposed review behaviour is specified in [EXPERIENCE.md](EXPERIENCE.md); its exact host surface remains undecided.

## Colors

No new UI palette is selected; the empty colour-token map is intentional. Source garment colours are product facts and must not be normalized to a decorative brand palette. The inventory screenshots show a dark interface and a lavender save action, but sampled screenshots do not establish exact reusable design tokens.

## Typography

Use inherited host typography as documented in `{typography.body.note}`. Product copy must render readable Arabic and English without corrupting direction, punctuation, size codes or barcode digits. Exact font families and scale changes have not been requested.

## Layout & Spacing

Existing host layouts are retained. The proposed review presentation places original source references beside generated output, keeps front/back/side labels visible, and associates each gallery with its exact colourway and version. No new spacing tokens or responsive breakpoints are binding in this baseline.

## Components

| Surface element | Visual requirement / status |
| --- | --- |
| Original versus generated image comparison | Proposed side-by-side evidence with view/colour/version labels; original images must stay inspectable at useful size. |
| Bilingual copy review | Proposed separate English and Arabic blocks with correct reading direction and obvious parent-versus-variant scope. |
| Duplicate/grouping evidence | Proposed original pictures, raw titles, barcodes, colours/sizes and source locations together. |
| Inventory form | Existing third-party surface; two supplied screenshots are reference evidence, not an implementation-ready component specification. |
| Generated gallery | Faithful garment, consistent model/photography style across views and confirmed colours; source references govern product details. |

## Do's and Don'ts

- Preserve the actual garment print, lettering, construction and colour relationships.
- Use model audience appropriate to confirmed product information.
- Keep a consistent photo treatment across a confirmed product family; reuse a colour gallery across sizes when faithful.
- Show uncertainty and asset/version labels as meaningful text, not colour alone.
- Do not invent palette, body measurements, detailed photo dimensions or a complete custom review application from the broad aesthetic reference.
- Do not label an unreviewed rendering as accepted product photography.

This visual boundary document is a draft with explicit unselected values. No custom mockups were produced because a new UI and visual direction were not requested or chosen.
