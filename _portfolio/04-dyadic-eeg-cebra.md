---
title: "Brain-to-Brain Decoder: Dyadic EEG Representation Learning with CEBRA"
excerpt: "An independent study that learns joint neural embeddings of two people in conversation from hyperscanning EEG. A hybrid CEBRA embedding decodes affective condition with 0.967 k-NN accuracy, while label- and temporal-shuffle controls fall to chance. Includes a reproducible pipeline and a plan for scaling to multiple dyads."
collection: portfolio
order: 3
permalink: /portfolio/dyadic-eeg-cebra
---

**Context:** independent study, 2026. [Report (PDF)](/files/Brain_to_Brain_Decoder_Khan_2026.pdf). Code is available on request.

Idea
------
Most EEG analyses model one brain at a time. In *hyperscanning*, EEG is recorded from two people at once, here a speaker and a listener. That makes it possible to treat the pair as **one coupled system** and ask whether a joint low-dimensional embedding of both brains encodes the affective content of their interaction. CEBRA (Schneider, Lee & Mathis, 2023) learns such embeddings by contrastive learning, using time and/or behavioural labels as auxiliary variables.

Pipeline
------
- **Data:** a single dyadic hyperscanning recording, two 64-channel EEG streams at 250 Hz, aligned using shared DIN1 trigger markers (constant 217 ms offset, no drift).
- **Pre-processing:** 1–40 Hz band-pass filter, matched bad-channel interpolation in both recordings, and Extended-Infomax ICA with ICLabel-assisted component rejection. Global z-scoring after concatenation avoids the label leakage that within-segment normalisation introduces.
- **Joint representation:** listener and speaker channels are concatenated into one 128-channel input (75,431 time points), then embedded with three CEBRA variants: *time-only*, *behaviour (label)-driven* and *hybrid*.
- **Evaluation:** k-NN decoding (k = 5, 5-fold CV) of affective condition, goodness-of-fit, and two controls (shuffled labels and shuffled time). Further analyses split decoding by participant, frequency band and scalp region.

Results
------

| Embedding | k-NN accuracy | R² |
|---|---|---|
| Time-only | 0.490 | −0.478 |
| Behaviour | 0.948 | 0.818 |
| Hybrid | **0.967** | **0.878** |

Both controls fall to chance. Shuffled labels give 0.499 ± 0.007, and shuffling the speaker's time axis, which breaks inter-brain alignment, gives 0.515. Decoding therefore depends on the true label structure and on the temporal coupling between the two recordings. The joint embedding (0.843) decoded better than either participant alone (listener 0.624, speaker 0.821).

- **Frequency bands:** delta (1–4 Hz, 0.973) and gamma (30–45 Hz, 0.931) carried most of the decodable information.
- **Scalp regions:** in channel-level ablation, frontal (+0.450) and temporal (+0.417 left, +0.378 right) regions contributed most, parietal regions moderately (+0.261), and occipital regions least (+0.065).

<img src="/images/cebra-affect-decoding.png" alt="k-NN decoding accuracy of CEBRA variants and shuffle controls" width="85%">

*Figure 1. Affect decoding accuracy of the CEBRA variants compared with shuffle controls (dashed line = chance).*

<img src="/images/eeg-embedding-3d.png" alt="3D CEBRA embedding of the dyadic EEG signal coloured by affect condition" width="85%">

*Figure 2. 3D CEBRA embedding of the joint dyadic signal (label-based), coloured by affect condition.*

Next steps
------
The report sets out how to extend the pipeline from one dyad to many:
- Leave-One-Dyad-Out validation and learning curves over the number of dyads.
- Seed-averaged reporting.
- Statistical comparison of embeddings with the cross-entropy test (Roca et al., 2023).
- Phase-randomisation controls.
- Procrustes alignment of embeddings across dyads.
