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
We explore the hypothesis that
>**fine-tuning a model to maximize benchmark
performance may unintentionally strengthen sycophantic behavior**,
shifting the model toward conformity-based reasoning rather than genuine truth-seeking.

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

<div style="border: 1px solid #ddd; border-radius: 8px; padding: 16px;
margin-bottom: 20px;">
  <h4 style="margin-top: 0;">Problem Identification & Research Motivation</h4>
  <p style="margin: 0;">
    A detailed walkthrough of the research gap, conceptual
    framing, and why benchmark-driven sycophancy represents an overlooked
    alignment risk.<br><br>
    <a href="01_problem_definition_and_review/problem_identification.pdf"><strong>
    Open Problem Identification</strong></a>
  </p>
</div>

<div style="border: 1px solid #ddd; border-radius: 8px; padding: 16px;">
  <h4 style="margin-top: 0;"> Background & Literature Review</h4>
  <p style="margin: 0;">
    A curated review of prior research on RLHF, sycophancy, benchmark
    optimization, and behavioral alignment dynamics.<br><br>
    <a href="01_problem_definition_and_review/literature_background_review.pdf"><strong>
     Open Literature Review</strong></a>
  </p>
</div>

---

## Repository Structure

``` bash
├── 01_problem_definition_and_review/# Problem identification + literature
review  
├── 02_datasets/                         # Datasets, preprocessing, links  
├── 03_model_evaluation_and_finetuning/# pre and post evaluation notebooks and
fine-tuning  
├── results/                              # Outputs, plots, metrics, analysis  
├── requirements.txt                       # Dependencies  
└── README.md                   # You're reading it
```

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

## Reproducibility & Environment Setup

To ensure full reproducibility of all
notebook runs, this
repository includes a `requirements.txt` file containing the exact library
versions used during model training and evaluation.

Before running any notebook, install all dependencies with:

```bash
pip install -r requirements.txt
