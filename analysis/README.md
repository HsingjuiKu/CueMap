# Task Clustering and Modeling Preference Analysis in Chatbot Arena Dataset

This repository contains a modular pipeline to cluster prompt tasks, compare clustering strategies, and evaluate large language model (LLM) performance in the Chatbot Arena dataset. The project culminates in modeling tasks that predict LLM winners and hardness scores, enabling interpretability and fairness-aware analysis.

---

## Notebooks Overview

### Clustering and Analysis

- **`cluster.ipynb`**  
  Generates cluster IDs from topic modeling outputs using sentence embeddings, UMAP, and K-Means. Outputs an augmented training and test dataset with `cluster_id`.

- **`model_compare.ipynb`**  
  Compares two clustering methods (K-Means vs. BERTopic + HDBSCAN) using metrics and qualitative visualization.

- **`winner_distribution.ipynb`**  
  Visualizes per-cluster winner model distributions to detect preference bias across task types.

---

## Data Processing and Labeling

- **`data_cleaning.ipynb`**  
  Loads and merges six datasets, cleans NA values, deduplicates, and joins topic modeling, hardness, and clustering results. Produces `complete_data_for_tasks_undeciphered`.

- **`cluster_meaning.ipynb`**  
  Assigns human-readable labels to clusters based on semantic rules. Outputs `complete_data_for_tasks_deciphered`, used in all modeling tasks.

- **`eda.ipynb`**  
  Conducts exploratory data analysis (EDA) to motivate feature engineering for Tasks A and B using the deciphered dataset.

---

## Modeling Tasks

- **`taskA_winner_classification.ipynb`**  
  Predicts which LLM wins (model A or B) for a given prompt using engineered features. Trains and validates a classifier with and without cluster features. Outputs predictions as `taskA_results`.

- **`taskB_hardness_score_prediction.ipynb`**  
  Predicts prompt hardness scores using regression. Incorporates embeddings and features from Task A (`taskA_results`). Outputs predictions as `taskB_results`, and final merged results as `ready_to_submit_tasks_AB`.
