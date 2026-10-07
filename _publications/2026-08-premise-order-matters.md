---
title: "Premise Order Matters: Positional Bias in Nested Defeasible Reasoning in SLM and LLM"
collection: publications
category: manuscripts
permalink: /publication/2026-08-premise-order-matters
excerpt: 'Five language models (3.8–9B parameters) lose 13–23 percentage points of accuracy when the premises of a logically order-invariant defeasible-reasoning problem are permuted. A new Stepwise Transfer Score shows that correct final answers are supported by correct intermediate reasoning only 20–27% of the time.'
date: 2026-08-01
venue: 'Manuscript under review'
citation: 'M. A. Khan. (2026). &quot;Premise Order Matters: Positional Bias in Nested Defeasible Reasoning in SLM and LLM.&quot; <i>Manuscript under review</i>.'
---

**Status:** under peer review. A preprint and code will be linked here once the review process allows. Code is available on request.

Summary
------
In *defeasible* reasoning, a general rule can be overridden by an exception, and that exception can be overridden by a more specific meta-exception. For example: *birds fly* (P1); *penguins are birds that do not fly* (P2); *this penguin is on a plane* (P3). The correct conclusion depends only on what P1–P3 say, not on the order in which they appear. This work tests whether language models respect that invariance.

**Benchmark.** 1,230 three-level nested defeasible problems spanning multiple domains. Every problem is shown under all six orderings of its premises. Models must give the intermediate conclusions (levels 1 and 2) as well as the final answer (level 3).

**Models.** Five small and mid-sized open-weight language models (3.8B–9B parameters), evaluated at inference time without fine-tuning.

Findings
------
- **Order sensitivity.** Accuracy falls by **13–23 percentage points** from the canonical premise order to the worst-case permutation, although the correct answer is the same for every permutation.
- **Consistent asymmetry.** In every architecture, the largest failures occur when the *meta-exception comes first*, i.e., when the most specific premise is presented first. This suggests the models do not resolve the hierarchy in an order-invariant way.
- **Stepwise Transfer Score (STS).** A new metric: the probability that the intermediate (level 1 and level 2) conclusions are correct *given* that the final answer is correct. Final-answer accuracy is 80–90%, but only **20–27%** of correct predictions rest on correct intermediate reasoning. Final-answer accuracy alone therefore greatly overstates reasoning ability.

Ongoing work
------
A scaling follow-up extends the benchmark and evaluates a ladder of model sizes. It tests whether order sensitivity and unfaithful intermediate reasoning decrease with scale, and how much of the measured effect is due to weight quantisation.
