---
license: cc-by-4.0
language:
- en
- sw
pretty_name: African Scam Message Patterns
task_categories:
- text-classification
configs:
- config_name: default
  data_files: data/afriscam-v0.1.jsonl
---

# African Scam Message Patterns

A dataset of scam and fraud messages from African countries, labelled with a shared taxonomy of scam types, persuasion tactics, claimed identities, requested actions and verification status. It supports research, evaluation of scam-detection models, and public awareness work. Work in progress.

## Contents

| Path | Description |
|---|---|
| `data/kenya/af-scam-ke-v0.1.csv` | Kenya observations: 60 records, 10 real-world first, then 50 synthetic |
| `data/nigeria/af-scam-ng-screenshots-v0.1.csv` | Nigeria observations from public screenshots: 53 real-world records (pending review) |
| `data/nigeria/af-scam-ng-contributor-R-F8JM-W6U-v0.1.csv` | Nigeria observations from a contributor: 10 real-world records (pending review) |
| `taxonomy/scam_taxonomy.csv` | Category → scam type → subtype hierarchy (68 subtypes) with working definitions |
| `taxonomy/tactics.csv` | Controlled vocabulary of 22 persuasion tactics |
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
- `data/afriscam-v0.1.jsonl` combines all the CSVs into one file, one JSON object per line. List columns are real lists, and `source_file` names the CSV each record came from. Rebuild it with `python3 scripts/combine_data.py`. The Hugging Face viewer shows this file.
- `tactics`, `requested_action`, `risk_indicators` and `language_tags` are JSON arrays, e.g. `["authority_claim", "urgency_pressure"]`. An empty cell means not yet labelled.
- `language_tags` use ISO 639-1 codes (`en`, `sw`). Sheng has no ISO code and is tagged `sw`, with a note in `review_notes`.
- Personal and financial details are replaced with placeholders: `[PHONE]`, `[LINK]`, `[EMAIL]`, `[PAYBILL]`, `[ACCOUNT]`, `[AMOUNT]`, `[ORGANIZATION]`, `[NAME]`, `[ADDRESS]`, `[CODE]`.
- Spelling and grammar in message text are kept exactly as received, because errors are themselves scam signals.

## Quick start

Load the dataset from Hugging Face:

```python
from datasets import load_dataset

ds = load_dataset("Afrieval/african-scam-message-patterns", split="train")
df = ds.to_pandas()

real = df[df.record_origin == "real_world"]
print(real.explode("tactics").tactics.value_counts())
```

Or read the file from a clone of this repository:

```python
import pandas as pd

df = pd.read_json("data/afriscam-v0.1.jsonl", lines=True)
```

`tactics`, `requested_action`, `risk_indicators` and `language_tags` load as lists.

## Status

Version 0.1 is a draft. All records are `pending_review`.

- **Working files:** each CSV is exported from an Excel workbook used for annotation (`AF-SCAM-KE_Standardized_v0.1.xlsx` for Kenya, and the matching `.xlsx` next to each Nigeria CSV). The workbooks also hold verification events and review notes, and are not published.
- **Nigeria duplicates:** one public screenshot record duplicated a contributor's firsthand submission (`AF-SCAM-NG-REAL-0071`). The contribution is kept and the screenshot copy removed; its ID `AF-SCAM-NG-REAL-0010` is retired.
- **Out of scope:** eight screenshot records from outside Africa were removed and their IDs retired: `AF-SCAM-NG-REAL-0005`, `0058` and `0053` (US, US, Singapore), `0033`, `0046` and `0047` (Australia), `0057` (Philippines) and `0060` (India). Subtypes TAX-058 and TAX-065 now have no records but stay in the taxonomy.
- **Negative examples:** four screenshot records judged legitimate on review are kept with `fraud_status = not_scam` (`AF-SCAM-NG-REAL-0023`, `0029`, `0034`, `0048`). Filter them out when you need scam messages only.
- **Taxonomy:** 12 subtypes (TAX-057 to TAX-068) and one tactic (`religious_appeal`) were added from the Nigeria data, including BVN update phishing, fake bank credit alerts and fake password change alerts.

See [CHANGELOG.md](CHANGELOG.md) for changes.

## License

See [LICENSE](LICENSE).
