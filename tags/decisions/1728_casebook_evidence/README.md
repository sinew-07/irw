# Evidence accompanying the #1728 development casebook

These are exported summaries from the existing local audit and two preserved
2026-09-06 targeted-check runs. The handoff adds no new real-table validator run.
See [the casebook](../1728_development_casebook.md) for the questions, judgments,
actions and known limits, including dated follow-ups.

## Files and scope

- `validator_comparison.csv`: 38 profile observations from 19 selected-check
  calls, including calls with no finding. It is not 38 independent alerts or
  a full CLI validation of any table. Profiles are `triage` and `upload`,
  both with `strict=false`; `target_check_blocking` concerns only the selected check.
- `human_claims.csv`: the existing 21 scoped assessments across eight case groups,
  with their historical evidence scope and subsequent notes. These are not
  independent reference labels; no source-reading times or independent reviews
  are inferred from the recorded assessment time.
- `su_distributions.csv`: complete observed item-response marginal counts for
  the four Su scales, before and after the audited conversion.
- `su_old_reproduction.csv`: the archived incomplete/full-script comparison;
  the missing-call defect has since been repaired and merged in #1993.
- `su_rt_summary.csv`, `su_identity.csv`, `su_closeout.json`: archived RT/alignment,
  source-file identity and fresh-directory conversion summaries. The aggregate
  files report prior audit findings; they do not reproduce the underlying keyed
  participant-level comparison by themselves.
- `nguyen_marginals.json`: per-item response counts and the workbook's documented
  MSPSS permitted set. Questionnaire wording is omitted. Expanding these counts
  produces artificial pairings and cannot establish participant alignment,
  correlations or joint missingness. Barthel's observed sets are not a codebook.

## Pinned versions and sources

- Baseline: `847b7b628f06714f4970fc17fd453cfd8585eac0`.
- Candidate: `4f3ccfcb920e7491cb34a2e5f10bf3c06d169ecb` from
  [#1697](https://github.com/ben-domingue/irw/pull/1697).
  These are comparison snapshots, not a claim about current main.
- Su et al. (2024), *Temporal dynamics in psychological assessments: a novel
  dataset with scales and response times*, Scientific Data 11, 1046:
  [paper](https://doi.org/10.1038/s41597-024-03888-8),
  [data release](https://zenodo.org/records/10423537), CC BY 4.0.
  RT units: paper Table 1, PDF page 3; precision: Methods, Data generation process.
- Nguyen data: [Dataverse version 1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/X2C2PL&version=1.0),
  workbook `gycosurganx_data_censored.xlsx`, file ID 14113156, deposit CC0.
  `codes!B32:B38`, list `likertmspss`, provides 1–7; `vars!B24:B35`
  identifies the MSPSS items. The inspected workbook did not give exhaustive
  permitted sets for each Barthel item.

This is a readable documentation/evidence handoff, not a standalone distribution
of the complete original audit or replay environment. It contains neither raw
participant records nor copied papers. The complete local audit remains archived.
Neither these selected historical cases nor the synthetic appendix estimates a
corpus false-positive rate, sensitivity, accuracy or time saving.
