---
layout: archive
title: "Curriculum Vitae"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[Download CV (PDF)](/files/Mohammad_Ahmadullah_Khan_CV.pdf)

Education
======
* **B.S. in Data Science and Applications**, Indian Institute of Technology Madras, Chennai. Jan 2023 – Dec 2026 (expected)
  * SGPA 7.67 / 10
  * Relevant coursework: Machine Learning Practice, Statistical Computing, Big Data Analytics, System Design
* **B.Tech in Computer Engineering**, Jamia Millia Islamia, New Delhi. Jul 2022 – Jun 2026
  * CGPA 8.70 / 10
  * Thesis: *Low-Resource Indian Sign Language Video Generation via Compressed Multi-Condition Tokenisation* (supervisor: Mr. Shamim Ahmad)
  * Relevant coursework: Responsible and Safe AI, Analysis of Algorithms, Data Mining, Database Management Systems
* **Senior Secondary (CBSE)**, Bal Bhawan School, Bhopal. 2019 – 2021
  * Class XII (Physics, Chemistry, Mathematics): 95.8%; Class X: 95.2%; qualified JEE Advanced

Research and professional experience
======
* **Machine Learning Intern**, "Walk for Life" project, Institute of Liver and Biliary Sciences (ILBS), New Delhi. Jan 2026 – present
  * Project leads: Prof. (Dr.) Shiv Kumar Sarin (PI; Director, ILBS) and Dr. Harsh Vardhan T. (Co-PI; Associate Professor, Hepatology)
  * Built a pipeline that merges and normalises longitudinal patient records from 10+ clinical sources.
  * Developed real-time contactless vital-sign estimation (heart rate, HRV, SpO2) from webcam video using rPPG.
  * Built low-latency IPC mechanisms and data-validation constraints for concurrent telemetry streams.
* **Open-source contributor**: scikit-learn, scikit-bio, Keras Hub. Jan 2026 – present
  * Five merged pull requests, including a ≈24× speed-up of FastICA's deflation path (scikit-learn #33269) and a 37% reduction in scikit-bio import time (#2427). [Details](/open-source/)

Publications and working papers
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>

Research software and projects
======
* **flwr-trees**: federated learning for Random Forest, XGBoost and gradient-boosted trees with a scikit-learn API, built on Flower. Published on [PyPI](https://pypi.org/project/flwr-trees/). [Details](/portfolio/flwr-trees)
* **Dyadic EEG representation learning with CEBRA** (independent project, 2026): joint embeddings of speaker and listener EEG; 0.967 k-NN decoding of affective condition, with chance-level shuffle controls. [Details](/portfolio/dyadic-eeg-cebra)
* **LUFY**: retrieval-augmented legal-document assistant (FastAPI, ChromaDB, BM25 + dense hybrid retrieval, Docker). [Details](/portfolio/lufy-legal-rag)

Honours and awards
======
* APASL International Travel Award, APASL STC 2026, Kumamoto, Japan (2026)
* Winner, Smart India Hackathon 2024 Grand Finale, NTRO, problem statement 1680 (2024)
* Rank 98 of 32,000+ teams (top 0.3%), Amazon ML Challenge 2024 (2024)
* Winner, HackJMI 2024 (2024)
* Qualified, National Standard Examination in Physics (NSEP), top 1% nationally (2021)

Technical skills
======
* **Languages:** Python, C++, SQL, Bash
* **Machine learning:** PyTorch, scikit-learn, TensorFlow / Keras, Hugging Face Transformers, OpenCV, retrieval-augmented generation, local LLM inference (Ollama)
* **Systems and tools:** FastAPI, Flask, Docker, ChromaDB, Git and GitHub Actions, Linux, pytest, PySpark, Azure Databricks
* **Foundations:** data structures and algorithms, linear algebra, optimisation, discrete mathematics, system design

Teaching and outreach
======
  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Certifications
======
* Google Data Analytics Professional Certificate, Coursera (SQL, R, Tableau)
* NPTEL: Responsible and Safe AI Systems (Elite), funded by the Ministry of Education, Government of India

Service and leadership
======
* General Secretary, IEEE Student Branch, Jamia Millia Islamia (Mar 2024 – present): led a team of 15+ to run 10+ technical workshops for 1,200+ students
* Chief Arbiter, Piper Chess Club: organised and adjudicated tournaments for 30+ participants
