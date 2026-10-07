---
title: "Zero- and Few-Shot Clinical Entity Linking with SNOMED CT Graph Structure (Proposal)"
excerpt: "A research proposal and literature review on using heterogeneous graph neural networks over the SNOMED CT ontology to link rare and unseen clinical concepts in free-text notes. In preparation."
collection: portfolio
order: 8
permalink: /portfolio/clinical-entity-linking
---

**Status:** literature review and research design (2026). No experimental results yet.

Problem
------
Clinical entity linking maps mentions in clinical notes ("SOB", "shortness of breath on exertion") to concepts in a terminology such as SNOMED CT, which contains over 350,000 concepts. Current systems perform well on frequent concepts but degrade sharply on rare concepts and on concepts never seen in training. These long-tail concepts are often the clinically important ones. In the SNOMED CT Entity Linking Challenge (MIMIC-IV discharge notes), the best reported score was an IoU of about 0.42, which shows how unsolved the task remains.

Proposed direction
------
- Exploit the **ontology topology**: a rare concept's parents, siblings and defining relationships carry information that text-only encoders ignore.
- Represent SNOMED CT as a **heterogeneous graph** (concept, description and relationship types) and adapt Heterogeneous Graph Transformers, with sampling strategies suitable for a graph of this size, to produce concept embeddings for unseen concepts.
- Combine these graph embeddings with a text encoder for mention–concept matching.
- Evaluate with a benchmarking checklist that separates seen, rare and unseen concepts, so that improvements on the long tail are not hidden by frequent-concept performance.
