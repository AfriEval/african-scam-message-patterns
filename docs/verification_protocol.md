# Verification Protocol

Verification establishes whether a real-world message was a fraudulent request. It applies only to `real_world` records; synthetic records are `not_applicable`.

## Verification events

Each verification is logged as a separate event, kept outside the public dataset with `restricted` visibility. An event records:

| Field | Description |
|---|---|
| `verification_id` | `VER-NNNN` |
| `observation_id` | Record being verified |
| `verification_method` | How the check was done (see below) |
| `verification_status` | Outcome state of the check |
| `reported_finding_or_missing_evidence` | What was found, or what evidence is missing |
| `verification_limitations` | Known weaknesses of the check |
| `resulting_fraud_status` | `fraud_status` this event supports |
| `visibility` | `restricted` or `public` |

## Methods

| Method | Meaning |
|---|---|
| `contributor_reported_checks` | The contributor reports their own checks, e.g. they have no children at the named school, or the company does not exist. |
| `account_owner_confirmation_reported` | The owner of an impersonated or compromised account reportedly confirmed they did not send the request. |
| `property_management_confirmation_reported` | Genuine property management reportedly denied authorising changed payment instructions. |

Per RULE-004, owner or management confirmations are recorded as contributor-reported unless independently reviewed.

## Status values

| `verification_status` | Meaning |
|---|---|
| `not_applicable` | Synthetic record |
| `completed_reported` | A check was completed and reported by the contributor |
| `not_documented` | No verification evidence was supplied |

## Setting `fraud_status`

- `verified_fraudulent_request`: at least one completed verification event supports it.
- `suspected_fraud`: the message shows risk indicators but is not verified (all synthetic records).
- `unassessed`: evidence is missing or inadequate. This is not a finding of legitimacy.
- `not_scam`: a reviewer judged the message legitimate (for example, an operator promotion that asks for nothing). Leave `taxonomy_id` empty.

Never copy a fraud status from a source spreadsheet without supporting evidence (RULE-002).
