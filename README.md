# African Scam Message Patterns

A structured dataset of scam and fraud messages observed in African countries, annotated with a shared taxonomy of scam types, persuasion tactics, claimed identities and requested actions. It supports research, evaluation of scam-detection models, and public awareness work.

## Contents

| Path | Description |
|---|---|
| `data/kenya/af-scam-ke-v0.1.csv` | Kenya observations (59 records: 50 synthetic, 9 real-world) |
| `data/nigeria/af-scam-ng-v0.1.csv` | Nigeria observations (schema only, no records yet) |
| `taxonomy/scam_taxonomy.csv` | Category → scam type → subtype hierarchy with working definitions |
| `taxonomy/tactics.csv` | Controlled vocabulary of persuasion tactics |
| `docs/data_dictionary.md` | Field definitions and allowed values |
| `docs/annotation_guidelines.md` | How records are labelled |
| `docs/verification_protocol.md` | How fraud status is established and recorded |
| `docs/privacy_and_consent.md` | Redaction, consent and release rules |
| `examples/` | Usage examples |

## Record origin

Each record is either `synthetic` (generated to illustrate a taxonomy subtype) or `real_world` (a message contributed firsthand). The two are never mixed: synthetic records are never marked verified. Filter on `record_origin` when evaluating models.

## Quick start

```python
import pandas as pd

ke = pd.read_csv("data/kenya/af-scam-ke-v0.1.csv")
tax = pd.read_csv("taxonomy/scam_taxonomy.csv")
real = ke[ke.record_origin == "real_world"].merge(tax, on="taxonomy_id", suffixes=("", "_tax"))
```

## Status

Version 0.1 is a draft. All records are `pending_review`. See [CHANGELOG.md](CHANGELOG.md).

## License

See [LICENSE](LICENSE).
