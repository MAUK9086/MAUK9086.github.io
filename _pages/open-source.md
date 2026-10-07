---
layout: single
title: "Open-Source Contributions"
permalink: /open-source/
author_profile: true
---

I contribute performance, correctness and documentation fixes to the scientific Python ecosystem. Statuses below are as of October 2026.

scikit-learn
------

| PR | Title | Status |
|---|---|---|
| [#33269](https://github.com/scikit-learn/scikit-learn/pull/33269) | Vectorize `_logcosh` in FastICA | Merged (Apr 2026) |
| [#33268](https://github.com/scikit-learn/scikit-learn/pull/33268) | Use `check_array` in `inverse_transform` for `PowerTransformer` / `QuantileTransformer` | Merged (Apr 2026) |
| [#33153](https://github.com/scikit-learn/scikit-learn/pull/33153) | Document startup overhead in parallelism | Merged (Jan 2026) |
| [#33148](https://github.com/scikit-learn/scikit-learn/pull/33148) | Correct validation in `BisectingKMeans` with custom `init` | Merged (Feb 2026) |
| [#33271](https://github.com/scikit-learn/scikit-learn/pull/33271) | Use `pinv` instead of `inv` in PCA for numerical stability | Closed |

- **FastICA performance (#33269, fixes #32914).** In the deflation algorithm, FastICA calls the `_logcosh` non-linearity on 1-D arrays. The existing code then computed the derivative one element at a time in a Python loop. The PR adds a vectorised path for 1-D input and keeps the memory-saving loop for 2-D input. For `FastICA(algorithm="deflation", fun="logcosh")` on a 2000 × 50 dataset, fitting time fell from **424.0 s to 17.7 s (≈ 24×)**. A regression test was added.
- **Spurious feature-name warning (#33268, fixes #31947).** `PowerTransformer` and `QuantileTransformer` wrongly warned "X has feature names, but … was fitted without feature names" in `inverse_transform`. The fix validates input with `check_array` and adds regression tests. It builds on earlier work by another contributor in a closed PR.

*Core change in #33269 (`sklearn/decomposition/_fastica.py`):*

```diff
 def _logcosh(x, fun_args=None):
     alpha = fun_args.get("alpha", 1.0)

     x *= alpha
     gx = np.tanh(x, x)  # apply the tanh inplace
+
+    if x.ndim == 1:
+        return gx, alpha * (1 - gx**2)
+
+    # When the input is 2D, compute in a loop to avoid extra allocation
+    # of array of shape x.shape
     g_x = np.empty(x.shape[0], dtype=x.dtype)
     for i, gx_i in enumerate(gx):
         g_x[i] = (alpha * (1 - gx_i**2)).mean()
     return gx, g_x
```

scikit-bio
------

| PR | Title | Status |
|---|---|---|
| [#2427](https://github.com/scikit-bio/scikit-bio/pull/2427) | Lazy-load `requests` and `h5py` to reduce import time | Merged (Apr 2026) |
| [#2425](https://github.com/scikit-bio/scikit-bio/pull/2425) | Fix `multi_replace` output type for pandas 3.0 `apply` | In progress |

- **Import latency (#2427).** Moved the optional `requests` and `h5py` imports into the functions that use them, so `import skbio` no longer loads them. Mean import time fell from **112.7 ms to 70.3 ms (−37%)** over 5 fresh-process runs, and all 368 I/O tests pass. This is a step towards the project's broader import-time issue (#2170).

Keras Hub
------

| PR | Title | Status |
|---|---|---|
| [#2555](https://github.com/keras-team/keras-hub/pull/2555) | Fix Moonshine LiteRT export: handle boolean masks in test runner | In progress |
| [#2551](https://github.com/keras-team/keras-hub/pull/2551) | Fix default masking warnings in `TransformerDecoder` and `PositionEmbedding` | Open |
| [#2550](https://github.com/keras-team/keras-hub/pull/2550) | Fix `SparseCategoricalCrossentropy` crash by ignoring −1 labels | Open |

- **LiteRT export (#2555, fixes #2493).** The LiteRT (TFLite) export test helper cast boolean attention masks to `int32`, which broke export of the Moonshine speech model. Keeping the masks boolean lets the previously skipped Moonshine export test run again.

Own packages
------
- [**flwr-trees**](/portfolio/flwr-trees): federated learning for tree ensembles with a scikit-learn API ([PyPI](https://pypi.org/project/flwr-trees/)).
