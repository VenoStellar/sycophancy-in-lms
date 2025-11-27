# Benchmark Datasets Metadata

This document summarizes the benchmark datasets used in the project.  
Each dataset includes metadata inside an expandable section.

---

## GSM8K (Grade School Math 8K)

A dataset of math word problems designed to evaluate reasoning
and problem-solving abilities in language models.

<details>
<summary><strong>Metadata</strong></summary>

**• Source**: <https://huggingface.co/datasets/openai/gsm8k>  
**• Split**: Train / Test  
**• License**: MIT  
**• Approx size**: ~10K - 100K  
**• Format**: JSON (question, answer)

```json
{ "question": "If Tom has 5 apples and buys 3 more, how many 
does he have?", "answer": "8" }
```

</details>

---

## MMLU (Massive Multitask Language Understanding)

A multitask benchmark covering 57 subjects across STEM,
humanities, social sciences, and professional domains.

<details>
<summary><strong>Metadata</strong></summary>

**• Source**: <https://huggingface.co/datasets/cais/mmlu>  
**• Split**: Train / Test (per subject)  
**• License**: MIT  
**• Approx size**: ~10K - 100K  
**• Format**: JSON (question, choices, answer)

```json

{
  "question": "What is the chemical symbol for gold?",
  "choices": ["Au", "Ag", "Gd", "Pb"],
  "answer": "Au"
}
```

</details>

---

## TruthfulQA

A dataset built to test models’ resistance to
common misconceptions, misleading assumptions, and factual inaccuracies.

<details>
<summary><strong>Metadata</strong></summary>

**• Source**: <https://huggingface.co/datasets/truthfulqa/truthful_qa>  
**• Split**: Validation (MC and generative variants)  
**• License**: apache-2.0  
**• Approx size**: ~1k-10k  
**• Format**: JSON (question, correct_answer or choices)

```json

{
  "question": "Can humans breathe in space without a spacesuit?",
  "correct_answer": "No"
}
```

</details>

---

## HellaSwag

A commonsense reasoning benchmark where models must choose the
most plausible continuation of a scenario.

<details>
<summary><strong>Metadata</strong></summary>

**• Source**: <https://huggingface.co/datasets/Rowan/hellaswag>  
**• Split**: Train / Validation/ test  
**• License**: MIT  
**• Approx size**: ~10k-100k  
**• Format**: JSON (ctx, endings, label)

```json

{
  "ctx": "The cat climbed the tree because it was scared of the dog.",
  "endings": [
    "It scratched the dog.",
    "It ran down the tree.",
    "It hid in the branches.",
    "It meowed loudly."
  ],
  "label": 2
}

```

</details>
