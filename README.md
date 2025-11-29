#

<div align="center">

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=24&pause=1000&color=2D9CCD&width=435&lines=Sycophancy+in+Language+Models)](https://git.io/typing-svg)

</div>

This repository explores sycophancy in language models (LMs), the tendency
of models to agree with user opinions without regard to truth or reasoning.  
We investigate whether fine-tuning on general benchmarks
(e.g., MMLU, GSM8K, HellaSwag, TruthfulQA) affects a model’s susceptibility to
sycophantic responses.

---

## Project Overview

Sycophancy, models agreeing with users even when users are factually wrong, has
become one of the most persistent alignment failures in modern language models.
Most research traces this behavior to RLHF and instruction tuning, arguing that
models learn to please users because they are trained to optimize for human
approval. This framing has shaped almost all discussions about sycophancy
and has left a major gap in how the field understands the problem.

At the same time, the AI community increasingly relies on general capability
benchmarks such as MMLU, GSM8K, TruthfulQA, and HellaSwag to measure progress
and guide model development. These benchmarks are treated as neutral
scoreboards, yet they shape nearly every stage of model optimization. What
remains almost entirely unexplored is whether the push to excel on these
benchmarks creates its own incentive structure, one that might subtly reward
*answer conformity* in a way that resembles the approval-driven loop of RLHF.

This project investigates that overlooked possibility.  
We explore the hypothesis that `fine-tuning a model to maximize benchmark
performance may unintentionally strengthen sycophantic behavior,
shifting the model toward conformity-based reasoning rather than genuine truth-seeking.`

To test this, we fine-tune **Llama-2-7B-Chat** on a suite of general benchmarks
and compare the model’s behavior before and after
tuning using **SycophancyEval**. Our analysis focuses on changes in:

- reasoning independence  
- truth alignment  
- agreement bias when user beliefs are revealed  

By examining whether benchmark gains correlate with increased sycophancy,
the project challenges the assumption that benchmarks are neutral tools of
evaluation. If benchmark-driven optimization contributes to the problem,
it suggests the field may be reinforcing misalignment through the very
metrics meant to measure capability.

### Further Reading

> [Problem Identification & Research Motivation](01_problem_definition_and_review/problem_identification.pdf)
>
> A detailed walkthrough of the research gap, conceptual framing,
>and why benchmark-driven sycophancy may be an overlooked alignment risk.  
>

---

> [Background & Literature Review](01_problem_definition_and_review/literature_background_review.pdf)
>
> A review of prior work on
RLHF, sycophancy, benchmark optimization, and behavioral alignment.  
>

---

## Repository Structure

``` bash
├── 01_problem_definition_and_review/# Problem identification + literature
review  
├── 02_datasets/                         # Datasets, preprocessing, links  
├── 03_model_evaluation_and_finetuning/# pre/post evaluation notebooks + fine-tuning
├── 04_analysis                             # Outputs, plots, metrics, analysis
├── requirements.txt                       # Dependencies  
└── README.md                   # You're reading it
```

---

## Methodology

Our methodology combines model evaluation, targeted dataset construction, and
LoRA-based fine-tuning to measure and reduce sycophancy in instruction-tuned LLMs.

### Model Selection

We selected Llama-2 7B Chat as the model under investigation. Sycophancy
behaviors are most visible in instruction-tuned models (especially after
supervised fine-tuning and RLHF), which aligns with findings in current literature.

### Benchmark Evaluation

We used two evaluation categories:

1) General Capability Benchmarks
These measure knowledge, reasoning, and factual alignment before and after
fine-tuning:  
– MMLU (57-domain general knowledge)  
– GSM8K (math reasoning)  
– HellaSwag (commonsense reasoning)  
– TruthfulQA (misinformation resistance)

2) Sycophancy Benchmarks
These are designed specifically to measure behavior changes when user
preferences are injected:  
– Feedback: does the model stop identifying logical fallacies when the user
says they “like” the argument?  
– Are You Sure: does the model change its answer simply because the user
expresses doubt?  
– Answer Manipulation: does the model shift from a correct answer to a
user-suggested incorrect one?

*Each evaluation uses controlled pairs of prompts (neutral vs. user-biased) and
compares model behavior.*

i) **Dataset Construction**  
We created a focused fine-tuning dataset targeting sycophancy-prone scenarios.
The dataset includes:

- arguments with and without explicit logical fallacies
- QA examples designed to test answer stability
- preference-injected prompts that model must resist
- All samples follow a consistent instruction–response dialog format.

ii) **Fine-Tuning Procedure**  
We applied LoRA (Low-Rank Adaptation) to fine-tune the model efficiently without
modifying the full weights.
Training followed:  

- supervised fine-tuning on the curated anti-sycophancy dataset
- monitoring loss and response patterns
- preserving base model general capability through light-touch adaptation

