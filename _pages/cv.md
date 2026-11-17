---
layout: archive
title: "Curriculum Vitae"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[Download CV (PDF)](/files/Mohammad_Ahmadullah_Khan_CV.pdf). This page follows the PDF.

Education
======
* **B.Tech in Computer Engineering**, Jamia Millia Islamia, New Delhi. Jul 2022 – Jun 2026. CGPA 8.70 / 10
* **B.S. in Data Science and Applications**, Indian Institute of Technology Madras (online degree). Jan 2023 – present. SGPA 7.67 / 10

Research experience
======
* **Machine Learning Intern**, "Walk for Life" project, Institute of Liver and Biliary Sciences (ILBS), New Delhi. Jan 2026 – present
  * Project leads: Prof. (Dr.) Shiv Kumar Sarin (PI; Director, ILBS) and Dr. Harsh Vardhan T. (Co-PI; Hepatology)
  * Developed real-time contactless estimation of heart rate, HRV and SpO2 from webcam video using remote photoplethysmography (face-landmark regions, ICA, band-pass filtering, spectral and inter-beat metrics). [Details](/portfolio/contactless-vital-signs)
  * Built a non-contact anthropometry system from three RGB-D cameras: pose estimation (YOLOv8), 3D reconstruction from depth, and gradient boosting under nested leave-one-out CV and permutation tests on 89 patients: height within 2.18 cm mean absolute error (r = 0.96), waist and hip r = 0.84 and 0.78; traced neck-measurement failure to chin occlusion.
  * Built a multimodal model that fuses a RETFound fundus-image encoder with clinical tabular data (missingness-aware tokens, bottleneck fusion transformer, two-stage training) to predict seven systemic conditions from retinal images.

Publications and presentations
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>

Honours and awards
======
* International Travel Award, APASL Single Topic Conference 2026, Kumamoto, Japan (2026)
* Winner, Smart India Hackathon 2024 Grand Finale (problem statement 1680, NTRO) (2024)
* Rank 98 of 32,000+ teams (top 0.3%), Amazon ML Challenge (2024)
* Winner, HackJMI (2024)

Teaching and leadership
======
* **General Secretary**, IEEE Student Branch, Jamia Millia Islamia: 10+ workshops for 1,200+ students (2024 – 2025)
* **Co-instructor**, Introduction to Machine Learning workshop, W3B, Jamia Millia Islamia: 150+ students (Jan – Feb 2025)

Research projects
======
* **Counting Clusters, Not Pairs: forensics on agent-swarm text** (Nov 2026; sole author, Apart Research Swarm Alignment sprint): on 300,000 Moltbook posts and a held-out collusion.wiki export, no copy-direction cue beat "the longer text is later", and scoring pairs instead of clusters makes a chance-level method look significant in 86% of null draws. [Details](/portfolio/swarm-lineage) · [Report (PDF)](/files/Counting_Clusters_Not_Pairs_Khan_2026.pdf)
* **La Espada: frame-level ball possession from tracking data** (Nov 2026; solo entry to More than a Hack 2027, a football-data challenge by FC Barcelona's Barça Innovation Hub and Mobile World Capital Barcelona with Metrica Sports): rules plus a three-model TCN ensemble trained only on external matches, decoded by an event-gated Viterbi pass; leave-one-match-out spellF1 0.759. [Details](/portfolio/la-espada-possession)
* **Patch Sloth: second opinion on vulnerability severity** (Oct 2026): flags vulnerabilities whose vendor-only severity score an independent reviewer would likely raise; when it flagged a CVE as "likely under-rated", NIST had raised the score 75% of the time against a 9.5% base rate, on 8,000 CVEs from 2026. [Details](/portfolio/patch-sloth)
* **Brain-to-Brain Decoder: dyadic EEG with CEBRA** (independent study, 2026): joint embeddings of two people's hyperscanning EEG; a hybrid CEBRA embedding decodes affective condition with 0.967 k-NN accuracy, while shuffle controls fall to chance. [Details](/portfolio/dyadic-eeg-cebra) · [Report (PDF)](/files/Brain_to_Brain_Decoder_Khan_2026.pdf)

Software projects
======
* **flwr-trees: federated learning for tree ensembles** (2026): library for training tree ensembles across institutions that cannot share data; histogram aggregation cuts the first-round upload by 45–83% on benchmark datasets; 171 tests in CI. [Details](/portfolio/flwr-trees) · [PyPI](https://pypi.org/project/flwr-trees/)
* **LUFY: legal-document assistant** (2025 – 2026): plain-language summaries, clause risk flags and cited answers in English and 16 Indian languages, using dense + BM25 retrieval fused with Reciprocal Rank Fusion and cross-encoder re-ranking; 31 tests. [Details](/portfolio/lufy-legal-rag)

Open-source contributions
======
* **scikit-learn** (4 merged pull requests): a vectorised FastICA non-linearity cut fitting time on a 2,000×50 dataset from 424.0 s to 17.7 s (≈24× faster, #33269); fixes for spurious feature-name warnings in `PowerTransformer`/`QuantileTransformer` (#33268) and `BisectingKMeans` validation (#33148); parallelism documentation (#33153).
* **scikit-bio:** lazy imports cut import time from 112.7 ms to 70.3 ms (−37%) with all 368 I/O tests passing (#2427, merged); pandas-3 fix open (#2661). **Keras Hub:** two fixes open (#2550, #2551). [Details](/open-source/)

Technical skills
======
* **Languages:** Python, C++, SQL, Bash, Lean 4, LaTeX
* **Machine learning:** PyTorch, scikit-learn, XGBoost, TabPFN, Hugging Face Transformers, LoRA fine-tuning, CEBRA, OpenCV, RAG, statistical testing
* **Systems and tools:** FastAPI, Docker, ChromaDB, Git and GitHub Actions, pytest, Linux, Flower, PySpark
* **Certifications:** Google Data Analytics Professional Certificate; NPTEL Responsible and Safe AI (Elite)
