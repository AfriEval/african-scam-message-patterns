# Privacy and Consent

## Redaction

Before any record enters the dataset, remove or replace:

- phone numbers → `[PHONE]`
- live URLs → `[LINK]`
- bank, paybill and till numbers → `[Account Number]`, `[Paybill Number]`
- names of private individuals, schools, estates or businesses that could identify the contributor
- national ID, KRA PIN or similar identifiers

Also review indirect identifiers: a combination of location, institution and date can identify a contributor even after direct identifiers are removed (RULE-005).

## Consent

Real-world messages are accepted only from the person who received them, with their informed consent to inclusion. Contributors may withdraw a record at any time; withdrawn records are removed in the next release and listed in the CHANGELOG by ID only.

## Release

- Synthetic records may be published once reviewed.
- Real-world records remain restricted until rights, consent or lawful basis, and privacy reviews have passed (RULE-009).
- Verification events contain contributor statements and stay restricted. They are not published in this repository.

## Reporting a problem

If you find personal data in this dataset, open an issue without quoting the data, and the record will be removed.
