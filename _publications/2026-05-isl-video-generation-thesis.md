---
title: "Low-Resource Indian Sign Language Video Generation via Compressed Multi-Condition Tokenisation"
collection: publications
category: theses
permalink: /publication/2026-05-isl-video-generation-thesis
excerpt: 'B.Tech thesis (with Hammad Ali). The first text-to-skeleton-to-video baseline for Indian Sign Language on ISL-CSLTR (471 videos), using body-part finite scalar quantisation and a frozen Stable Diffusion + ControlNet + IP-Adapter renderer.'
date: 2026-05-01
venue: 'B.Tech Thesis, Department of Computer Engineering, Jamia Millia Islamia'
paperurl: '/files/ISL_thesis_Ali_Khan_2026.pdf'
citation: 'H. Ali and M. A. Khan. (2026). &quot;Low-Resource Indian Sign Language Video Generation via Compressed Multi-Condition Tokenisation.&quot; <i>B.Tech Thesis</i>, Jamia Millia Islamia, New Delhi. Supervisor: Mr. Shamim Ahmad.'
---

**Authors:** Hammad Ali and Mohammad Ahmadullah Khan. **Supervisor:** Mr. Shamim Ahmad, Department of Computer Engineering, Jamia Millia Islamia. [Thesis (PDF)](/files/ISL_thesis_Ali_Khan_2026.pdf)

Problem
------
Sign-language video generation systems are usually trained on large corpora. RWTH-PHOENIX-Weather, for German Sign Language, has about 8,257 sentences. Indian Sign Language (ISL) has no comparable resource. After quality filtering, the largest public corpus, ISL-CSLTR, yields 471 videos covering 97 unique sentences, roughly an 85-fold gap. The thesis asks how a modern sign-generation pipeline can be adapted to this low-resource setting.

Approach
------
We adapt the SignViP framework into a two-stage pipeline:

1. **Stage A, text → skeleton.** A frozen CLIP text encoder conditions a 1.5M-parameter autoregressive token translator. The translator predicts a 16-frame skeleton as discrete tokens from a *body-part finite scalar quantisation* (FSQ) tokeniser, with separate codebooks for the upper body, left hand and right hand.
2. **Stage B, skeleton → video.** Frozen pretrained components render the video: Stable Diffusion 1.5, ControlNet-OpenPose for pose, and IP-Adapter for the signer's appearance from a single reference image.

<img src="/images/isl-pipeline.png" alt="End-to-end text-to-skeleton-to-video pipeline" width="100%">

*Figure 1. End-to-end inference pipeline. Pink: components introduced in this work. Grey: frozen pretrained models.*

Contributions and findings
------
- **Compact body-part tokenisation for low-resource data.**
  - The original 625-code FSQ design collapses on ISL-CSLTR, using only 1 of its 625 codes. A 4-axis, 81-code codebook per body part reaches 100% utilisation. Three axes collapse, so four is the minimum at this data scale.
  - Separate codebooks per body part reduce reconstruction MSE by 37% (0.473 → 0.296). They also triple the tokens per clip (16 → 48).
- **Pose extraction for seated signers.** MediaPipe Holistic, widely used in ISL pipelines, detects only 30.9% / 57.4% of left / right hands on seated signers. DWPose detects 96.4% / 99.7%. This finding is useful for any future ISL work.
- **Decomposed evaluation.** We report metrics for Stage B given ground-truth skeletons alongside full text-to-video metrics, which isolates the cost of predicting motion from text. On a sentence-disjoint test set (51 samples):
  - Full-pipeline video: SSIM 0.415 ± 0.105, LPIPS 0.601 ± 0.096, CLIP image similarity 0.795.
  - With ground-truth skeletons: SSIM 0.516.
  - Most remaining pose error (71%) comes from the translator rather than the tokeniser. The right hand, which carries the most sign-specific information, is the hardest to predict.
- **Engineering.** A parallel scheduled-sampling scheme cut translator training from about 16 hours to about 4 minutes per run (~240×). This made the full model-sizing ablation feasible on free Kaggle GPUs.

To our knowledge, this is the first complete text-to-skeleton-to-video baseline on ISL-CSLTR. Prior ISL video-generation work evaluates rendering from ground-truth skeletons.

<img src="/images/isl-per-signer-metrics.png" alt="Per-signer SSIM, LPIPS and PSNR for ground-truth-conditioned and full pipeline" width="100%">

*Figure 2. Per-signer video quality on the test set: SSIM, LPIPS and PSNR with ground-truth skeletons (green) and for the full text-to-video pipeline (orange).*
