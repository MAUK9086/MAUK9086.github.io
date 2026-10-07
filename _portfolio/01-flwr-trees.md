---
title: "flwr-trees: Federated Learning for Tree Ensembles"
excerpt: "An open-source Python library (on PyPI) that trains Random Forest, XGBoost and gradient-boosted tree models across clients using the Flower framework, behind a standard scikit-learn interface. Introduces histogram-based aggregation that cuts the first-round upload by 45–83% on benchmark datasets."
collection: portfolio
order: 1
permalink: /portfolio/flwr-trees
---

**Links:** [PyPI](https://pypi.org/project/flwr-trees/) · [GitHub](https://github.com/MAUK9086/flwr-trees) · `pip install flwr-trees` · License: Apache-2.0

Motivation
------
Tree ensembles remain the strongest models for tabular data, including clinical and financial records that often cannot leave the institution that holds them. Most federated learning tooling, however, targets neural networks, and federating tree models usually means writing a separate client–server script for each experiment. flwr-trees makes federated tree models usable as ordinary scikit-learn estimators.

Design
------
- **scikit-learn compatibility.** The library has eight estimators: Random Forest, XGBoost, gradient-boosted trees and histogram-RF, each as a classifier and as a regressor. All of them implement the `BaseEstimator` contract and pass scikit-learn's `check_estimator()`. They therefore work inside `Pipeline`, `GridSearchCV` and cross-validation without modification.
- **Three aggregation strategies:**
  - `FedForestBagging`: each client trains trees locally, and the server pools them into one forest.
  - `FedForestCyclic`: an XGBoost booster is passed round-robin between clients, each adding boosting rounds on its own data.
  - `FedHistogramAggregation`: the main methodological contribution. In the first round, clients send per-feature split histograms instead of fitted trees. The server builds global split thresholds from these histograms, and clients then train with the shared thresholds.
- **Experimental controls.** The library supports Dirichlet non-IID partitioning (parameter α), client-dropout simulation, differential-privacy hooks (Laplace noise on histograms, Gaussian noise on leaf values) and CUDA support for XGBoost.
- **Memory.** A disk-backed tree store writes fitted ensemble members to disk and loads them lazily during evaluation, so memory use does not grow with ensemble size.
- **Engineering.** The test suite has 171 tests, run by continuous integration on GitHub Actions.

Usage
------
```python
from flwr_trees import FederatedHistogramRFClassifier

clf = FederatedHistogramRFClassifier(
    n_estimators=50, n_clients=10, n_rounds=3,
    n_bins=32, iid=False, alpha=0.5,
    use_flower=True, random_state=42,
)
clf.fit(X_train, y_train)
print(clf.score(X_test, y_test))

# Inspect communication cost
print(clf.strategy_.bytes_sent_per_round)    # [histogram_bytes, tree_bytes, ...]
print(clf.strategy_.bytes_saved_vs_bagging)  # savings vs standard bagging
```

Results
------
Benchmark settings: 5 clients, 20 trees, 3 rounds, 32 histogram bins. The comparison is the size of the first-round upload under histogram aggregation versus standard bagging.

| Dataset | Round-1 payload saving | Accuracy (bagging → histogram) |
|---|---|---|
| Breast Cancer (IID) | 45.2% | 0.974 → 0.965 |
| Synthetic (IID) | 82.8% | 0.910 → 0.880 |
| Synthetic (non-IID, α = 0.3) | 80.6% | 0.665 → 0.700 |
| Adult (census income) | 99.8% (108 KB vs. 48 MB) | — |

<img src="/images/flwr-trees-round1-payload.png" alt="Round-1 upload payload, bagging vs histogram aggregation" width="85%">

*Figure. First-round upload size per strategy. Data: `benchmarks/results.json` in the repository.*
