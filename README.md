# African Scam Message Patterns

A dataset of scam and fraud messages from African countries, labelled with a shared taxonomy of scam types, persuasion tactics, claimed identities, requested actions and verification status. It supports research, evaluation of scam-detection models, and public awareness work. Work in progress.

## Contents

| Path | Description |
|---|---|
| `data/kenya/af-scam-ke-v0.1.csv` | Kenya observations: 60 records (50 synthetic, 10 real-world) |
| `data/nigeria/af-scam-ng-screenshots-v0.1.xlsx` | Nigeria observations from public screenshots: 62 real-world records (pending review) |
| `data/nigeria/af-scam-ng-contributor-R-F8JM-W6U-v0.1.xlsx` | Nigeria observations from a contributor: 10 real-world records (pending review) |
| `taxonomy/scam_taxonomy.csv` | Category → scam type → subtype hierarchy (56 subtypes) with working definitions |
| `taxonomy/tactics.csv` | Controlled vocabulary of 21 persuasion tactics |
| `docs/data_dictionary.md` | Field definitions and allowed values |
| `docs/annotation_guidelines.md` | Annotation rules and open taxonomy questions |
| `docs/verification_protocol.md` | How fraud status is established and recorded |
| `docs/privacy_and_consent.md` | Redaction, consent and release rules |
| `examples/` | Usage examples |

## Record origin

Each record is either `synthetic` (written to illustrate a taxonomy subtype) or `real_world` (a message contributed by the person who received it). The two are never mixed: synthetic records are never marked verified. Filter on `record_origin` when evaluating models.

Real-world records may have a `screenshot_file` pointing to the original screenshot. Screenshots are unredacted and are not published in this repository.

## Format

- UTF-8 CSV, one row per message.
- `tactics`, `requested_action`, `risk_indicators` and `language_tags` are JSON arrays, e.g. `["authority_claim", "urgency_pressure"]`. An empty cell means not yet labelled.
- `language_tags` use ISO 639-1 codes (`en`, `sw`). Sheng has no ISO code and is tagged `sw`, with a note in `review_notes`.
- Personal and financial details are replaced with placeholders: `[PHONE]`, `[LINK]`, `[PAYBILL]`, `[ACCOUNT]`, `[AMOUNT]`, `[ORGANIZATION]`, `[NAME]`, `[CODE]`.
- Spelling and grammar in message text are kept exactly as received, because errors are themselves scam signals.

## Quick start

```python
import json
import pandas as pd

ke = pd.read_csv("data/kenya/af-scam-ke-v0.1.csv")
for col in ["tactics", "requested_action", "risk_indicators", "language_tags"]:
    ke[col] = ke[col].apply(lambda v: json.loads(v) if isinstance(v, str) else [])

real = ke[ke.record_origin == "real_world"]
print(real.explode("tactics").tactics.value_counts())
```

## Status

Version 0.1 is a draft. All records are `pending_review`.

- **Taxonomy:** 12 new subtypes (TAX-057 to TAX-068) are proposed from the Nigeria data, including BVN update phishing and fake bank credit alerts. They will be added once reviewed.

See [CHANGELOG.md](CHANGELOG.md) for changes.

## License

See [LICENSE](LICENSE).
