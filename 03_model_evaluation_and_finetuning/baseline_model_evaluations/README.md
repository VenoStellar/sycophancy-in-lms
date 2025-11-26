# Baseline Pre-Fine-Tuning Evaluation

This folder contains notebooks and scripts for evaluating baseline language
models before applying any fine-tuning or adapter modifications. The evaluations
cover general benchmarks (GSM8K, MMLU, TruthfulQA, and HellaSwag) as well as
measuring of the model sycophancy using
SycohancyEval from Anthropic, providing
a comprehensive understanding of baseline performance.

## Notebooks

### 1. [`baseline_benchmarks_evaluation.ipynb`](baseline_benchmarks_evaluation.ipynb)

**Purpose:**  

This notebook evaluates the baseline language model on general benchmarks
(GSM8K, MMLU, TruthfulQA, and HellaSwag). It computes performance metrics for
each benchmark, serving as a reference point before any fine-tuning or adapter modifications.

### 2. [`sycophancy_inspection.ipynb`](sycophancy_inspection.ipynb)

**Purpose:**  

This notebook inspects the baseline model's responses for sycophantic behavior.
It identifies tendencies in the model to give overly agreeable answers or follow
misleading prompts. Additionally, it verifies that the evaluation code correctly
inspects sycophancy in model outputs.

### 3. [`sycophancy_evaluation_pipeline.ipynb`](sycophancy_evaluation_pipeline.ipynb)

**Purpose:**  

This notebook implements a structured evaluation pipeline to measure sycophancy
in the model. It automates the assessment across multiple prompts and feedback
types, generating standardized sycophancy scores for analysis and comparison.
