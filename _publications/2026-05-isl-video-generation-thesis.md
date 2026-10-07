---
title: "Low-Resource Indian Sign Language Video Generation via Compressed Multi-Condition Tokenisation"
collection: publications
category: theses
permalink: /publication/2026-05-isl-video-generation-thesis
excerpt: 'B.Tech thesis (with Hammad Ali). A two-stage text → skeleton → video pipeline for Indian Sign Language trained on 471 videos, using body-part finite scalar quantisation and a frozen Stable Diffusion + ControlNet renderer.'
date: 2026-05-01
venue: 'B.Tech Thesis, Department of Computer Engineering, Jamia Millia Islamia'
citation: 'H. Ali and M. A. Khan. (2026). &quot;Low-Resource Indian Sign Language Video Generation via Compressed Multi-Condition Tokenisation.&quot; <i>B.Tech Thesis</i>, Jamia Millia Islamia, New Delhi. Supervisor: Mr. Shamim Ahmad.'
---

**Authors:** Hammad Ali and Mohammad Ahmadullah Khan. **Supervisor:** Mr. Shamim Ahmad, Department of Computer Engineering, Jamia Millia Islamia. The thesis is available on request.

Problem
------
Sign-language video generation systems are usually trained on thousands of hours of data. Indian Sign Language (ISL) has very little. The ISL-CSLTR corpus used here has 471 videos covering 97 sentences. The thesis asks how much of a modern sign-generation pipeline can work at this scale.

Approach
------
We adapt the SignViP design into two stages:

1. **Text → pose tokens.** A frozen CLIP text encoder conditions a small (1.5M-parameter) autoregressive translator. It predicts a 16-frame skeleton sequence as discrete tokens. Poses are tokenised with *body-part finite scalar quantisation* (FSQ), using separate 81-code codebooks for the body, left hand and right hand.
2. **Pose → video.** A frozen Stable Diffusion 1.5 model renders the video frames, with ControlNet-OpenPose for pose conditioning and IP-Adapter for signer appearance.

Key findings
------
- **Codebook collapse at low data.** A single 625-code codebook collapsed to 1 of 625 codes in use. The body-part 81-code design used 100% of its codes and cut reconstruction MSE from 0.473 to 0.296 (−37%).
- **Hand keypoints are the bottleneck.** DWPose detected hands in 96.4% / 99.7% of frames (left / right), versus 30.9% / 57.4% for MediaPipe, so all pose extraction uses DWPose.
- **Error attribution.** On a sentence-disjoint test set (51 samples), pose MPJPE was 0.250, against an FSQ reconstruction ceiling of 0.074. About 71% of the pose error therefore comes from the translator, not the tokeniser. Token accuracy was 53.8%, versus 51% for a constant-token baseline, which shows how hard sentence-level generalisation is with only 97 training sentences.
- **Video quality.** The full pipeline reached SSIM 0.415 ± 0.105, LPIPS 0.601 ± 0.096 and CLIP image similarity 0.795. With ground-truth skeletons as input, SSIM was 0.516, which isolates the renderer's contribution.
