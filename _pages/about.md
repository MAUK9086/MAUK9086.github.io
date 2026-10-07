---
permalink: /
title: "About"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I am an undergraduate researcher in machine learning. I hold a B.Tech in Computer Engineering from [Jamia Millia Islamia](https://jmi.ac.in), New Delhi (2022–2026), and I am completing a B.S. in Data Science and Applications at the [Indian Institute of Technology Madras](https://study.iitm.ac.in/ds/) (expected December 2026). Since January 2026 I have been a Machine Learning Intern on the "Walk for Life" project at the [Institute of Liver and Biliary Sciences (ILBS)](https://www.ilbs.in), New Delhi. There I work on clinical data pipelines and on contactless vital-sign estimation from video.

My work asks a common question: **when does a model look right for the wrong reasons, and how can we measure it?** In language models, I study whether models reason over nested defeasible premises in an order-invariant way. I introduced a metric that tests whether correct final answers are supported by correct intermediate steps. In clinical ML, I study where established screening rules fail. One example is the FIB-4 index in obese patients with MASLD (metabolic dysfunction-associated steatotic liver disease), presented as an oral talk at APASL STC 2026. I also build research software, including [flwr-trees](https://pypi.org/project/flwr-trees/), a scikit-learn–compatible library for federated tree ensembles, and I contribute to scikit-learn and the wider scientific Python ecosystem.

Research statement
======
I want to build machine-learning systems whose success can be trusted for the right reasons. In both language models and clinical prediction, aggregate accuracy often hides systematic failure: a model can be accurate on average while relying on input order, surface cues, or a population it was not designed for. My goal is to develop evaluation methods that expose these failures, using controlled perturbations, subgroup analysis and step-level metrics. I also want to develop modelling approaches that remain reliable when they are deployed in clinical and other high-stakes settings. I am looking for research positions where I can pursue these questions with rigorous experimental design and real-world data.

Research interests
======
- **Reliable reasoning in language models:** order sensitivity, faithfulness of intermediate reasoning, evaluation design
- **Clinical machine learning:** failure modes of clinical risk scores, interpretable models, population-level evaluation
- **Privacy-preserving and federated learning:** communication-efficient aggregation for tree ensembles
- **Physiological signal processing:** remote photoplethysmography (rPPG), heart-rate variability, EEG representation learning

News
======
- **Sep 2026:** Presented *"FIB-4 False Negatives in MASLD: Clinical Phenotypes and an Augmented Triage Model"* as an **oral presentation** at APASL STC 2026 (Kumamoto, Japan), and received the **APASL International Travel Award**.
- **May 2026:** Released [flwr-trees 0.1.0](https://pypi.org/project/flwr-trees/) on PyPI.
- **Apr 2026:** Pull requests merged into scikit-learn (FastICA performance, preprocessing validation fix) and scikit-bio (import-time reduction). See [Open Source](/open-source/).
- **Jan 2026:** Joined the Institute of Liver and Biliary Sciences, New Delhi, as a Machine Learning Intern.
- **Dec 2024:** Winner, Smart India Hackathon 2024 Grand Finale (problem statement 1680, NTRO).

Education
======
- **B.S. in Data Science and Applications**, Indian Institute of Technology Madras, 2023 – Dec 2026 (expected)
- **B.Tech in Computer Engineering**, Jamia Millia Islamia, New Delhi, 2022 – 2026. CGPA 8.70 / 10

Selected honours
======
- APASL International Travel Award, APASL STC 2026
- Winner, Smart India Hackathon 2024 (Grand Finale, NTRO)
- Rank 98 of 32,000+ teams (top 0.3%), Amazon ML Challenge 2024
- Winner, HackJMI 2024
- Qualified, National Standard Examination in Physics (NSEP) 2021; qualified JEE Advanced 2021

A full CV is available [here](/cv/) ([PDF](/files/Mohammad_Ahmadullah_Khan_CV.pdf)).