iii) **Post-Training Evaluation**  

After fine-tuning, we repeated:

- all general benchmarks
- all sycophancy benchmark tests
- comparison of before/after behavior, including confidence intervals

*We also conducted qualitative inspection of edge cases such as:*

- *ambiguous answers*
- *shifts in sentiment*
- *fallacy detection consistency*

> **Implementation:**  
All evaluation and fine-tuning logic is implemented in the
[`03_model_evaluation_and_finetuning/`](03_model_evaluation_and_finetuning)
folder, which contains notebooks and
scripts for:  
>
>- Baseline benchmark and sycophancy evaluation (`baseline_model_evaluations/`)
>- LoRA fine-tuning adapters and post-fine-tuning evaluation (`finetuning_and_post_evaluation/`)

---

## Findings & Conclusion

Our investigation shows that fine-tuning Llama-2-7B-Chat is not behaviorally
neutral. Capability improvements reshape the model’s tendencies in
domain-specific ways, with sycophancy emerging as a measurable trade-off in
several training settings.

### Key Findings

Fine-tuning on broad, ambiguous, or socially framed benchmarks particularly
**TruthfulQA** consistently increased sycophantic behavior. The model became more
likely to revise correct answers when questioned (Are-You-Sure tests) and to
change responses based on user dissatisfaction (Feedback tests).  

The **Combined** multi-task adapter amplified these effects:  

- Average performance gain: **+0.183**  
- Average sycophancy increase: **+0.080**  
- Are-You-Sure susceptibility rose from **0.000 → 0.193**  
- Feedback conformity increased by **23%**  

These results indicate that improving “helpfulness” or “truthfulness” on certain
benchmarks can unintentionally strengthen patterns of deference where the model
becomes more compliant with user framing rather than more robustly accurate.

In contrast, **GSM8K (mathematical reasoning)** was the clear exception. It
showed strong *negative* correlations with sycophancy and was the only adapter
that reduced these behaviors:  

- Are-You-Sure correlation: **r = –0.805**  
- Feedback sycophancy: **r = –0.613**  
- Net sycophancy change: **–0.028**  

This demonstrates that domains with objective, verifiable answers reinforce
stable, independent reasoning rather than conformity.

### Conclusion

Fine-tuning does more than boost benchmark scores it changes the model’s
behavioral priors. Some capability gains introduce meaningful
alignment risks, while others (like mathematical reasoning) appear protective.

This suggests that **what** a model is trained on matters as much as
**how well** it performs. Developers should treat benchmark selection as a
strategic decision with direct consequences for model behavior. Capability and
alignment do not always move together, and improving performance on certain tasks
can come at the cost of increased user-dependent conformity.

A more deliberate approach to fine-tuning is necessary if we want models that
are both capable and consistently independent in their reasoning.
> All quantitative results, correlation tables, plots, and post–fine-tuning
evaluation outputs are available in the **[`analysis`](04_analysis/)** folder.

---

## Limitation

1) **Model Scale**  
All results are based on LLaMA-2 7B, so findings may not generalize to larger
models with different RLHF dynamics.

2) **Benchmark Scope**  
The benchmarks used focus on structured tasks and do not reflect the open-ended
dialogue contexts where sycophancy often appears.

3) **Measurement Limits**  
SycophancyEval captures only a subset of sycophantic behaviors and may
oversimplify real user–model interactions.

4) **Short-Term Effects**  
The study measures immediate post-fine-tuning behavior and does not examine
longer-term stability or drift.

5) **Initialization Bias**  
Starting from LLaMA-2 7B Chat means the model already carries RLHF-induced
sycophancy, so effects cannot be isolated to our fine-tuning alone.

---

## Reproducibility & Environment Setup

For full reproducibility, install the exact library versions from [`requirements.txt`](requirements.txt).

**Prerequisites:**

- Python 3.10+
- GPU access (highly recommended; this project is developed on Google Colab Pro+)

**Quick Start:**

1. **Clone and enter the repo:**

    ```bash
    git clone https://github.com/VenoStellar/sycophancy-in-lms.git
    cd sycophancy-in-lms
    ```

2. **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3. **Setup Model:** Have the Hugging Face `Llama-2-7B-Chat` model accessible.
4. **Run Notebooks** (in order):
    - [`03_model_evaluation_and_finetuning/baseline_model_evaluations/`](03_model_evaluation_and_finetuning/baseline_model_evaluations)
For baseline tests.
    - [`03_model_evaluation_and_finetuning/finetuning_and_post_evaluation/`](03_model_evaluation_and_finetuning/finetuning_and_post_evaluation)
For fine-tuning and evaluation.
    - Results and full analysis script in [`04_analysis/`](04_analysis) folder.
