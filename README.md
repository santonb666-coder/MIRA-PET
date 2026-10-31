# MIRA-PET

MIRA-PET is a multi-agent iterative quality-control framework for whole-body PET/CT report generation. It coordinates report drafting, quality assessment, and iterative refinement to support structured radiology reporting.

This repository accompanies the main experimental comparison in Table 2 of *MIRA-PET: An Iterative Multi-Agent Framework for Whole-Body PET/CT Analysis and Structured Report Generation*.

## Contents

| File | Description |
| --- | --- |
| `pseudocode.md` | A conceptual illustration of the multi-agent refinement loop. |
| `outputs/mira_pet_test.jsonl` | Fixed MIRA-PET predictions paired with reference reports for 505 evaluated cases. |
| `results/main_metrics.csv` | The 14 main-comparison rows reported in manuscript Table 2, with scores rounded to four decimal places. |

Each JSONL record contains exactly three fields: `sample_id`, `reference_report`, and `generated_report`. Sample identifiers are local to this release. The generated reports preserve the archived final outputs, including their consistency annotations and diagnostic metadata.

## Workflow

The pseudocode presents functional agent roles and a simplified refinement loop. Retrieved reference cases are included as a conceptual input, rather than an implemented or evaluated retrieval module. Detailed quality-scoring rules, stopping criteria, and report selection are described in Section 3.4 of the current manuscript.

## Fixed-output evaluation

The paired reports support independent offline re-evaluation of the MIRA-PET outputs. Re-scoring should use the study's text normalization, tokenization, clinical-status extraction, and aggregation settings:

- Textual metrics and ClinKappa are averaged over the 505 cases. For textual evaluation, remove consistency suffixes and diagnostic metadata using the study's normalization procedure.
- Clinical entity counts are extracted from the archived report text and accumulated across cases for each uptake category. CE-PRE and CE-REC are the category-macro precision and recall; CE-F1 is their harmonic mean.

These aggregation settings define the MIRA-PET row in Table 2. The other CSV rows preserve the baseline values reported in the manuscript; the released JSONL contains MIRA-PET predictions.

## Data and acknowledgements

The benchmark and reference reports originate from [PET2Rep](https://github.com/YichiZhang98/PET2Rep). Original PET/CT images are distributed through the upstream project's dataset access instructions and are not bundled here. Dataset access and use follow the upstream terms.

Ablation experiment results are presented in manuscript Table 3.
