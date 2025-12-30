# CueMap

**Task-Aware Signaling for Human–Agent Delegation**

This repository contains the analysis code and artifacts for our paper on deriving **task-conditioned collaboration signals** (Capability Profiles and Coordination-Risk Cues) from large-scale human preference data (Chatbot Arena), and validating them via two predictive probes:
- **Task A:** Winner prediction (multinomial logistic regression)
- **Task B:** Difficulty prediction (ridge regression)

---

## Repository Structure

- `analysis/` — notebooks for the full pipeline
  - `data_cleaning.ipynb` — load/clean Arena comparisons; export `complete_data_for_tasks_*.csv`
  - `cluster.ipynb` — embed → reduce → KMeans (K=30); export cluster assignments
  - `cluster_meaning.ipynb` — interpret clusters (keywords/labels) for reporting
  - `winner_distribution.ipynb` — task-conditioned winner distributions (Capability Profile Map)
  - `taskA_winner_classificiation.ipynb` — Task A: winner prediction (multinomial logistic regression)
  - `taskB_hardness_score_prediction.ipynb` — Task B: difficulty prediction (ridge regression)
  - `model_compare.ipynb` — regularization sweep + ablations summary
  - `eda.ipynb` — dataset sanity checks / descriptive stats

- `data/` — processed datasets and embeddings
  - `prompt_embeddings.npy`, `response_a_embeddings.npy`, `response_b_embeddings.npy`
  - `complete_data_for_tasks_undeciphered.csv` / `..._deciphered.csv`
  - `hayden_cluster_train.csv`, `hayden_cluster_test.csv` (+ `_deciphered`)
  - `ready_to_submit_tasks_AB.csv`
  - `taskA_results.csv`, `taskB_results.csv`

- `figures/` — paper figures (`Figure1.png` ... `Figure13.png`, `all_clusters.png`)

## Quickstart (Notebooks)

> Recommended order to reproduce paper signals + experiments:

1. **Data preparation**
   - Run: `analysis/data_cleaning.ipynb`
   - Outputs: cleaned comparison tables in `data/complete_data_for_tasks_*.csv`

2. **Task typing (K=30)**
   - Run: `analysis/cluster.ipynb`
   - Outputs: cluster assignments + train/test splits
     - `data/hayden_cluster_train.csv`
     - `data/hayden_cluster_test.csv`

3. **Signals for collaboration**
   - Capability profiles (task-conditioned win patterns):
     - Run: `analysis/winner_distribution.ipynb`
     - Outputs: `figures/Figure5.png` (Capability Profile Map)
   - Coordination-risk cue (tie-rate / difficulty proxy by cluster):
     - Run: `analysis/taskB_hardness_score_prediction.ipynb` (also produces risk-related plots)
     - Outputs: `figures/Figure7.png` (Coordination Risk by Task Type)

4. **Validation probes (Experiments)**
   - **Task A: winner prediction**
     - Run: `analysis/taskA_winner_classificiation.ipynb`
     - Outputs: `data/taskA_results.csv`
   - **Task B: difficulty prediction**
     - Run: `analysis/taskB_hardness_score_prediction.ipynb`
     - Outputs: `data/taskB_results.csv`
   - Regularization sweep + cluster-feature ablation summary:
     - Run: `analysis/model_compare.ipynb`

## Key Outputs (for the paper)

- **Task taxonomy visualization**
  - `figures/Figure1.png` / `figures/all_clusters.png`

- **Capability Profile Map (winner vote distribution by cluster)**
  - `figures/Figure5.png`

- **Coordination Risk (uncertainty proxy by cluster)**
  - `figures/Figure7.png`

- **Experiment summaries**
  - `data/taskA_results.csv` (Task A: accuracy under CV / settings)
  - `data/taskB_results.csv` (Task B: MSE under CV / settings)

## Data Notes

- The dataset is derived from Chatbot Arena pairwise comparisons (single-turn prompts).
- Labels include `{A, B, tie, invalid}` and are used directly in Task A.
- Difficulty scores (1–10) are used for Task B where available.

## Citation

If you use this codebase, please cite the associated paper/preprint included with this repository.

## License

Research code released for reproducibility. Add your preferred license file if publishing.
