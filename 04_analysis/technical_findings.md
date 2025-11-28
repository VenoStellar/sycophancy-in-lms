# Technical Findings: Sycophancy Trade-offs in Llama-2-7B Fine-Tuning

## Experimental Summary

An analysis of isolated LoRA adapters for Llama-2-7B, fine-tuned on specific
benchmarks (GSM8K, MMLU, HellaSwag, TruthfulQA) and a multi-task Combined
adapter, reveals a strong domain-dependent performance-alignment trade-off.
Optimization for general capability or truthfulness systematically increases
sycophancy, while mathematical reasoning training demonstrates a protective effect.

## Key Results

### 1. Domain-Specific Performance-Sycophancy Correlation

- **TruthfulQA:** Strong positive correlation with increased
sycophancy (`Are You Sure`: r=0.718, `Feedback`: r=0.771). Truthfulness
optimization is the primary driver of agreement-seeking and confidence erosion.
- **GSM8K:** Strong negative correlation with sycophancy (`Are You Sure`: r=-0.805,
- `Feedback`: r=-0.613). Mathematical reasoning training consistently reduces
susceptibility to user influence.
- **MMLU:** Minimal correlation (r ≈ 0.08–0.11). General knowledge improvements
are effectively neutral to alignment.
- **HellaSwag:** Mixed correlations, with a moderate positive link to `Feedback`
sycophancy (r=0.651).

### 2. Quantified Sycophancy Shifts

- **Combined Adapter:** Exhibits the most severe trade-off:
  - Average benchmark performance: +0.183
  - Average sycophancy: +0.080
  - `Are You Sure` susceptibility: 0.000 → 0.193 (strongest degradation)
  - `Feedback` conformity: +0.117 (23% increase)
- **GSM8K Adapter:** The only configuration with net protective effect:
  - Average sycophancy: -0.028
  - `Feedback` conformity: -0.023
  - Maintains baseline `Are You Sure` resistance (0.000)
- **Universal Effect:** All adapters reduce `Answer` imitation sycophancy by
30-40%, indicating this behavior is consistently suppressed by fine-tuning.

### 3. Multi-Task Optimization as an Amplifier

The Combined adapter demonstrates that multi-task training aggregates and
amplifies the sycophancy risks inherent in its constituent tasks, particularly
from TruthfulQA and HellaSwag domains. This results in the highest capability
gains paired with the most pronounced alignment degradation.
