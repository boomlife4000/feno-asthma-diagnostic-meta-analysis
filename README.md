# feno-asthma-diagnostic-meta-analysis
For the multiple thresholds model meta-analysis 

PROSPERO: [CRD42023489738](https://www.crd.york.ac.uk/prospero/display_record.php?RecordID=489738)
DIVE cohort: [NCT05592519](https://clinicaltrials.gov/study/NCT05592519)

Each MasterData file contains one sheet per analysis subgroup. Sheets use a consistent structure with one row per study-cutoff combination:

| Column | Description |
|--------|-------------|
| `studylab` | Study identifier |
| `cutoff` | FeNO (ppb) or BEC (cells/µL) threshold |
| `TP` | True positives |
| `FN` | False negatives |
| `TN` | True negatives |
| `FP` | False positives |

**Step 1 — Meta-analysis** (`2026_04_02_All_table.R`):
- Fits a multiple-threshold diagnostic meta-analysis model via the `diagmeta` R package
- Computes sensitivity, specificity, AUC, LR+, and LR− at each integer cutoff
- Bootstraps 95% CIs for likelihood ratios (B = 500 iterations)
- Calculates PPV and NPV at four disease prevalence levels (20%, 40%, 56%, 67%)
- Exports results to `diagmeta_results_*.xlsx` (one sheet per subgroup)

**Step 2 — Figures** (`2026_04_02_All_plot.R`):
- Generates summary ROC (SROC) curves with confidence and prediction regions
- Creates PPV/NPV panels across prevalence levels with confidence intervals

To reproduce the analysis
Run:
```r
source("2026_04_02_All_table.R")  
source("2026_04_02_All_plot.R")   
```

Note: Bootstrap CIs (LR+, LR−) are stochastic (B = 500) and will vary slightly between runs

