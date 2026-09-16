# PFSP Applied Sciences Revision — OFAT-robustness analysis Final OFAT Robustness Report

## Status
OFAT-robustness analysis is complete. The frozen OFAT design used the same 28 result-independent problems as weight-sensitivity analysis (problem #1 and #10 from each of 14 groups), five historical pools per problem, the fixed P/R weight 0.65/0.35, and 11 unique configurations including the single shared baseline. No OFAT-robustness analysis result was inspected for parameter selection before the protocol was frozen.

Master QA: **GREEN**.

- 28 problems × 5 pools = 140 accepted replications.
- 15400 raw heuristic outcomes (11 configs × 2 mining modes × 5 families per replication).
- Historical baseline regression: 1400/1400 exact PASS.
- ablation analysis P+R cross-check: 1400/1400 exact Cmax+sequence matches.
- Independent solution QA: 0 invalid permutations; 0 Cmax mismatches.
- Seed/pool mismatches: 0; duplicate raw/pool/audit keys: 0/0/0.

An optimized cumulative-statistics implementation was used for the final 200-job block. It was cross-validated against the earlier implementation on n=20, n=100, and n=200 cases; the explicit n=200 validation reproduced all 110 OFAT Cmax/sequence cells exactly.

## Mean-of-Five robustness summary
Positive Δ% means that the alternative setting produced a lower Mean-of-Five Cmax than the frozen baseline; negative values mean deterioration. W/T/L is computed over the 280 Problem × Mining × Family Mean-of-Five cells for each alternative.

| Alternative | Mean Δ% | Median Δ% | Mean |Δ|% | W/T/L |
|---|---:|---:|---:|---:|
| Top P = 2n | -0.0019 | +0.0000 | 0.1375 | 93/86/101 |
| Top P = 4n | +0.0307 | +0.0000 | 0.1722 | 112/74/94 |
| R regions = 2 | -0.0047 | +0.0000 | 0.3428 | 119/31/130 |
| R regions = 8 | -0.0125 | +0.0000 | 0.3155 | 129/29/122 |
| q = 2 | -0.0807 | +0.0000 | 0.1621 | 31/172/77 |
| q = 6 | +0.0379 | +0.0000 | 0.0909 | 65/176/39 |
| Elite = 2.5% | -0.0138 | +0.0000 | 0.1439 | 106/69/105 |
| Elite = 10% | +0.0042 | +0.0000 | 0.1102 | 99/86/95 |
| Poor = 5% | -0.0060 | +0.0000 | 0.0506 | 43/188/49 |
| Poor = 20% | -0.0048 | +0.0000 | 0.0639 | 52/184/44 |

## Scientific reading
The frozen main configuration is broadly insensitive to the local OFAT perturbations of retained P-rule count, R-region count, Elite fraction, and Poor fraction. Their mean changes relative to the baseline are only a few hundredths of a percent, with no consistent directional deterioration across the 28-problem panel. This supports describing these settings as a common fixed protocol rather than as instance-specific tuned parameters.

The clearest sensitivity is q, the number of additional information-guided reinsertion candidates. Across all five families, q=2 changes Mean-of-Five performance by -0.0807% on average, whereas q=6 changes it by +0.0379%. Because q does not affect the three purely constructive families, the effect is concentrated in FRB4-p1 and INEH-inspired: within those search-guided families the corresponding mean changes are -0.2017% and +0.0948%. Thus q controls search breadth in the expected direction and should not be described as completely insensitive.

Poor-fraction perturbations affect Contrast mining only; Elite-only is definitionally unchanged. The QA check confirmed 1400/1400 exact Elite-only invariance comparisons. Within Contrast alone, changing Poor from 10% to 5% or 20% changes Mean-of-Five Cmax by only -0.0120% and -0.0096% on average, respectively.

The region alternatives show near-zero average shifts but larger cell-level dispersion than the other non-q factors. This indicates heterogeneous instance-level responses even when the aggregate effect is small. Detailed loss-case and distributional inference should therefore remain deferred to analysis phase 9 rather than being inferred from OFAT-robustness analysis alone.

OFAT-robustness analysis is a robustness analysis, not a tuning exercise. In particular, the small numerical advantage of q=6 or Top P=4n is not used to replace the frozen baseline. The publication claim should be that the main protocol is broadly robust over the tested neighborhoods, while q is a detectable search-intensity parameter and 0.65/0.35, 3n, four regions, q=4, 5% Elite, and 10% Poor remain the pre-specified common baseline.

## Reviewer linkage
These results directly strengthen Reviewer 2’s request for sensitivity evidence on the four-region representation and the other fixed hyperparameters, and Reviewer 1/Reviewer 3 concerns about whether the main configuration was arbitrarily imposed. Final inferential tests, effect sizes, confidence intervals, distribution plots, and loss-instance analysis are intentionally reserved for analysis phase 9, where the unit of analysis and multiplicity scope will be frozen together.

## SHA-256
- `ofat_robustness_ofat_raw.csv`: `9d5ed08eccccb7170affb96fc8c31c87e284aee54e392ac2d29fbf132bd7e254`
- `ofat_robustness_pool_audit.csv`: `9bc123b3f20c044f1933b6ca6dee14e35791810803da7ebe07d2688853c21a77`
- `ofat_robustness_baseline_regression_audit.csv`: `419d0c9b54bd0500dbe5726d7800d43e98c7952107a39e1a474de1c48d513446`

## Next analysis phase
structural-stability analysis: five-pool structural stability (P-rule overlap/Jaccard, P-score correlation, R stability, and guided-output variability), with full P/R structures saved for publication-grade stability analysis.