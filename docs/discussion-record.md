# Discussion record

Session date: 2026-10-27. This is a structured record of the BMad party discussion, not a verbatim transcript or an approval of every assistant suggestion.

## Initial intent

The owner requested a local n8n automation that imports Excel workbooks from a Drive folder, separates merged product/size text, unifies related variants under one SKU, creates improved product photographs through Gemini or ChatGPT websites, appends generated values to the source workbook, and enters products through the inventory website. The owner handles account login and wants to review the first generated images before directing corrections.

## Evidence brought into the discussion

Two screenshots show the inventory product/variant form. A bounded Drive listing returned 100 Excel files, including very large workbooks. Three sample workbooks exposed inconsistent headers and size encodings. Inspection of the original children's workbook showed embedded front/back images and distinct printed designs sharing the same generic name, brand, colour, and size. These observations informed the need for evidence-based grouping; they do not establish full-folder correctness or live inventory behaviour.

## Owner clarifications

1. A source row must have one barcode. A duplicate is a flag requiring a check for an exact existing product or duplicate record before other work.
2. The same confirmed product design shares a parent SKU across colours, with size variants within each colour. Recognizing these relationships is the difficult task. Similar barcodes and adjacent rows may help, but adjacency is not universal.
3. Suitable product descriptions and improved titles in English and Arabic are core outputs, based on product information and original images. The owner supplied the [writing example](references/bilingual-copy-example.md).
4. Prices use Saudi riyals. The follow-up question about selling price versus purchase cost was not answered before documentation was requested.
5. The owner asked to round up the discussion and produce the project specification and BMad documentation.

## Perspectives and proposals

- Mary emphasized barcode uniqueness, source provenance, factual content, and unresolved business inputs.
- Winston proposed a local n8n orchestrator, an external worker, persistent identity/state records, safe workbook updates, and read-back verification after save.
- Sally proposed matching the actual garment details, consistent models/poses across colour versions, one gallery per colour, and bilingual copy with parent-versus-variant titles.
- John proposed proving a complete multi-colour/multi-size family before expanding, keeping review focused on uncertainty, and measuring both image providers on the same inputs.

These are design proposals unless separately listed as owner-confirmed decisions. No model was declared the measured winner; no numeric confidence threshold, supplier price semantics, runtime stack version, or rollout schedule was chosen.

## Outcome of this documentation pass

The discussion is closed into a versioned documentation baseline with a canonical capability contract, detailed companions, BMad planning artifacts, an explicit question register, and a backlog. Implementation and external operations remain separate future work. See [readiness](../_bmad-output/planning-artifacts/implementation-readiness.md) and [validation](DOCUMENTATION-VALIDATION.md) for the current limits.
