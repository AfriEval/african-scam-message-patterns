# Changelog

All notable changes to this dataset are documented here.

## [0.1.0] - 2026-10-22

### Added
- Kenya dataset `af-scam-ke-v0.1.csv` with 59 records (50 synthetic, 9 real-world), exported from `AF-SCAM-KE_Standardized_v0.1.xlsx`.
- Scam taxonomy with 56 subtypes (`TAX-001` to `TAX-056`).
- Tactics vocabulary with 21 tactics.
- Empty Nigeria dataset with the shared schema.
- Data dictionary, annotation guidelines, verification protocol and privacy policy.

### Known issues
- `tactics` and `requested_action` values are not yet normalised to the controlled vocabularies (mixed casing, `;_` separators, typos such as `shortend_url`).
- `language_tags` is missing for 19 records.
- Open taxonomy questions are listed in `docs/annotation_guidelines.md`.
