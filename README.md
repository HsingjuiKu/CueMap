# CueMap

CueMap is the research code and data workspace for **Task-Aware Delegation Cues for LLM Agents**. The project studies how offline pairwise preference data can be transformed into task-aware signals that help people decide when to delegate to an LLM agent, when to request an auditor, and when extra verification is needed.

The core idea is to move beyond a single global model ranking. CueMap first induces an interpretable task taxonomy from Chatbot Arena prompts, then estimates task-conditioned model behavior:

- **Capability Profiles**: per-task win-rate maps that describe which models tend to perform well for a given task cluster.
- **Coordination-Risk Cues**: per-task disagreement or tie-rate priors that flag prompts where collaboration may be brittle.
- **Delegation Signals**: lightweight cues that can support adaptive routing, common-ground verification, rationale disclosure, and accountability logs.

## Paper

- **Title**: Task-Aware Delegation Cues for LLM Agents
- **Author**: Xingrui Gu
- **arXiv**: [arXiv:2603.11011](https://arxiv.org/abs/2603.11011)
- **PDF**: [https://arxiv.org/pdf/2603.11011](https://arxiv.org/pdf/2603.11011)
- **DOI**: [10.48550/arXiv.2603.11011](https://doi.org/10.48550/arXiv.2603.11011)

## Repository Structure

```text
CueMap/
+-- analysis/
|   +-- data_cleaning.ipynb
|   +-- cluster.ipynb
|   +-- cluster_meaning.ipynb
|   +-- eda.ipynb
|   +-- winner_distribution.ipynb
|   +-- model_compare.ipynb
|   +-- taskA_winner_classificiation.ipynb
|   +-- taskB_hardness_score_prediction.ipynb
+-- data/
|   +-- complete_data_for_tasks_deciphered.csv
|   +-- complete_data_for_tasks_undeciphered.csv
|   +-- hayden_cluster_train.csv
|   +-- hayden_cluster_test.csv
|   +-- prompt_embeddings.npy
|   +-- response_a_embeddings.npy
|   +-- response_b_embeddings.npy
|   +-- taskA_results.csv
|   +-- taskB_results.csv
|   +-- ready_to_submit_tasks_AB.csv
+-- figures/
    +-- Figure1.png
    +-- ...
    +-- all_clusters.png
```

## Analysis Pipeline

1. **Data cleaning**  
   `analysis/data_cleaning.ipynb` merges Chatbot Arena pairwise comparisons, prompt/response embeddings, GPT-generated task topics, and prompt hardness scores.

2. **Task clustering**  
   `analysis/cluster.ipynb` embeds unique task topics with SentenceTransformers, reduces them with UMAP, and groups them into 30 semantic task clusters using K-Means.

3. **Cluster interpretation**  
   `analysis/cluster_meaning.ipynb` maps numeric cluster IDs to human-readable labels such as `Mathematics, Mathematical`, `Programming, Python`, `Logic, Reasoning`, and `Storytelling, Role-playing`.

4. **Exploratory analysis**  
   `analysis/eda.ipynb` and `analysis/winner_distribution.ipynb` examine task distributions, winner distributions, hardness scores, model win rates, and per-cluster model preference patterns.

5. **Predictive probes**  
   `analysis/taskA_winner_classificiation.ipynb` predicts pairwise winners, while `analysis/taskB_hardness_score_prediction.ipynb` predicts prompt hardness. These probes test whether task clusters carry useful structure for delegation-related decisions.

## Outputs

- `data/complete_data_for_tasks_deciphered.csv`: cleaned training data with readable task cluster labels.
- `data/hayden_cluster_test_deciphered.csv`: test prompts with readable cluster labels.
- `data/taskA_results.csv`: predicted winner labels for Task A.
- `data/taskB_results.csv`: predicted hardness scores for Task B.
- `data/ready_to_submit_tasks_AB.csv`: merged Task A and Task B output.
- `figures/all_clusters.png`: model winner distributions across task clusters.

## Citation

If you use this repository or build on the CueMap analysis, please cite:

```bibtex
@article{gu2026task,
  title={Task-Aware Delegation Cues for LLM Agents},
  author={Gu, Xingrui},
  journal={arXiv preprint arXiv:2603.11011},
  year={2026}
}
```

## License

No license has been specified yet. Please contact the author before reusing or redistributing the repository contents.
