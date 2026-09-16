# PFSP Computational Reproducibility Archive

This archive accompanies the manuscript:

**Learning from Random Solutions: Data-Mining-Guided Heuristic Search for Permutation Flow Shop Scheduling**

## Scope

The archive supports the confirmatory 140-instance random-pool mining study, the 28-problem native external-comparator panel, the representative runtime audit, and the separate five-target exploratory transfer analysis in which mined structural information is integrated directly into QIG and Q-NEH through architecture-compatible interfaces.

The native external-comparator panel and the exploratory transfer study answer different questions. The native panel provides absolute-quality context and shows that QIG and Q-NEH remain stronger solvers in their native forms. The exploratory transfer study asks whether the mined P/R information itself can also assist those stronger algorithms. The five targets were selected only from the already-frozen native-comparator results, before any transfer outcome was observed. The development cases were Ta50x10 #1 (worst QIG mean RPD), Ta50x20 #1 (second-worst QIG mean RPD), and Ta100x20 #1 (worst Q-NEH and third-worst QIG mean RPD). Two additional holdouts were frozen before development execution: Ta100x20 #10 (the next-worst non-development Taillard QIG case) and VFR100x40 #10 (the worst non-development VFR QIG case). Thus, the five-instance panel is a deliberately difficult exploratory stress test rather than a representative sample, and no target was added, removed, or replaced because of transfer outcomes. Its selected-interface results are favorable on all five targeted instances for both comparators, whereas the uniform strict H=10 amortized-cost audit retains favorable problem-mean effects on 3/5 QIG targets and 4/5 Q-NEH targets. The strict-cost aggregate evidence is mixed and does not establish a general transfer advantage; the follow-up is retained as exploratory mechanism evidence.

## Contents

- `Supplementary_Material.docx` — reader-facing Supplementary Material, Sections S1-S7 and Tables S1-S8.
- `PFSP_Supplementary_Tables_FINAL.xlsx` — machine-readable reader-facing versions of Tables S1-S8 cited in the manuscript.
- `PFSP_AllProblems_AllResults.xlsx` — consolidated manuscript-facing problem-level and aggregate results.
- `PFSP_ComparatorMining_Exploratory_Transfer_Tables.xlsx` — reader-facing target-selection rationale, selected-interface results, strict H=10 audit, paired summaries, and development-lineage tables for the five-target QIG/Q-NEH transfer analysis.
- `PFSP_Code_Robustness_Stability.zip` — code for P/R ablation, weight sensitivity, OFAT robustness, and five-pool structural stability.
- `PFSP_Results_Robustness_Stability.zip` — raw/master results, structural archives, QA evidence, and publication summaries.
- `PFSP_External_Comparator_Results.zip` — code and outputs for the 28-problem Q-NEH/QIG native external-comparator panel and common local-search analysis.
- `PFSP_Runtime_Results.zip` — runtime scripts, wall/CPU logs, environment metadata, run manifest, and historical audit.
- `PFSP_Pure_Python_Single_Instance.zip` — portable single-instance reference implementation and validation aid. (The run_pfsp_single.py Python code, located in this zip file, performs the quality assurance (QA) checks for the solutions obtained for the problems presented in the article using a specified initial random seed.)
- `PFSP_ComparatorMining_Exploratory_Transfer_Reproducibility.zip` — full five-target QIG/Q-NEH exploratory-transfer archive, including source code, frozen protocols, paired seeds/raw outputs, selected and unsuccessful intermediate variants, QA files, and integrated synthesis records.
- `SHA256SUMS.txt` — SHA-256 checksums for all top-level files in this archive.

## Seed-level reproducibility

The main random-pool experiments include **700 recorded pool seeds** (140 benchmark instances x 5 independent pools), together with PCG64 random-number-generator state information. The native external-comparator experiments include **280 recorded seeds** (28 problems x 10 independent replications). The exploratory QIG/Q-NEH transfer archive preserves its paired validation seeds and complete development lineage.

## QA boundary

Instrumented runtime reruns are used for computational-cost accounting only and do not replace the frozen Cmax results used for solution-quality analyses. The historical runtime audit documents environment-sensitive Elite/Poor membership differences at equal-Cmax boundaries under NumPy `quicksort`.

The five-target comparator-transfer analysis is exploratory and is kept separate from the confirmatory 28-problem native-comparator panel. Target identities were frozen from native-comparator difficulty before transfer outcomes, and no target was added, removed, or replaced afterward. Unfavorable and abandoned interface variants are retained in the transfer reproducibility archive rather than removed after selection.

## Public-facing nomenclature

Public package names, documentation, code identifiers, and provenance labels use analysis-specific terminology such as ablation, weight sensitivity, OFAT robustness, structural stability, external comparison, and exploratory transfer. This terminology corresponds directly to the scientific analyses described in the manuscript and Supplementary Material.
