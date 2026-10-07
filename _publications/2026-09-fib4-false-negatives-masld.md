---
title: "FIB-4 False Negatives in MASLD: Clinical Phenotypes and an Augmented Triage Model"
collection: publications
category: conferences
permalink: /publication/2026-09-fib4-false-negatives-masld
excerpt: 'In NHANES 2017–2020 data (N = 1,998), FIB-4 misses significant fibrosis in 16.6% of MASLD patients it classifies as low-risk, rising to 37.7% at BMI ≥ 40 kg/m². A supplementary model (FIB-4 Plus) outperforms the NAFLD Fibrosis Score (AUROC 0.837 vs. 0.749, DeLong p = 0.019). <b>Oral presentation; APASL International Travel Award.</b>'
date: 2026-09-18
venue: 'APASL Single Topic Conference (STC) 2026, Kumamoto, Japan (Oral Presentation)'
citation: 'M. A. Khan. (2026). &quot;FIB-4 False Negatives in MASLD: Clinical Phenotypes and an Augmented Triage Model.&quot; <i>APASL Single Topic Conference 2026</i>, Kumamoto, Japan. Oral presentation.'
---

**Selected for oral presentation; APASL International Travel Award.** Code: [github.com/MAUK9086/malsd_fib4](https://github.com/MAUK9086/malsd_fib4)

Background
------
The Fibrosis-4 index, FIB-4 = (age × AST) / (platelets × √ALT), is the guideline-recommended first-line screen for liver fibrosis in metabolic dysfunction-associated steatotic liver disease (MASLD). A value below 1.30 counts as low risk. FIB-4 relies on liver enzymes and platelet count, which can stay near-normal in a recognised obesity-driven phenotype (BMI ≥ 30 kg/m², ALT/AST < 40 U/L). As a result, its accuracy for early-to-moderate (F2+) fibrosis in this group is poorly characterised.

Methods
------
- **Cohort:** NHANES 2017–2020 adults who had vibration-controlled transient elastography (FibroScan), restricted to MASLD-eligible participants (final N = 1,998). Significant fibrosis was defined as liver stiffness ≥ 8.0 kPa.
- **False-negative analysis:** prevalence of elevated liver stiffness among FIB-4 low-risk patients, stratified by BMI, with sensitivity analyses on the stiffness cut-off and age range.
- **Drivers of misclassification:** gradient-boosted trees (XGBoost) with SHAP attributions across 40 clinical variables, plus unsupervised phenotyping (UMAP + k-means) of the false-negative group.
- **Augmented triage:** a logistic model, **FIB-4 Plus** (FIB-4 + BMI + waist circumference + Hepatic Steatosis Index), compared with the NAFLD Fibrosis Score (NFS) using DeLong's test.

Results
------
- FIB-4 missed F2+ fibrosis in **16.6%** (95% CI 13.5–20.0%) of patients it classified as low risk.
- The false-negative rate rose steeply with BMI: 5.1% (BMI < 25), 5.4% (25–30), 15.5% (30–40) and **37.7%** (≥ 40 kg/m²).
- Within the FIB-4 low-risk stratum, FIB-4 Plus reached **AUROC 0.837** (95% CI 0.773–0.898). This beat NFS (0.749; DeLong p = 0.019) and BMI alone (0.793).

<img src="/images/fib4-fn-rate-by-bmi.png" alt="FIB-4 false-negative rate by BMI group" width="80%">

*Figure 1. Share of FIB-4 low-risk MASLD patients with liver stiffness ≥ 8.0 kPa, by BMI group (NHANES 2017–2020).*

<img src="/images/fib4-plus-roc.png" alt="ROC curves for FIB-4 Plus, BMI only and NFS" width="70%">

*Figure 2. ROC curves within the FIB-4 low-risk stratum: FIB-4 Plus vs. BMI alone vs. NAFLD Fibrosis Score.*

Conclusion
------
In obese MASLD patients, a low FIB-4 does not reliably rule out significant fibrosis. Adding inexpensive body-measurement and steatosis markers to FIB-4 recovers much of the missed risk. This could support a second-line triage step before elastography.

Code snippet
------
```python
def compute_fib4(df: pd.DataFrame) -> pd.Series:
    """FIB-4 = (Age × AST) / (Platelets × √ALT)"""
    age = df["RIDAGEYR"]; ast = df["LBXSASSI"]
    alt = df["LBXSATSI"].clip(lower=0.01)
    plt = df["LBXPLTSI"].clip(lower=0.01)
    return (age * ast) / (plt * np.sqrt(alt))
```
