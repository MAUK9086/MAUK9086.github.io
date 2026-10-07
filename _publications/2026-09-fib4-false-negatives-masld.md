---
title: "FIB-4 False Negatives in MASLD: Clinical Phenotypes and an Augmented Triage Model"
collection: publications
category: conferences
permalink: /publication/2026-09-fib4-false-negatives-masld
excerpt: 'Among MASLD patients classified as low-risk by FIB-4 (NHANES 2017–2020), 16.6% had significant (F2+) fibrosis, rising to 37.7% at BMI ≥ 40 kg/m². A supplementary model, FIB-4 Plus, outperformed the NAFLD Fibrosis Score (AUROC 0.837 vs. 0.749, DeLong p = 0.019). <b>Oral presentation; APASL International Travel Award.</b>'
date: 2026-09-19
venue: 'APASL Single Topic Conference (STC) 2026, Kumamoto, Japan. Oral presentation FP5-2'
slidesurl: '/files/APASL_STC2026_FP5-2_slides.pdf'
citation: 'M. A. Khan. (2026). &quot;FIB-4 False Negatives in MASLD: Clinical Phenotypes and an Augmented Triage Model.&quot; Oral presentation FP5-2 (Abstract No. 10340), <i>APASL Single Topic Conference 2026</i>, Kumamoto, Japan.'
---

**Oral presentation** in Free Papers 5-1: MASLD/ALD 1, Saturday 19 September 2026, Kumamoto, Japan. **Recipient of the APASL STC 2026 Kumamoto International Travel Award.**
Affiliation: BS Degree Program in Data Science and Applications, Indian Institute of Technology Madras.
[Slides (PDF)](/files/APASL_STC2026_FP5-2_slides.pdf) · [Code](https://github.com/MAUK9086/malsd_fib4)

Background
------
FIB-4 is the guideline-recommended first-line test for triaging liver fibrosis in metabolic dysfunction-associated steatotic liver disease (MASLD). It was designed to rule out advanced (F3–F4) disease. It relies on AST, ALT and platelet count. These values are near-normal in a recognised obesity-driven phenotype (BMI ≥ 30 kg/m², ALT/AST < 40 U/L), and FIB-4 contains no measure of adiposity. How well it performs for early-to-moderate (F2+) fibrosis is poorly characterised. The aim was to identify FIB-4 false negatives, characterise them, and develop a supplementary triage tool for primary care.

Methods
------
- **Cohort:** NHANES 2017–2020: 1,998 MASLD-eligible adults with complete FibroScan elastography (median age 50 years, 54% male).
- **Definition:** a false negative is FIB-4 < 1.30 despite liver stiffness ≥ 8.0 kPa (F2+ fibrosis).
- **Characterisation:** gradient-boosted trees with SHAP attributions across 40 clinical variables, plus clustering to identify phenotypes of missed patients.
- **Supplementary model:** FIB-4 Plus (FIB-4 + BMI + waist circumference + Hepatic Steatosis Index), compared with the NAFLD Fibrosis Score (NFS).

Results
------
- **One in six missed.** FIB-4 classified 1,390 patients (70%) as low risk. Of these, **16.6%** (95% CI 13.5–20.0%) had F2+ fibrosis.
- **Concentrated in obesity and diabetes.** False-negative rates rose from 5.1% at BMI < 25 kg/m² to **37.7%** at BMI ≥ 40 kg/m². They were 2.5-fold higher in patients with diabetes (29.8% vs. 11.8%).
- **Best predictors are absent from FIB-4.** Waist circumference (AUROC 0.754) and BMI (AUROC 0.737) best predicted a missed case.
- **Two phenotypes of missed patients:**
  - *Severely Obese Metabolic* (n = 89; BMI 46.1 kg/m²; 67% female; liver stiffness 10.5 kPa).
  - *Dyslipidaemic Metabolic* (n = 131; BMI 35.3 kg/m²; 76% male; 44% diabetic; triglycerides 168 mg/dL).
- **FIB-4 Plus** outperformed NFS: AUROC **0.837** (95% CI 0.773–0.898) vs. 0.749 (95% CI 0.656–0.830); DeLong p = 0.019; net reclassification improvement 9.2%.

<img src="/images/fib4-apasl-figure.jpg" alt="FIB-4 false-negative rates by BMI and subgroup, phenotype profiles, and ROC comparison of FIB-4 Plus vs NFS" width="100%">

*Figure (as submitted with the abstract). (A) FIB-4 false-negative rate by BMI category. (B) False-negative rate by clinical subgroup. (C) Profiles of the two false-negative phenotypes. (D) ROC comparison of FIB-4 Plus and the NAFLD Fibrosis Score.*

Conclusions
------
FIB-4's blind spot is systematic: metabolic obesity with preserved transaminases. Supplementing FIB-4 with routine anthropometric and metabolic measurements, all recorded at a standard visit, recovers a substantial part of the missed fibrosis. This is most relevant for primary-care patients with BMI ≥ 30 kg/m² or diabetes. Fibrosis occurs at lower BMI in Asian populations, so validation in lean MASLD phenotypes is the next step.

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
