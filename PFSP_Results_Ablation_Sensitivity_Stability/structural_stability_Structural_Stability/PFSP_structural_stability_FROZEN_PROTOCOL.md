# PFSP Applied Sciences Revision — structural-stability analysis Frozen Protocol

## Purpose
structural-stability analysis quantifies the five-pool structural stability of the mined P/R information under the unchanged manuscript protocol. It is a robustness/stability analysis, not a tuning analysis phase and does not alter any ablation, weight-sensitivity, and OFAT-robustness analyses decision.

## Scope
- All 140 benchmark problems (110 Taillard + 30 VFR).
- The same five historical pool seeds per problem used in the main experiment.
- Uniform random permutation pools, S = 10000n.
- Elite = best 5%; Poor = worst 10%.
- Four relative-position regions.
- P sparsification = top 3n unordered job pairs, using the historical `np.argpartition` selection semantics.
- Mining modes: Elite-only and Contrast.
- Main guided-output variability is evaluated for the historical P+R arm (wP,wR)=(0.65,0.35), q=4, five manuscript heuristic families, no post-LS.

## Saved structural objects per problem × replication × mining mode
For every pool, save the complete (unsparsified) score representations needed for stability analysis:
- P score vector over the upper triangle (i<j):
  - Elite-only: Pr_Elite(i precedes j) - 0.5
  - Contrast: Pr_Elite(i precedes j) - Pr_Poor(i precedes j)
- R score matrix (n × 4):
  - Elite-only: Pr_Elite(job i in region r) - 0.25
  - Contrast: Pr_Elite(job i in region r) - Pr_Poor(job i in region r)
- Historical top-3n P support and the sign/direction of each retained rule.

## Five-pool structural stability metrics
There are C(5,2)=10 pool-pair comparisons per problem and mining mode.

### P stability
1. **Top-P support Jaccard**: |A∩B| / |A∪B|, where A and B are the retained top-3n unordered pair supports.
2. **Top-P directional agreement**: among rules retained in both pools, proportion with the same score sign/direction. If the support intersection is empty, this metric is NA.
3. **Signed-rule Jaccard**: Jaccard after treating (unordered pair, sign) as the rule identity.
4. **P-score Pearson correlation** across all unsparsified upper-triangle scores.
5. **P-score Spearman correlation** across all unsparsified upper-triangle scores.

### R stability
6. **R-score Pearson correlation** after flattening the n×4 score matrix.
7. **R-score Spearman correlation** after flattening the n×4 score matrix.
8. **R-score MAE** between the two n×4 score matrices.
9. **Preferred-region agreement**: proportion of jobs whose deterministic argmax region is the same in both pools.

No arbitrary pass/fail threshold is imposed on these continuous stability metrics; analysis phase 9 will handle inferential/statistical interpretation.

## Guided-output variability (from the already QA-clean ablation analysis P+R results)
For each problem × mining mode × heuristic family over the five historical pools, report:
- Mean Cmax
- Sample SD
- CV% = 100×SD/Mean
- Range = max-min
- Relative range% = 100×(max-min)/Mean
- Number of distinct Cmax values
- Number of distinct final permutations

Summaries are produced overall and by benchmark-size group, with mean, median and IQR of problem-level stability/variability measures.

## QA / regression gates
A structural-stability analysis replication is accepted only if:
1. Problem ID, n, m, seed and pool size match the frozen manifests.
2. Regenerated pool Best/Mean/SD/Worst match the authoritative ablation analysis pool audit (integer extrema exactly; floating summaries to numerical tolerance).
3. The mined historical P+R structures reproduce all 10 ablation analysis P+R Cmax cells exactly (2 mining modes × 5 families).
4. Saved score arrays have the expected dimensions and finite values.
5. Top-P support size is exactly min(3n, n(n-1)/2) for each mining mode.

## Reporting rule
structural-stability analysis is descriptive structural robustness evidence. It does not retune P/R weights, top-P, region count, q, Elite fraction or Poor fraction, and it does not replace the analysis phase 9 inferential analysis.
