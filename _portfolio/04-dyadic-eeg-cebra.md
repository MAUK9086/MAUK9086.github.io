---
title: "Dyadic EEG Representation Learning with CEBRA"
excerpt: "Learning joint neural embeddings of two people in conversation from hyperscanning EEG. Hybrid CEBRA embeddings decode affective condition with 0.967 k-NN accuracy, while shuffle controls stay at chance. Independent project, 2026."
collection: portfolio
order: 3
permalink: /portfolio/dyadic-eeg-cebra
---

**Context:** independent project, 2026. Code is available on request.

Idea
------
Most EEG analyses model one brain at a time. In *hyperscanning*, EEG is recorded from two people at once, here a speaker and a listener. That makes it possible to treat the pair as **one coupled system** and ask whether a joint low-dimensional embedding of both brains encodes the affective content of their interaction. CEBRA (Schneider, Lee & Mathis, 2023) learns such embeddings by contrastive learning, using time and/or behavioural labels as auxiliary variables.

Pipeline
------
- **Data:** two 64-channel EEG recordings at 250 Hz, aligned using shared trigger markers (constant 217 ms offset).
- **Pre-processing:** 1–40 Hz band-pass filter, matched bad-channel interpolation in both recordings, and Extended-Infomax ICA (22/30 and 19/30 components rejected for listener and speaker). Normalisation is chosen to avoid information leaking between segments.
- **Joint representation:** listener and speaker channels are concatenated into one 128-channel input (75,431 time points), then embedded with three CEBRA variants: *time-only*, *behaviour (label)-driven* and *hybrid*.
- **Evaluation:** k-NN decoding (k = 5, 5-fold CV) of affective condition, goodness-of-fit, and two controls (shuffled labels and shuffled time). Further analyses split decoding by participant and by frequency band.

Results
------
| Embedding | k-NN accuracy | R² |
|---|---|---|
| Time-only | 0.490 | −0.478 |
| Behaviour | 0.948 | 0.818 |
| Hybrid | **0.967** | **0.878** |

Both controls fall to chance: shuffled labels give 0.499 ± 0.007, and shuffling the speaker's time axis, which breaks inter-brain alignment, gives 0.515. Decoding therefore depends on the true label structure and on the temporal coupling between the two recordings. The joint embedding (0.843) decoded better than either participant alone (listener 0.624, speaker 0.821). Delta and gamma bands carried most of the information.

<img src="/images/cebra-affect-decoding.png" alt="k-NN decoding accuracy of CEBRA variants and shuffle controls" width="85%">

*Figure. Affect decoding accuracy of the CEBRA variants compared with shuffle controls (dashed line = chance).*

**Next steps:** extend the pipeline to multiple dyads, test whether embeddings are consistent across dyads, and compare embeddings with a statistical test (the cross-entropy test).
