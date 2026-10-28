# Data Dictionary

Applies to every country file in `data/` (e.g. `data/kenya/af-scam-ke-v0.1.csv`). Files are UTF-8 CSV with a header row. Multi-valued fields (type `list`) hold a JSON array of strings, e.g. `["authority_claim", "urgency_pressure"]`; an empty cell means not yet labelled.

| Field | Type | Description | Allowed values / format |
|---|---|---|---|
| `observation_id` | string | Unique record ID | `AF-SCAM-{CC}-{SYN or REAL}-{NNNN}`, e.g. `AF-SCAM-KE-REAL-0001` |
| `country` | string | ISO 3166-1 alpha-2 country code | `KE`, `NG`, ... |
| `record_origin` | enum | Whether the message is real or generated | `synthetic`, `real_world` |
| `source_type` | enum | Channel the message came from | `synthetic_generated`; firsthand: `firsthand_sms`, `firsthand_whatsapp`, `firsthand_other`; collected from public web sources: `public_screenshot_sms`, `public_screenshot_email`, `public_screenshot_social_dm` |
| `message_text_redacted` | text | Message body with identifiers replaced by placeholders | Placeholders: `[PHONE]`, `[LINK]`, `[EMAIL]`, `[PAYBILL]`, `[ACCOUNT]`, `[AMOUNT]`, `[ORGANIZATION]`, `[NAME]`, `[ADDRESS]`, `[CODE]` |
| `language_tags` | list | Languages present in the message | ISO 639-1 codes, e.g. `["sw", "en"]`. Empty in v0.1 pending fresh labelling |
| `taxonomy_id` | string | Subtype assigned from the taxonomy | `TAX-NNN`, see `taxonomy/scam_taxonomy.csv` |
| `category` | string | Top-level category (looked up from `taxonomy_id`) | |
| `scam_type` | string | Mid-level scam type (looked up from `taxonomy_id`) | |
| `subtype` | string | Subtype (looked up from `taxonomy_id`) | |
| `claimed_identity` | string | Who the sender claims to be | Free text, e.g. `Bank`, `Property management` |
| `tactics` | list | Persuasion tactics used | `tactic` codes from `taxonomy/tactics.csv`, e.g. `["authority_claim", "urgency_pressure"]` |
| `requested_action` | list | What the recipient is asked to do | Values from: `Open link`, `Pay fee`, `Pay deposit`, `Pay to account`, `Send money`, `Submit information`, `Submit documents`, `Call number`, `Share code`, `Invest`, `Attend in person`, `Dial USSD code`, `Reply to message`, `Reply by email`, `Release goods`, `Activate service`, `Vote`, `None stated` |
| `risk_indicators` | list | Observable red flags in the message | Free text items |
| `fraud_status` | enum | Fraud determination | `suspected_fraud`, `verified_fraudulent_request`, `unassessed` |
| `verification_status` | enum | State of verification | `not_applicable` (synthetic), `completed_reported`, `not_documented` |
| `review_status` | enum | Editorial review state | `pending_review`, `reviewed` |
| `review_notes` | text | Reviewer comments | Free text |
| `screenshot_file` | string | Source screenshot for a real-world record, if one exists | File name in the country's `screenshots/` folder. Screenshots are unredacted and are not published |

## Notes

- `category`, `scam_type` and `subtype` always match the row for `taxonomy_id` in `taxonomy/scam_taxonomy.csv`. In the source workbook they are formulas; enter only `taxonomy_id`.
- `unassessed` means evidence is missing or inadequate. It does not mean the message is legitimate.
- Synthetic records always have `verification_status = not_applicable`.
