---
title: "LUFY: Retrieval-Augmented Understanding of Legal Documents"
excerpt: "A legal-document assistant that turns an uploaded contract into a plain-language summary, a three-tier clause risk analysis and citation-grounded Q&A in English and 16 Indian languages. Uses hybrid dense + BM25 retrieval with reciprocal rank fusion and structure-aware chunking."
collection: portfolio
order: 6
permalink: /portfolio/lufy-legal-rag
---

**Code:** [github.com/MAUK9086/LUFY-Law_Understandable_For_You](https://github.com/MAUK9086/LUFY-Law_Understandable_For_You) · License: MIT

Problem
------
Legal documents are long, cross-referenced and written in specialised language. Retrieval-augmented generation (RAG) built only on embedding similarity struggles with them. Exact legal terms ("indemnify", "force majeure", clause numbers) matter more than general semantic closeness, and the meaning of a clause depends on the section it sits in.

System
------
- **Input and output:** a PDF, DOCX or TXT contract produces (i) a five-section plain-language summary aimed at a chosen reader, (ii) a red / amber / green risk rating for each clause, and (iii) question answering with citations to the source passages, in English and 16 Indian languages.
- **Structure-aware chunking:** chunks of about 800 characters with 150 characters of overlap, split on paragraph and section boundaries. Legal section headers are detected and attached to every chunk, and overlap between a query and a section heading boosts retrieval.
- **Hybrid retrieval:** dense retrieval (all-MiniLM-L6-v2 embeddings in ChromaDB) and BM25 lexical retrieval are merged by Reciprocal Rank Fusion, score(d) = Σ 1 / (60 + rank(d)). A cross-encoder re-ranker (ms-marco-MiniLM-L-6-v2) then selects the final context passages.
- **Long documents:** documents that fit the context window are processed in a single call. Longer ones use concurrent map-reduce with rate-limit-aware retries.
- **Engineering:** a FastAPI service that pre-loads the embedding and re-ranker models at startup, packaged with Docker and covered by a 31-test pytest suite. Documents are processed in memory and never stored.

Why hybrid retrieval
------
Dense retrieval finds paraphrases but can miss rare exact terms and clause references. BM25 finds exact terms but misses paraphrases. Reciprocal rank fusion combines the two rankings without tuning score scales, and the section-header boost keeps retrieved passages in their legal context. The repository's `DESIGN.md` discusses these design choices in detail.
