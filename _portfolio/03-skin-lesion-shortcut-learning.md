---
title: "Metadata Shortcut Learning in Multimodal Skin-Lesion Classification"
excerpt: "Do image + metadata fusion models for dermatology learn shortcuts from patient age, sex and lesion site? Modality-occlusion experiments on ISIC 2019 show that the fusion model relies almost entirely on the image, and that metadata contributes little. Ongoing work."
collection: portfolio
order: 3
permalink: /portfolio/skin-lesion-shortcut-learning
---

**Status:** ongoing work (2026). **Code:** [github.com/MAUK9086/AIMCON_JMI_26](https://github.com/MAUK9086/AIMCON_JMI_26)

Question
------
Skin-lesion classifiers increasingly combine the dermoscopic image with patient metadata (age, sex, anatomical site). Metadata is correlated with diagnosis; for example, older age is associated with malignancy (point-biserial r = 0.37 in ISIC 2019). This raises the risk that a fusion model learns a demographic *shortcut* instead of visual evidence, which in turn could cause failures on populations whose metadata distribution differs from the training data.

Method
------
- **Data:** ISIC 2019, 8 diagnostic classes, held-out test set of 3,801 images.
- **Models:** image-only, metadata-only and late-fusion classifiers trained under the same protocol.
- **Modality occlusion:** at test time, the image or the metadata input of the fusion model is replaced with an uninformative value. The drop in per-class sensitivity measures how much the model relies on that modality, with significance tested against the unoccluded baseline.
- **Subgroup analysis:** melanoma false-negative rates for an Indian-like vs. a Western-like metadata profile, with bootstrap confidence intervals and a power analysis.
- **Mitigations:** metadata dropout during training, and sample re-weighting.

Results so far
------
| Model | Balanced accuracy | Macro AUC |
|---|---|---|
| Metadata only | 0.317 | 0.709 |
| Image only | 0.774 | 0.967 |
| Fusion (image + metadata) | 0.795 | 0.969 |

- Occluding the **image** drops the fusion model's balanced accuracy from 0.795 to **0.163**. Occluding the **metadata** drops it only to **0.784**. On this benchmark the fusion model relies on visual evidence, not on a metadata shortcut.
- The melanoma false-negative rate was 0.325 for the Indian-like profile vs. 0.233 for the Western-like profile. This gap was **not** statistically significant: power was 0.36, and about 298 positive cases would be needed for 80% power. The disparity question therefore remains open.
- Metadata dropout (0.803) and re-weighting (0.805) gave small gains in balanced accuracy over the fusion baseline.

<img src="/images/skin-lesion-modality-reliance.png" alt="Per-class modality reliance heatmap for the fusion model" width="75%">

*Figure. Per-class reliance of the fusion model on each modality: the fall in sensitivity when that modality is occluded (* = p < 0.05).*
