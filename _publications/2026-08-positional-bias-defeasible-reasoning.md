---
title: "Positional Bias in Nested Defeasible Reasoning: Order Sensitivity and Unfaithful Intermediate Steps in Small Language Models"
collection: publications
category: manuscripts
permalink: /publication/2026-positional-bias-defeasible-reasoning
excerpt: 'A permutation-based benchmark for nested defeasible reasoning shows that five open language models (3.8–9B parameters) are not order-invariant: accuracy falls by 13–23 percentage points under logically equivalent premise orderings, and correct final answers rarely rest on correct intermediate steps.'
date: 2026-08-01
venue: 'Working paper'
citation: 'M. A. Khan. (2026). &quot;Positional Bias in Nested Defeasible Reasoning: Order Sensitivity and Unfaithful Intermediate Steps in Small Language Models.&quot; <i>Working paper</i>.'
---

**Status:** working paper. An extended version, with a larger benchmark and a model-scaling study, is in preparation. Code and data are available on request.

Question
------
In formal reasoning, a valid conclusion does not depend on the order of its premises. This work tests whether instruction-tuned language models satisfy that property in **nested defeasible reasoning**. Here a general rule (P1) is overridden by an exception (P2), which is in turn overridden by a more specific meta-exception (P3). The logical structure is fixed, so any change in accuracy across premise orderings reflects positional bias rather than reasoning.

Setup
------
- **Benchmark:** 206 three-level defeasible-reasoning problems across eight domains. Each is presented under all six premise orderings.
- **Models:** five open instruction-tuned models from five organisations, between 3.8B and 9B parameters: Gemma-2-9B, Llama-3.1-8B, Mistral-7B, Phi-4-mini and Qwen2.5-7B.
- **Evaluation:** accuracy at each level of the hierarchy (L1–L3) under every ordering, with significance tests against the standard order.

Findings
------
- **No model is order-invariant.** Accuracy falls by **13–23 percentage points** from the standard premise order to the worst-case ordering, although the correct answer is the same in every ordering.
- **A consistent structural pattern.** Orderings that lead with the *exception* stay close to standard-order accuracy. Orderings that lead with the *meta-exception* produce the largest drops, in every model and domain.
- **Stepwise Transfer Score (STS).** A new metric for whether correct final answers are built from correct intermediate conclusions. Final-answer accuracy is 79.6–89.8%, but STS is only **20.4–27.2%**. Models often reach the right answer without the right intermediate reasoning.

<img src="/images/defeasible-order-heatmap.png" alt="Accuracy across all six premise orderings for five language models" width="100%">

*Figure. Final-answer accuracy (%) for each of the six premise orderings (rows) and five models (columns). The gold border marks the standard order. Orderings that place the meta-exception (P3) first give the lowest accuracy.*
