# Analysis: Benchmark Performance and Sycophancy Trade-offs

This folder contains the complete analysis of behavioral changes in Llama-2-7B after
domain-specific fine-tuning. The analysis examines the relationship
between benchmark performance improvements and alignment properties, specifically
measuring changes in sycophantic behavior across three dimensions: Feedback,
Are You Sure, and Answer imitation.

## Folder Structure

**analysis/**  
├── `analysis.ipynb`  
├── `analysis_figures/`  
│   ├── `benchmark performance.png`  
│   ├── `sycophacy across all adapters.png`  
│   ├── `detailed sycophancy bar analysis.png`  
│   ├── `heatmap correlation.png`  
│   ├── `trade-off analysis.png`  
│   ├── `progression.png`  
│   ├── `ranking.png`  
│   └── `each adapter analysis.png`  
├── `analysis_results/`  
│   ├── `performance_changes.csv`  
│   ├── `correlation_analysis.csv`  
│   └── `complete_results.csv`  
├── `sycophancy_tradeoffs_summary.md`  
└── `technical_findings.md`

## Overview

### 1. Main Analysis Notebook

The [`analysis.ipynb`](analysis.ipynb) notebook contains the complete
analytical workflow, including:

- Performance comparison between baseline
and fine-tuned adapters across GSM8K, MMLU, TruthfulQA, and HellaSwag
- Sycophancy evaluation across three behavioral dimensions
- Correlation analysis between benchmark performance and alignment changes
- Trade-off visualization and model profiling

### 2. Analysis Results

The [`analysis_results/`](analysis_results) directory contains structured data outputs:

- **`performance_changes.csv`**: Quantitative deltas between baseline and
fine-tuned models
  - Benchmark performance changes (GSM8K, MMLU, TruthfulQA, HellaSwag)
  - Sycophancy behavior changes (Feedback, Are You Sure, Answer)
  - Key finding

- **`correlation_analysis.csv`**: Statistical relationships between
capabilities and alignment
  - TruthfulQA strongly correlates with increased sycophanc
 (Feedback: r=0.718, Are You Sure: r=0.771)
  - GSM8K shows protective effects (Feedback: r=-0.613)
  - HellaSwag has complex mixed correlations

- **`complete_results.csv`**: Comprehensive dataset with raw scores,
changes, and metadata
  - Baseline and fine-tuned model performance across all benchmarks
  - Sycophancy scores and calculated changes
  - Complete experimental records with timestamps

### 3. Analysis Figures

The [`analysis_figures/`](analysis_figures) directory contains all generated visualizations:

- **`benchmark performance.png`**: Comparative performance across GSM8K,
MMLU, TruthfulQA, and HellaSwag for all adapters
- **`sycophacy across all adapters.png`**:
Sycophancy scores comparison across different adapter configurations
- **`detailed sycophancy bar analysis.png`**: Breakdown of sycophancy changes
by type and adapter
- **`heatmap correlation.png`**: Correlation matrix between benchmark performance
and sycophancy dimensions
- **`trade-off analysis.png`**: Scatter plots showing performance-sycophancy
trade-offs by benchmark
- **`progression.png`**: Evolution of sycophancy as benchmark performance improves
- **`ranking.png`**: Adapter rankings based on different
performance-alignment weighting schemes
- **`each adapter analysis.png`**: Individual adapter profiles across all metrics

### 4. Summary Documentation

- [`sycophancy_tradeoffs_summary.md`](sycophancy_tradeoffs_summary.md): High-level
summary of findings and strategic recommendations
- [`technical_findings.md`](technical_findings.md): Concise technical overview with
quantitative results

## Key Findings

The analysis reveals that benchmark optimization produces
predictable, domain-dependent changes in model alignment:

- **TruthfulQA optimization** increases sycophancy despite performance gains
(+0.605 TruthfulQA, +0.080 Feedback sycophancy)
- **Multi-task training (Combined)** amplifies alignment risks
(+0.193 Are You Sure vulnerability)
- **Mathematical reasoning (GSM8K)** reduces sycophancy while improving
target performance (-0.023 Feedback, +0.112 GSM8K)
- **Answer imitation** consistently decreases across all adapters (30-40% reduction)
