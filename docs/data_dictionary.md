# Data Dictionary

Applies to every country file in `data/` (e.g. `data/kenya/af-scam-ke-v0.1.csv`). Files are UTF-8 CSV with a header row; multi-valued fields use `; ` as the separator.

| Field | Type | Description | Allowed values / format |
|---|---|---|---|
| `observation_id` | string | Unique record ID | `AF-SCAM-{CC}-{SYN or REAL}-{NNNN}`, e.g. `AF-SCAM-KE-REAL-0001` |
| `country` | string | ISO 3166-1 alpha-2 country code | `KE`, `NG`, ... |
| `record_origin` | enum | Whether the message is real or generated | `synthetic`, `real_world` |
| `source_type` | enum | Channel the message came from | `synthetic_generated`, `firsthand_sms`, `firsthand_whatsapp` |
| `message_text_redacted` | text | Message body with identifiers replaced by placeholders | Placeholders: `[PHONE]`, `[LINK]`, `[Account Number]`, `[Paybill Number]`, etc. |
| `language_tags` | list | Languages present in the message | ISO 639-1 codes, `;`-separated, e.g. `sw;en` |
| `taxonomy_id` | string | Subtype assigned from the taxonomy | `TAX-NNN`, see `taxonomy/scam_taxonomy.csv` |
| `category` | string | Top-level category (copied from taxonomy) | |
| `scam_type` | string | Mid-level scam type (copied from taxonomy) | |
| `subtype` | string | Subtype (copied from taxonomy) | |
| `claimed_identity` | string | Who the sender claims to be | Free text, e.g. `Bank`, `Property management` |
| `tactics` | list | Persuasion tactics used | Values from `taxonomy/tactics.csv`, `;`-separated |
| `requested_action` | list | What the recipient is asked to do | e.g. `Open link`, `Pay fee`, `Send money`, `Submit information`, `Call number`, `Share code` |
| `risk_indicators` | text | Observable red flags in the message | Free text |
| `fraud_status` | enum | Fraud determination | `suspected_fraud`, `verified_fraudulent_request`, `unassessed` |
| `verification_status` | enum | State of verification | `not_applicable` (synthetic), `completed_reported`, `not_documented` |
| `review_status` | enum | Editorial review state | `pending_review`, `reviewed` |
| `review_notes` | text | Reviewer comments | Free text |

## Notes

- `category`, `scam_type` and `subtype` must match the row for `taxonomy_id` in `taxonomy/scam_taxonomy.csv`.
- `unassessed` means evidence is missing or inadequate. It does not mean the message is legitimate.
- Synthetic records always have `verification_status = not_applicable`.
