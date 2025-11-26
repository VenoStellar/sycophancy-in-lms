# Model Evaluation and Fine-Tuning

This folder contains the full workflow for evaluating and fine-tuning a baseline
language model. It is organized into two main subfolders: one for
**baseline evaluation** and another for **fine-tuning with adapters and
post-evaluation**. The structure allows tracking model performance, analyzing
behavioral tendencies (sycophancy), and measuring again after fine-tuning.

## Folder Structure

**03_model_evaluation_and_finetuning/**  
├── **baseline_benchmarks_evaluation/**  
│   ├── `baseline_benchmarks_evaluation.ipynb`  
│   ├── `sycophancy_inspection.ipynb`  
│   └── `sycophancy_evaluation_pipeline.ipynb`  
│  
└── **finetuning_and_post_evaluation/**  
│   ├── `finetuning.ipynb`  
│   ├── `GSM8K_adapter.ipynb`  
│   ├── `MMLU_adapter.ipynb`  
│   ├── `TruthfulQA_adapter.ipynb`  
│   ├── `HellaSwag_adapter.ipynb`  
│   └── `combined_adapters_evaluation.ipynb`

## Overview

### 1. Baseline Evaluation

The `baseline_benchmarks_evaluation` folder contains notebooks to assess the
**baseline model performance** on general benchmarks
(GSM8K, MMLU, TruthfulQA, HellaSwag) and analyze **sycophancy**. This
establishes a reference for model capabilities and behavioral tendencies before
any fine-tuning or adapter modifications.  
For details, see the [Baseline README](baseline_model_evaluations/README.md).

### 2. Fine-Tuning and Post-Evaluation

The `finetuning_and_post_evaluation` folder contains notebooks to **fine-tune
the model** using adapters for specific benchmarks. Each adapter notebook also
includes **post-sycophancy evaluation** to measure changes in model behavior.  
Additionally, a combined adapter evaluation assesses performance and behavioral
impacts when multiple adapters are used together.  
For details, see the [Fine-Tuning README](finetuning_and_post_evaluation/README.md).
