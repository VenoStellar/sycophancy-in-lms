# Fine-Tuning and Post-Evaluation

This folder contains notebooks for fine-tuning the baseline language model using
adapters and evaluating the model's performance after fine-tuning. Each adapter
includes a **post-sycophancy evaluation** to assess changes in the model's
behavior and bias after training. The folder also includes a combined adapter
evaluation to understand performance improvements across tasks.

## Notebooks

### 1. [`fine_tuning.ipynb`](fine_tuning.ipynb)

**Purpose:**  

This notebook performs general fine-tuning of the baseline language model using
adapters. It sets up the training pipeline, defines hyperparameters, and trains
the model on relevant datasets to improve performance on targeted benchmarks.

### 2. [`gsm8k_adapter_evaluation.ipynb`](gsm8k_adapter_evaluation.ipynb)

**Purpose:**  

This notebook fine-tunes the model for the GSM8K benchmark using a dedicated
adapter and evaluates its performance. It also includes a **post-sycophancy
evaluation** to analyze whether fine-tuning affected the model's tendency to give
overly agreeable or biased answers.

### 3. [`mmlu_adapter_evaluation.ipynb`](mmlu_adapter_evaluation.ipynb)

**Purpose:**  

This notebook fine-tunes and evaluates the model for the MMLU benchmark with a
dedicated adapter. It includes **post-sycophancy evaluation** to measure changes
in model behavior after fine-tuning.

### 4. [`truthfulqa_adapter_evaluation.ipynb`](truthfulqa_adapter_evaluation.ipynb)

**Purpose:**  

This notebook fine-tunes the model for the TruthfulQA benchmark using an adapter.
It evaluates improvements in factual accuracy and conducts **post-sycophancy
analysis** to detect behavioral changes after fine-tuning.

### 5. [`hellaswag_adapter_evaluation.ipynb`](hellaswag_adapter_evaluation.ipynb)

**Purpose:**  

This notebook fine-tunes the model for the HellaSwag benchmark using an adapter.
It focuses on improving commonsense reasoning and performs **post-sycophancy
evaluation** to assess any shifts in model bias or agreeableness.

### 6. [`combined_adapter_evaluation.ipynb`](combined_adapter_evaluation.ipynb)

**Purpose:**  

This notebook evaluates the model using a combination of all task-specific
adapters. It provides an overview of model performance across multiple benchmarks
and includes **post-sycophancy evaluation** to understand behavioral impacts when
multiple adapters are used simultaneously.
