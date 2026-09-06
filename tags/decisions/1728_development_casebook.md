# Development casebook for #1728

**Status: existing development material shared for discussion, 2026-09-07.**
These are six retrospective cases from two source families, Su and Nguyen,
followed by two synthetic regression cases. They are not eight independent
datasets, an independent benchmark, accepted repository policy, or a completed
corpus triage pass. Selection followed earlier audits and validator development;
the cases cannot estimate accuracy or corpus failure rates.

This shares the existing material requested in
[Ben's #1728 reply](https://github.com/ben-domingue/irw/issues/1728#issuecomment-5560926244).
The next real-table set and check/profile scope remain to be agreed with Ben.
Synthetic examples will not enter that pass's empirical denominators.

The [evidence README](1728_casebook_evidence/README.md) describes the accompanying
files. [Human claims](1728_casebook_evidence/human_claims.csv) preserve 21 scoped
judgments explicitly endorsed by Sinew on 2026-09-06. Endorsement is not a claim
of independent, blinded source review; personal source-inspection details and
review duration were not reported. Historical judgments and subsequent workflow
updates are distinguished below.

## What the saved checks cover

[Validator comparisons](1728_casebook_evidence/validator_comparison.csv) contain
38 profile observations from 19 targeted check calls, including cases where no
finding was emitted. They compare baseline `847b7b628f06714f4970fc17fd453cfd8585eac0`
with [#1697](https://github.com/ben-domingue/irw/pull/1697) candidate
`4f3ccfcb920e7491cb34a2e5f10bf3c06d169ecb`, using `triage` and `upload`,
`strict=False`. These are pinned historical revisions, not a claim about current
main. This was a bounded replay using aggregates and synthetic inputs, not a
full CLI run on each original table.

Raw check status and effective profile severity are separate. In the baseline,
`resp_scale_mixed=fail` became an error under `triage` but a warning under
`upload`. Consequently, the comparison does not show that width differences
previously blocked uploads. No emitted finding is not whole-table certification.
Marginal replays cannot verify participant-item alignment or joint distributions.

## 1. Su: category concentration and its interpretation

**Situation.** Three Su items triggered possible-imputation warnings because one
response category exceeded 60%.

**Evidence.** [Full marginal distributions](1728_casebook_evidence/su_distributions.csv)
show identical raw and converted counts. The dominant value is zero:
GAD_1 has 15,687/24,292 (64.5768%); ISI_1 has 17,036/24,292 (70.1301%);
PHQ_3 has 15,558/24,292 (64.0458%). The saved check emits advisory warnings in
both tested profiles. These three related observations form one case.

**Judgment and action.** The distributional feature is real; the audited
conversion did not introduce it. Retain the responses and document the warning.
Category concentration alone does not establish mean imputation, so the
observation and its proposed causal explanation should not receive one
undifferentiated true/false label.

**Limits.** Processing before the deposited exports remains unverified. This
is a known provenance limit, not a new work item. Source preservation does not
establish the validity of every response.

## 2. Su: a successful process exit with missing outputs

**Situation.** The historical repository converter exited successfully while
producing only PHQ-9. The expected GAD-7, ISI, PSS-14 and QC outputs were absent.

**Evidence.** The [archived reproduction comparison](1728_casebook_evidence/su_old_reproduction.csv)
records expected filenames, production status, exit codes and hashes for the
incomplete repository script and complete local script. The
[closeout summary](1728_casebook_evidence/su_closeout.json) records four response
CSVs plus a separate QC summary, with matching output contents.

**Judgment and action.** This was a real completeness defect: exit code zero
was insufficient evidence of reproduction. Restore the missing calls, retain
the existing response data, and place QC under `output/qc/`.

**Follow-up.** Ben merged [#1993](https://github.com/ben-domingue/irw/pull/1993)
on 2026-09-06 at 03:40:57 UTC. Four missing Su core Dictionary entries were then
added, and a saved online read at 04:12:35 UTC verified them. These are completed
steps, not open repair requests. Dictionary completion alone does not establish
later biblio, Tags or publication state.

**Limits.** This case uses archived reproduction evidence; the casebook replay
did not freshly rerun the R conversion. QC is not a fifth response table.

## 3. Su: response-time units

**Situation.** Review asked whether the released times required division by
1,000 before use as seconds.

**Evidence.** [Su et al.](https://doi.org/10.1038/s41597-024-03888-8), Table 1,
defines the four files' `timeX` fields in seconds; Methods describes two-decimal
precision. [File identity checks](1728_casebook_evidence/su_identity.csv) match
all five local input sizes and MD5 values to
[Zenodo record 10423537](https://zenodo.org/records/10423537).
[Pooled item-time medians](1728_casebook_evidence/su_rt_summary.csv) are GAD-7
2.20, ISI 2.65, PHQ-9 3.00 and PSS-14 3.22 seconds.

**Judgment and action.** Preserve seconds; do not divide by 1,000. The unit
decision rests on source documentation and file identity, not numerical
plausibility alone. The historical personal-review record was conditional on
unreported source inspection; this does not reopen the unit question resolved
in the merged PR.

**Limits.** Correct units do not establish attention or measurement validity
for zero and long-tail times. Separately, released PSS values are 1–5; the
supplement's scoring description does not establish a storage-to-scoring
mapping. Preserve those codes without inferring subtraction or reverse scoring.

## 4. Nguyen Barthel: unequal observed supports

**Situation.** Ten Barthel items have different observed response widths.

**Evidence.** [Saved marginals](1728_casebook_evidence/nguyen_marginals.json),
from [dataset version 1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/X2C2PL&version=1.0),
contain 394 responses per item, 3,940 total. Two observed intervals are 0–5,
six 0–10 and two 0–15. Mobility observes 0, 10 and 15, not 5. The available
workbook does not establish exhaustive item-specific permitted sets.

**Judgment and action.** Width differences alone do not establish invalid
codes or different constructs. Preserve values and treat the candidate's
nested-support finding as advisory. Complete permitted-value acceptance would
require the study-specific item categories.

**Limits.** This accepts the insufficiency of width evidence, not the legality
of every value. Neither observed categories nor a generic Barthel form can
substitute for this study's codebook. Marginal agreement does not establish
participant alignment.

## 5. Nguyen MSPSS: a permitted category goes unused

**Situation.** Four MSPSS items observe 1–7; eight observe 2–7.

**Evidence.** All twelve have 394 responses, 4,728 total, in the
[marginals](1728_casebook_evidence/nguyen_marginals.json).
The [source workbook](https://dataverse.harvard.edu/api/access/datafile/14113156)
explicitly lists 1–7 in `codes!B32:B38`, list `likertmspss`. Every observed
response belongs to that set. The pinned candidate emits a width warning
without documentation and suppresses that finding when supplied the documented
set.

**Judgment and action.** Accept this permitted-category claim and retain all
responses. Absence of observed ones does not imply another scale or require
manufacturing missing categories.

**Limits.** The code list settles membership only. It does not validate every
field, scoring practice, upstream process or psychometric property.

## 6. Nguyen metadata: presence versus meaning

**Situation.** A saved 2026-09-05 23:07:39 UTC snapshot contained all five
Nguyen Dictionary and Tags rows, after an earlier missing-row gap.

**Evidence and judgment.** The [recorded claims](1728_casebook_evidence/human_claims.csv)
distinguish row completeness from semantic review. In that snapshot, Barthel's
construct needed Physical health/functioning and GAD-7 needed Affective/mental
health. Barthel's Survey/questionnaire administration claim lacked study-specific
support. Clinical-only sample labels and ISI's mental-health-only classification
were defensible narrower choices; differences from a proposal were not all
errors.

**Action and limits.** Retain defensible choices and check current state before
any further edit. This is a historical decision record, not evidence that those
cells remain wrong, that all metadata are now correct, or that generated
metadata have been published. Source author, depositor and reconstruction
contributor are distinct roles.

## Appendix: two synthetic regression cases

**A. Mixed format.** A single construct was stipulated for three MC/CR
fixtures: 20:5, 5:20 and 5:5 items. The candidate produced a nested-support
warning across all three; the baseline emitted its mixed-scale finding only
for 20:5. Retain this as a regression example showing why majority composition
should not by itself decide invalidity. It establishes neither arbitrary
composition invariance nor anything about real corpus rates.

**B. Documented boundary.** Two synthetic frames contain `{1,7}` and `{1,8}`,
with 60 responses at each value and supplied allowed values 1–7. The candidate
emits no permitted-range violation for 7 and a blocking `resp_outside_permitted`
error for 8 under both tested profiles. This establishes behavior against a
stipulated contract, not an empirical codebook finding. It does not authorize
silent correction or deletion of real records.

Both remain separate regression documentation. The proposed real-table triage
pass, its population and its denominators have not yet been agreed or executed.
