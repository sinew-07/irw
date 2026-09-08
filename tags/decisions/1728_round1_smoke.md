# #1728: published-table CLI smoke, 2026-09-09

The mechanism smoke is complete: three full published tables, each run through
the actual CLI separately under `triage` and `upload`. All six runs completed
without input failures, timeouts or size downgrades. This is a convenience smoke
set, not the formal sweep or a statistical sample; no TP/FP labels or rates have
been assigned.

## Inputs and execution

Code: [`de4155b83d59451b9fc3ecabd161688bbef70521`](https://github.com/ben-domingue/irw/tree/de4155b83d59451b9fc3ecabd161688bbef70521),
unmodified validator. The source hashes, Python/dependency versions, timestamps,
input hashes and full aggregate CLI reports are in [the evidence JSON](1728_round1_smoke.json).
Only local filesystem prefixes were removed from report labels in this public
copy; complete original stdout/stderr remain in the local audit record.

The six recorded core releases list **4,238 tables and 4,237 distinct names**.
`zhou_2025_peer_relationship` occurs in shards 3 and 5; both references are retained.
The ordinary client resolves newest shard first. No table was exported from the
local `data/pub/` archive, a draft version, or a row sample.

| Table | Released shard version | Full rows | triage | upload |
|---|---|---:|---|---|
| `nguyen_2026_barthel` | warehouse 4, v6.0 | 3,940 | 1 error, 1 warning | 2 warnings |
| `nguyen_2026_mspss` | warehouse 4, v6.0 | 4,728 | 1 error | 1 warning |
| `su_2024_gad7` | warehouse 5, v2.0 | 170,044 | 1 warning | 1 warning |

The genuine command was run once per table/profile:

```sh
python -m irw_validate.cli TABLE.csv --profile triage --json
python -m irw_validate.cli TABLE.csv --profile upload --json
```

No strict mode, overrides, recoding, row filtering or validator modifications.
`IRW_COV_RANGE_SEVERITY=error` was fixed. The two triage exit codes of 1 are
completed inspections with error findings, not failed executions.

## Input fidelity

Published CSV export bytes were preserved. An additional full typed Arrow read
was compared with the CSV loader result for each profile using complete row
multisets, preserving duplicate multiplicity and participant–item–field pairing.
All **178,712 records** matched; published variable order and full row counts also
matched. All columns in these three tables have zero nulls or empty strings;
the floating RT column has zero NaNs. Diagnostic and CLI Python/pandas versions
match. Independent server reads are not assumed to share row order.

Storage types are recorded separately: numeric value equality does not establish
storage-type equivalence. This verification covers these three tables only;
CSV inference, literal NA tokens, leading zeros, nullable values and files above
the CLI's 512 MiB limit still require coverage accounting in the formal run.

## What follows

The `resp_scale_mixed` findings on Barthel and MSPSS are errors in triage and
warnings in upload. The concentration warnings remain observations, not proof
of imputation. These are recorded CLI outputs, not newly adjudicated labels.

Next, confirm the formal version stamp and check list with Ben. Then construct
the full eligible finding frame and take seeded samples of up to 15 per
`(profile, check, effective severity)` cell. Keep unresolved judgments and
execution/coverage failures explicit, and define the check's adjudicated claim
separately from whether it should block uploads. Item-text mapping remains
outside round one. No gate policy or published data has been changed.
