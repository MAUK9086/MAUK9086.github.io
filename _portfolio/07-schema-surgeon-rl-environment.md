---
title: "Schema Surgeon: An RL Environment for Database Schema Migration"
excerpt: "A reinforcement-learning environment, built on OpenEnv, in which an agent migrates a messy NoSQL collection to a target JSON schema through rename, cast, flatten and delete actions, with a dense reward and reproducible tasks of increasing difficulty."
collection: portfolio
order: 7
permalink: /portfolio/schema-surgeon
---

**Context:** OpenEnv Hackathon, 2026 (team project). **Code:** [github.com/MAUK9086/Schema_Surgeon_OpenEnv_Meta](https://github.com/MAUK9086/Schema_Surgeon_OpenEnv_Meta)

Motivation
------
Real-world data cleaning involves long sequences of small, irreversible decisions. Benchmarks for language-model agents rarely test this. Schema Surgeon frames schema migration as a sequential decision problem in which the agent acts as a database reliability engineer.

Environment
------
- **State:** a collection of 50 documents with inconsistent schemas. The agent observes a sample of 10 documents plus global key-frequency statistics.
- **Actions:** `rename_and_merge`, `cast_type`, `flatten_field`, `delete_key` and `terminate`.
- **Tasks (30 steps each, increasing difficulty):**
  1. *Key drift*: merge `uid` / `u_id` into `user_id`.
  2. *Type drift*: e.g., cast string-typed ages to integers and prices to floats.
  3. *Nested and ambiguous types*: values such as `"25"`, `true` or `{"val": 25}`, nested fields to flatten, and noise fields to remove.
- **Reward:** dense, equal to the change in the fraction of documents that validate against the target schema. Penalties apply to no-op actions (−0.1) and destructive actions (−0.5).
- **Reproducibility:** fixed datasets per task. The environment is served over a FastAPI WebSocket following the OpenEnv specification.
- **Baseline:** a `gpt-4o-mini` agent starts Task 1 at a score of 0.380 (19 of 50 documents already valid).
