# Risk register

Baseline: 2026-10-27. These are concrete risks identified in the discussion/design review; ratings are qualitative priorities for the proposed implementation, not measured incident probabilities.

| ID | Risk and practical impact | Required control / next evidence | Related questions |
| --- | --- | --- | --- |
| RISK-1 | Generic wording, similar barcodes or adjacent rows merge distinct designs. | Compare original garment details; retain separate print designs; review uncertain families and remember resolutions. | Q-11 |
| RISK-2 | A duplicate in a later file is discovered after an earlier row is enriched/imported. | Complete a versioned source-barcode index before clearance; partial source coverage stays unresolved. | Q-15 |
| RISK-3 | Repeated dated records inflate stock or replace a genuine value. | Flag duplicates first; link exact existing records and keep add/replace policy unresolved until supplied. | Q-06, Q-14 |
| RISK-4 | Cost is imported as selling price, or missing weight is fabricated. | Preserve unknown price kind; obtain actual commercial meaning and physical facts. | Q-01, Q-02 |
| RISK-5 | AI changes print, lettering, colour or unseen construction. | Original-source fidelity comparison, owner first-image review, retained versions and scoped acceptance. | Q-07, Q-08 |
| RISK-6 | English and Arabic disagree or age/size codes are misread. | One canonical fact record, correct parent/colour scope and bilingual review. | Q-11 |
| RISK-7 | Excel re-save drops drawings/formulas or writes to shifted rows. | Preserve and compare a staged copy, original image anchors and current row identities. | Q-09, Q-10 |
| RISK-8 | Drive enrichment overwrites a concurrent human edit. | Conditional write or enforced exclusive window; precheck-only races do not pass acceptance. | Q-09 |
| RISK-9 | Own enrichment retriggers work or invalidates valid review, while real source changes go unnoticed. | Separate physical Drive and supplier-fact/image revisions; compare original content independent of automation fields. | Q-09 |
| RISK-10 | Interrupted/delayed Save causes a duplicate on retry. | Persist SUBMITTING first; fence stale workers; retain reservation until definitive outcome/verified target guarantees; negative lookup alone is insufficient. | Q-05 |
| RISK-11 | Other inventory writers bypass local reservations. | Verify target uniqueness/idempotency or enforce an exclusive writing window. | Q-05 |
| RISK-12 | Browser controls, sessions or downloads change unexpectedly. | Pause with evidence; re-inspect the actual surface, keep model labels/versioned mappings and test recovery. | Q-03, Q-07 |
| RISK-13 | Large workbooks or repeated generation exhaust resources/budget. | Bounded jobs, referenced assets, measured pilot limits and retained retry counts. | Q-12, Q-13 |
| RISK-14 | A document or green local check is mistaken for deployed behaviour. | Separate documentation, offline verification, authenticated pilot and release results; use explicit current-state records. | All |

No risk entry grants authority to fabricate missing business values, silently change stock, or add an unrequested compliance programme. Controls are scoped to the catalogue and automation requirements discussed.
