# Project instructions

## Current state

This is a documentation baseline for HBrand Inventory Automation, not an implemented application. Start with `README.md`, `docs/project-context.md`, and `_bmad-output/specs/spec-hbrand-inventory/SPEC.md`; read every specification companion.

## Requirements and evidence

- Keep confirmed user requirements, assistant proposals, observations, and unresolved questions distinct. The current register is `docs/decisions-and-open-questions.md`.
- Preserve stable CAP, FR, AC, AD, epic, story, and question identifiers when updating documents.
- `SPEC.md` and its spec-authored companions are derived through the `bmad-spec` process from their append-only `.memlog.md`. Append decisions through `_bmad/scripts/memlog.py` before re-deriving; do not silently patch the contract from an unrelated workflow.
- Treat screenshot observations as screenshot observations. The authenticated inventory form, its SKU/image controls, and its lookup behaviour have not been inspected live.
- Do not treat browser clicks, optimistic messages, a matching local fixture, or a document status as proof of a saved inventory product.

## Business invariants

One barcode per source row. Flag duplicates before enrichment or product creation. Never sum or overwrite quantities merely because a barcode repeats. One stable parent SKU per confirmed design across colours and sizes; preserve each observed variant and its original barcode. Similar barcodes, row adjacency, and generic titles are candidate clues rather than sufficient merge evidence. Currency is SAR. Price meaning is unresolved.

Generate English and Arabic copy from original product information and source photos. Preserve unknown facts. Generated images are outputs, not evidence for fabric, construction, care, or other product facts. Initial image review belongs to the owner.

## Work boundaries

The current task produced documentation and BMad tooling. Installation of n8n, account login, Drive write-back, and inventory saves remain future implementation work. Future instructions can authorize that work; this file adds no separate approval ritual. Credentials, session data, and full source workbooks stay out of Git. Do not commit or push without a user request.

## BMad

Use the supported `bmad` setup/status workflow. `_bmad/config.toml` defines artifact locations. Runtime status and validation evidence belong in their appropriate documents; do not fabricate `stepsCompleted`, sprint completion, or user approval.
