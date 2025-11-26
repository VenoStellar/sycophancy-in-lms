# Datasets folder

This folder contains all datasets and data outputs used in the evaluation and
fine-tuning pipeline for analyzing the influence of general benchmarks on
sycophantic behavior in language models.

The structure emphasizes traceability, separation of concerns, and experimental reproducibility.

---

## Directory Overview

```text
02_datasets/
├── 01_raw_sources/
│   ├── sycophancy_eval/
│   │   ├── answer.jsonl
│   │   ├── are_you_sure.jsonl
│   │   └── feedback.jsonl
│   └── general_benchmarks_metadata.md
│
├── 02_general_benchmarks_splits/
│   ├── test_splits/
│   │   ├── gsm8k_test.json
│   │   ├── mmlu_test.json
│   │   ├── truthfulqa_test.json
│   │   └── hellaswag_test.json
│   └── train_splits/
│       ├── gsm8k_train.json
│       ├── mmlu_train.json
│       ├── truthfulqa_train.json
│       └── hellaswag_train.json
│
├── 03_sycophancy_samples/
│   ├── sycophancy_test_samples.json
│   ├── feedback_sycophantic_examples.json
│   └── answer_sycophantic_examples.json
│
└── 04_results/
    ├── pre_fine_tuning/
    │   ├── baseline_gsm8k_mmlu.json
    │   ├── baseline_truthfulqa_hellaswag.json
    │   └── sycophancy_baseline_results.json
    └── post_fine_tuning/
        ├── gsm8k_results.json
        ├── mmlu_results.json
        ├── truthfulqa_results.json
        ├── hellaswag_results.json
        └── all_benchmarks_results.json
```

---

## [01_raw_sources/](01_raw_sources)

Original, unaltered data sources. These files are never modified directly and
serve as the foundation for all derived datasets.

<details>
<summary><strong>Contents</strong></summary>

[**sycophancy_eval/**](01_raw_sources/sycophancy_eval)
Raw sycophancy evaluation datasets in JSONL format:

* `answer.jsonl`
* `are_you_sure.jsonl`
* `feedback.jsonl`

[**general_benchmarks_metadata.md**](01_raw_sources/general_benchmarks_metadata.md)
Documentation file containing source information for general benchmarks.

</details>

---

## [02_general_benchmarks_splits/](02_general_benchmarks_splits)

Standardized and structured versions of benchmark datasets prepared for
experimental use.

<details>
<summary><strong>Structure</strong></summary>

[**test_splits/**](02_general_benchmarks_splits/test_splits)
Contains evaluation-only data:

* `gsm8k_test.json`
* `mmlu_test.json`
* `truthfulqa_test.json`
* `hellaswag_test.json`

[**train_splits/**](02_general_benchmarks_splits/train_splits)
Contains fine-tuning data for adapter training:

* `gsm8k_train.json`
* `mmlu_train.json`
* `truthfulqa_train.json`
* `hellaswag_train.json`

</details>

---

## [03_sycophancy_samples/](03_sycophancy_samples)

Curated subsets for qualitative inspection and behavioural illustration.

<details>
<summary><strong>Files</strong></summary>

* `sycophancy_test_samples.json`
  Controlled subset used for explicit sycophancy evaluation.

* `feedback_sycophantic_examples.json`
  20 detected sycophantic responses from the Feedback dataset.

* `answer_sycophantic_examples.json`
  20 detected sycophantic responses from the Answer dataset.

</details>

<details>
<summary><strong>Analytical Role</strong></summary>

These samples serve as interpretive anchors and are used to:

* Illustrate behavioural failures
* Support narrative analysis in reports
* Contextualise quantitative metrics

They are not used for training purposes.

</details>

---

## [04_results/](04_results)

All experimental outputs produced during evaluation and adapter fine-tuning.

### [pre_fine_tuning/](04_results/pre_fine_tuning)

Baseline Evaluations output from the original model prior to any fine-tuning.

<details>
<summary><strong>Files</strong></summary>

* `baseline_gsm8k_mmlu.json`
* `baseline_truthfulqa_hellaswag.json`
* `sycophancy_baseline_results.json`

</details>

### [post_fine_tuning/](04_results/post_fine_tuning)

Evaluation outputs for each LoRA adapter.

<details>
<summary><strong>Adapters Evaluated</strong></summary>

* Benchmark-specific:

  * `gsm8k_results.json`
  * `mmlu_results.json`
  * `truthfulqa.json`
  * `hellaswag_results.json`

* `all_benchmarks_results` : Combined adapter trained on all benchmarks

</details>

---

## Data Flow Logic

```text
Raw Sources → Structured Splits → Fine-Tuning → Evaluation → Analytical Samples
```

This linear separation allows controlled experimentation
and precise interpretation of behavioural changes.

---
