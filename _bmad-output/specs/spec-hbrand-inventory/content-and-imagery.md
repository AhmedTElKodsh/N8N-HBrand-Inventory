# Bilingual content and product imagery

Companion to [SPEC.md](SPEC.md). The [owner's example](../../../docs/references/bilingual-copy-example.md) sets the desired editorial shape. Its product facts are illustrative, not defaults for other garments.

## Fact selection before writing

Build one structured product fact record from original row values, source front/back pictures, confirmed family relationships, and owner corrections. Record whether a fact is supplied, visibly supported, normalized, uncertain, or missing. Titles, descriptions, prompts and both languages consume this record. Do not add a feature merely because the generated human-model image depicts it.

Examples of supported facts include the recorded brand, clearly visible stripe/print, confirmed colourway, neckline/sleeve detail, product type, and actual listed sizes. Composition percentages, washing temperature, origin, stretch, performance and measurements need explicit evidence. Editorial outfit suggestions are permissible when presented as suggestions. Ambiguous product audience or fit requires restrained wording or review.

## Titles

- English and Arabic express the same product identity and confirmed audience.
- Parent titles stay accurate for all included colourways. Put colour-specific wording into variant titles when the parent contains several colours.
- Include type and a useful distinguishing detail; avoid inventing a collection, model number, certification, or material.
- Preserve brand spelling and identity; title corrections do not change parent SKU.

Illustrative parent: “Girls' Striped T-Shirt” / “تيشرت بناتي مخطط”. Illustrative colourway: “Girls' Yellow and White Striped T-Shirt” / “تيشرت بناتي مخطط باللونين الأصفر والأبيض”. These are formatting examples, not generated catalogue records.

## Full descriptions

| Section | English / Arabic purpose |
| --- | --- |
| Introduction | Natural garment summary using supported appearance and intended styling. |
| Product details / تفاصيل القطعة | Brand, confirmed colours, supported cut/design details. |
| Styling and selection / اقتراحات التنسيق والاختيار | Practical outfit suggestions, clearly editorial. |
| Sizes and fit / المقاسات واختيار الملاءمة | Actual recorded sizes with verified size system; preserve which sizes belong to each colour. |
| Care / العناية بالقطعة | Actual supplied instructions, or guidance to consult the garment's care label when no instructions were supplied. |

Maintain parity for audience, brand, colours, sizes and units. Use natural Arabic and English rather than literal phrasing that changes meaning. Correct output grammar such as “6–9 months”; retain `size_raw` unchanged. Do not turn `M6` into adult M or an age claim without supplier-code evidence. Record listed sizes separately from current in-stock availability so a stale description is not mistaken for a live stock promise.

Store the four main fields separately: product title EN/AR and description EN/AR. Colour-specific titles are separate additional fields. If the actual inventory form has one description control, a proposed mapping is clearly separated Arabic and English sections in that control; verify its length/format/rendering first.

## Provider comparison

Initial candidates are image generation available in the owner's Gemini and ChatGPT websites. Account model availability, limits and current UI names must be recorded during the actual comparison. No API-model listing establishes which model runs in a website account.

The same source garments and comparable instructions go to both providers. Start with the first reviewable example, then cover representative challenging products before claiming a general choice. Retain all attempts rather than reporting only a cherry-picked success.

| Dimension | Review evidence |
| --- | --- |
| Garment fidelity | Print/lettering, seams, pockets, neckline, sleeves, silhouette and relative proportions match source. |
| Colour fidelity | Confirmed source colour and print-colour relationships remain accurate; difficult lighting stays uncertain. |
| View consistency | Same garment and appropriate model across front/back/sides; no changed artwork or invented back feature. |
| Photography | Photorealism, fit plausibility, framing, background, lighting and usable downloaded resolution. |
| Operational effort | Actual generation/download success, latency, retries, account availability and corrections needed. |
| Owner acceptance | Review verdict and reasons tied to the actual versions. |

Numeric pass thresholds, acceptable correction rate and budget are not yet selected. A model can win for one product type without proving universal superiority. Official capability references are recorded in [source evidence](../../../docs/source-evidence.md); they are not benchmark results.

## Prompt contract

Each request identifies the original reference images by role, confirmed product facts, audience/model direction, requested view, photography direction, and details that must remain fixed. Retain the exact prompt/revision and the displayed provider/model.

Suggested instruction shape, to be adapted to actual product evidence:

> Create a photorealistic catalogue photograph of an appropriate human model wearing the garment in the attached original product references. Preserve the garment's confirmed construction, colour, print and lettering. Use the established model, lighting, framing and background for this product family. Produce the specified view. Treat unavailable garment details as uncertain and return them for review.

This is a prompt contract, not a claim that either model can guarantee those constraints. The initial style direction is professional brand-style catalogue photography; no specific brand campaign, face, background palette, or body measurements have been chosen.

## Colour and size reuse

Within a confirmed family, keep the model/photography style stable across colourways. Each colourway is grounded in its own original references. Similar wording alone must not trigger automatic recolouring. One gallery per colourway can be reused across size variants when faithful; do not generate new colours, sizes, prints, or views and present them as source facts.

Original front/back images should be supplied where available. If a view is missing, an AI-rendered view is an interpretation until reviewed. Distinct left and right outputs, gallery order, crop and minimum resolution are finalized during the pilot.

## Review and revision

The first image set stops for the owner. Show original references beside provider outputs with an obvious verdict and correction input. Retain rejected versions. Changes to garment identity, original supplier facts/image associations or generated assets invalidate affected approval; an automation-only physical Drive revision does not. Accepting the initial set does not silently establish a blanket acceptance rule for future products; Q-08 records the later policy gap.

Rejected or unreviewed assets must not reach the inventory under a label that implies accepted photography. The accepted colourway gallery is linked to all appropriate variants and written back through the source-preserving process.
