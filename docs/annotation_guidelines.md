# Annotation Guidelines

## Rules

| ID | Dimension | Rule |
|---|---|---|
| RULE-001 | Origin | Keep synthetic and real-world provenance separate; synthetic is never marked verified. |
| RULE-002 | Evidence | Do not accept source fraud-status claims without supporting verification evidence. |
| RULE-003 | Status | `unassessed` means the original evidence is missing or inadequate; it does not mean legitimate. |
| RULE-004 | Verification | Report direct owner/management confirmation as contributor-reported unless independently reviewed. |
| RULE-005 | Privacy | Remove live URLs, personal identifiers and financial account details before public release; review indirect identifiers. |
| RULE-006 | Taxonomy | Use category → scam_type → subtype; keep tactics, claimed identity and action independent. |
| RULE-007 | Language | Do not automatically infer code-mixing/switching from two language tags; request language review. |
| RULE-008 | Duplicates | Review exact duplicate texts; preserve provenance and do not count duplicates as independent incidents. |
| RULE-009 | Public release | All real-world records remain restricted until rights, consent/lawful basis and privacy reviews pass. |

## Assigning a subtype

1. Read the full message and identify the core request.
2. Pick the single best-fitting subtype in `taxonomy/scam_taxonomy.csv` using its `working_definition`. Assign a subtype only when the message evidence supports it; do not infer confirmed fraud from wording alone.
3. Copy `category`, `scam_type` and `subtype` exactly from the taxonomy row.
4. Use `TAX-012` (Uncontextualized payment instruction) only as a last resort. A high usage rate signals a missing subtype.

## Tactics, identity and action

- Tag every tactic present, using the `tactic` values in `taxonomy/tactics.csv`, separated by `; `.
- `claimed_identity` is who the sender says they are, not who they actually are.
- `requested_action` is what the recipient is asked to do, e.g. `Open link`, `Pay fee`.

## Open taxonomy questions

| Rows | Note |
|---|---|
| TAX-001 / TAX-002 | TAX-001 is a fake incoming transfer; TAX-002 is a claim that the recipient's own payment went astray. Confirm this matches intent. |
| TAX-013 / TAX-047 | Same intent (urgent money from a "known person") split across Account impersonation and Social impersonation. Consider one category, distinguished by hijacked account vs new number. |
| TAX-016 / 017 / 019 / 020 | Close neighbours, separated by framing: suspension threat (mobile money vs bank), support-agent persona, routine KYC. Needs a calibration round. |
| TAX-018 / TAX-036 | TAX-018 is under "Loyalty reward lure", TAX-036 under "Reward phishing". Consider aligning. |
| TAX-009, TAX-049 vs TAX-052 to 054 | Two education categories exist ("Education payment fraud" and "Education fraud"). Merge or document the difference. |
| TAX-007 | Task-based scams sit under Employment fraud; some taxonomies treat them as investment fraud. |
| TAX-026 | Utility disconnection sits under Housing fraud; could fit Government impersonation or a utility category. |
| TAX-012 | Strict fallback; track usage rate. |
| `annotation_rule` column | Identical on every taxonomy row; could be removed in favour of these guidelines. |
