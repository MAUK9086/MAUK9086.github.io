---
title: "Few-Shot, Language-Agnostic Keyword Spotting"
excerpt: "A keyword-spotting system that recognises new spoken keywords from a few examples, in any language. Winning solution at the Smart India Hackathon 2024 Grand Finale (NTRO, problem statement 1680), later extended from 10 to 440 keyword classes with under 10% accuracy loss relative to fully supervised baselines."
collection: portfolio
order: 5
permalink: /portfolio/few-shot-keyword-spotting
---

**Recognition:** Winner, Smart India Hackathon 2024 Grand Finale (National Technical Research Organisation, problem statement 1680).
**Follow-up research:** October – December 2025.
**Reference documents:** [Falkon_SIH](https://github.com/MAUK9086/Falkon_SIH)

Problem
------
The task is to detect user-defined keywords in audio streams that may be in any language, including low-resource ones, given only a handful of recorded examples per keyword. Standard keyword-spotting models need many labelled utterances per keyword and a fixed vocabulary.

Phase 1: hackathon system (2024)
------
- **Audio features as an image:** clips are resampled to 16 kHz and fixed to 3 s. A Mel spectrogram, spectral centroid and chromagram are stacked as three channels, so an ImageNet-pre-trained ResNet-50 can be fine-tuned with only its last layers trainable.
- **Few-shot weight generator:** to add a new keyword without retraining, its classifier weights are generated from the few support examples. The generator averages their features with a learnable scale and attends over existing base-class weights (cosine attention). It is trained in two stages with simulated "novel" classes. This follows the dynamic few-shot learning approach of Gidaris & Komodakis (2018).

```python
resnet = ResNet50(weights='imagenet', include_top=False, input_tensor=Input(shape=input_shape))
# Freeze all layers except the last few
for layer in resnet.layers[:-10]:
    layer.trainable = False
```

Phase 2: scaling study (2025)
------
- **Question:** can a language-agnostic few-shot spotter scale from 10 to hundreds of classes under extreme data scarcity in multilingual streams?
- **Model:** a Transformer encoder over MFCC features, with voice-activity detection (VAD) to segment speech from continuous streams.
- **Outcome:** scaled from 10 to **440 keyword classes** (44×) with **under 10%** accuracy degradation relative to fully supervised baselines.
