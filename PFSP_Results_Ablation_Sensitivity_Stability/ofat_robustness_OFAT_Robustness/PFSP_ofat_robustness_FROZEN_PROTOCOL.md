# PFSP Applied Sciences Revision — OFAT-robustness analysis Frozen OFAT Robustness Protocol

Frozen before inspection of any OFAT-robustness analysis result.

## Purpose
OFAT-robustness analysis evaluates whether the main conclusions are robust to other fixed hyperparameter choices. It is a one-factor-at-a-time (OFAT) robustness study, not retuning or optimization.

## Pre-specified problem subset
Use the same 28 result-independent problems as weight-sensitivity analysis: problem #1 and #10 from each of the 14 benchmark-size groups.

## Common settings
- Same five historical pool seeds per problem.
- Uniform random pools, S = 10000n.
- Same five manuscript heuristic families.
- Elite-only and Contrast mining modes.
- Fixed P/R weighting: wP = 0.65, wR = 0.35.
- No adjacency information.
- No post local search.
- Historical tie/cutoff compatibility rules retained.
- Every replication must reproduce the historical final-protocol baseline (5% Elite, 10% Poor, top 3n P, 4 regions, q=4) in all 10 mining×family cells before any OFAT-robustness analysis variation is accepted.

## OFAT configurations
Baseline: Elite 5%, Poor 10%, top P = 3n, regions = 4, q = 4.

Only one factor changes at a time:
1. Retained P relationships: 2n, 3n (baseline), 4n.
2. Number of R regions: 2, 4 (baseline), 8.
3. Additional information-guided candidates q: 2, 4 (baseline), 6.
4. Elite fraction: 2.5%, 5% (baseline), 10%.
5. Poor fraction: 5%, 10% (baseline), 20%.

This yields 11 unique configurations including the single shared baseline. Poor-fraction variation affects Contrast mining; Elite-only is expected to remain unchanged because the Poor stratum is not used by the Elite-only definition, but those rows are retained for a rectangular audit trail.

## Interpretation guardrail
Do not choose a new parameter setting from OFAT-robustness analysis. The analysis asks whether conclusions are stable around the fixed main-study configuration. No OFAT-robustness analysis result may be interpreted until all 28×5 replications pass master QA.
