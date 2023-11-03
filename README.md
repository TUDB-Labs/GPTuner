<img align='right' src="/assets/gptuner.png" alt="GPTuner logo" width="130">

# GPTuner: A Manual-Reading Database Tuning System via GPT-Guided Bayesian Optimization

- This repository hosts the source code and supplementary materials for our VLDB 2024 submission, "GPTuner: A Manual-Reading Database Tuning System via GPT-Guided Bayesian Optimization". 
- GPTuner collects and refines heterogeneous domain knowledge, unifies a structured view of the refined knowledge, and uses the knowlege to (1) select important knobs, (2) optimize the value range of each knob and (3) explore the optimized space with a novel Coarse-to-Fine Bayesian Optimization Framework.


## System Overview

<img src="/assets/gptuner_overview.png" alt="GPTuner overview" width="800">

**GPTuner** is a manual-reading database tuning system to suggest satisfactory knob configurations with reduced tuning costs. The figure above presents the tuning workflow that involves seven steps:
1. 📌 User provides the DBMS to be tuned (e.g., PostgreSQL or MySQL), the target workload, and the optimization objective (e.g., latency or throughput).
2. 📌 GPTuner collects and refines the heterogeneous knowledge from different sources (e.g., GPT-4, DBMS manuals, and web forums) to construct _Tuning Lake_, a collection of DBMS tuning knowledge.
3. 📌 GPTuner unifies the refined tuning knowledge from _Tuning Lake_ into a structured view accessible to machines (e.g., JSON).
4. 📌 GPTuner reduces the search space dimensionality by selecting important knobs to tune (i.e., fewer knobs to tune means fewer dimensions).
5. 📌 GPTuner optimizes the search space in terms of the value range for each knob based on structured knowledge.
6. 📌 GPTuner explores the optimized space via a novel Coarse-to-Fine Bayesian Optimization framework.
7. 📌 Finally, GPTuner identifies satisfactory knob configurations within resource limits (e.g., the maximum optimization time or iterations specified by users).

## Code Structure
├── configs
│ ├── postgres.ini
│ └── mysql.ini
├── optimization_results
│ ├── temp_results
│ ├── postgres
│ │ ├── coarse
│ │ └── fine
│ └── mysql
├── scripts
│ ├── install_benbase.sh
│ ├── build_benchmark.sh
│ ├── recover_postgres.sh
│ └── recover_mysql.sh
├── knowledge_collection
│ ├── postgres
│ │ ├── target_knobs.txt
│ │ ├── knob_info
│ │ │ ├── system_view.json
│ │ │ └── official_document.json
│ │ ├── knowledge_sources
│ │ │ ├── gpt
│ │ │ ├── manual
│ │ │ ├── web
│ │ │ └── dba
│ │ ├── tuning_lake
│ │ └── structured_knowledge
│ │ ├── special
│ │ └── normal
│ └── mysql
├── example_pool
└── src
├── dbms
│ ├── dbms_template.py
│ ├── postgres.py
│ └── mysql.py
├── knowledge_handler
│ ├── knowledge_preparation.py
│ └── knowledge_transformation.py
├── space_optimizer
│ ├── knob_selection.py
│ ├── default_space.py
│ ├── coarse_space.py
│ └── fine_space.py
├── config_recommender
│ ├── workload_runner.py
│ ├── coarse_stage.py
│ └── fine_stage.py
└── run_gptuner.py