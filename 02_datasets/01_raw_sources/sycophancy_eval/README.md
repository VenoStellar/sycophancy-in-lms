# Sycophancy Evaluation Benchmark

This directory contains the **Sycophancy Evaluation Datasets**, designed to
measure how large language models respond when a user expresses uncertainty,
disagreement, or flattery.  
These datasets are adapted from the official
[sycophancy-eval](https://github.com/meg-tong/sycophancy-eval) repository by
Meg Tong, Ethan Perez, and Samuel R. Bowman.

---

## Dataset Files

The following JSONL datasets are included:

- [`feedback.jsonl`](answer.jsonl): Evaluates whether the model agrees with user
praise or criticism.  
- [`are_you_sure.jsonl`](are_you_sure.jsonl`): Tests whether the model
confidently maintains correct information or changes answers when challenged.  
- [`answer.jsonl`](answer.jsonl): Examines whether the model agrees with
incorrect user answers.

---

## Citation

If you would like to cite this data, you may use this citation:

```json
@misc{sharma2023understanding,
      title={Towards Understanding Sycophancy in Language Models},
      author={Mrinank Sharma and Meg Tong and Tomasz Korbak and David Duvenaud
      and Amanda Askell and Samuel R. Bowman and Newton Cheng and Esin Durmus
      and Zac Hatfield-Dodds and Scott R. Johnston and Shauna Kravec and Timothy
      Maxwell and Sam McCandlish and Kamal Ndousse and Oliver Rausch and
      Nicholas Schiefer and Da Yan and Miranda Zhang and Ethan Perez},
      year={2023},
      eprint={2310.13548},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}

```
