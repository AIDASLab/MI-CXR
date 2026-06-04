<h1 align="center">MI-CXR: A Benchmark for Longitudinal Reasoning over Multi-Interval Chest X-rays</h1>
<h3 align="center">ACL 2026 Findings</h3>
<p align="center">
  <a href="https://arxiv.org/abs/2605.15574"><img src="https://img.shields.io/badge/arXiv-2605.15574-b31b1b.svg" alt="arXiv"></a>
  <a href="https://aidaslab.github.io/MI-CXR/"><img src="https://img.shields.io/badge/Project-Page-blue.svg" alt="Project Page"></a>
  <a href="https://huggingface.co/datasets/steve9712/MI-CXR"><img src="https://img.shields.io/badge/🤗-Dataset-FFD21E.svg" alt="HuggingFace Dataset"></a>
</p>

## Abstract

Longitudinal chest X-ray (CXR) interpretation requires reasoning over disease evolution across multiple patient visits, yet most existing medical VQA benchmarks focus on single images or short-horizon image pairs. We introduce **MI-CXR**, a benchmark for standardized evaluation of **M**ulti-**I**nterval longitudinal reasoning over multi-visit **CXR** sequences, without requiring free-form report generation or additional clinical context.

MI-CXR comprises five-way multiple-choice questions over five-visit patient timelines and instantiates three complementary task families:

- **Temporal Event Localization (TEL)**: Identify *when* clinically meaningful events occur along the timeline.
- **Interval-wise Change Reasoning (ICR)**: Interpret visual changes between consecutive visits.
- **Global Trajectory Summarization (GTS)**: Characterize the overall disease course across the full timeline.

Evaluating 14 state-of-the-art VLMs reveals low overall performance (29.3% accuracy), only modestly above random guessing. These findings highlight key limitations of current VLMs and establish MI-CXR as a principled benchmark for longitudinal medical reasoning.

---

## Dataset

### Access

MI-CXR is constructed on top of **MIMIC-CXR-JPG** and **MIMIC-Ext-CXR-QBA**, both distributed under PhysioNet's credentialed access framework. Users must obtain appropriate PhysioNet credentials and comply with the original data usage agreements.

- MIMIC-CXR-JPG: [https://physionet.org/content/mimic-cxr-jpg/2.1.0/](https://physionet.org/content/mimic-cxr-jpg/2.1.0/)
- MIMIC-Ext-CXR-QBA: [https://physionet.org/content/mimic-ext-cxr-qba/](https://physionet.org/content/mimic-ext-cxr-qba/)

### File Description

- `micxr_test.jsonl`: The MI-CXR test set, containing ~5,311 examples across all three task families.

### Data Fields

Each entry in `micxr_test.jsonl` contains the following fields:

| Field | Description |
|---|---|
| `qid` | Unique identifier for each question instance |
| `group_type` | High-level task category (TEL / ICR / GTS) |
| `qtype` | Fine-grained question type (e.g., single emergence, interval summary) |
| `images` | Temporally ordered CXR images (T1–T5) representing the patient's longitudinal studies |
| `question` | Natural language question requiring reasoning over the image sequence |
| `choices` | Five-way multiple-choice answer options (A–E) |
| `answer` | The correct answer choice |

**\*\* The `images` field contains relative paths (e.g., `files/p14/.../xxxxx.jpg`); simply set the root to your local MIMIC-CXR-JPG download directory to resolve them.**

---

## Images (MIMIC-CXR-JPG)

MI-CXR uses chest X-ray images from the **MIMIC-CXR-JPG** dataset. To obtain the images:

1. Request access and download from [https://physionet.org/content/mimic-cxr-jpg/2.1.0/](https://physionet.org/content/mimic-cxr-jpg/2.1.0/)
2. After downloading, either:
   - Create a symbolic link from this repository's `files/` directory to the `files/` directory in MIMIC-CXR-JPG, or
   - Modify the image paths in the dataset configuration to match your local setup.

---

## Results

Performance of 14 state-of-the-art VLMs on MI-CXR under zero-shot prompting. Random guessing = 20%.

| Category | Model | TEL (Single) | TEL (Multi) | TEL (E→R) | ICR | GTS (Single) | GTS (Multi) | Overall |
|---|---|---|---|---|---|---|---|---|
| **Closed** | Claude Sonnet 4.5 | 0.226 | 0.222 | 0.243 | 0.442 | 0.292 | 0.389 | 0.315 |
| | Gemini 3.0 Pro | 0.246 | 0.325 | 0.290 | 0.457 | 0.407 | 0.556 | 0.387 |
| | GPT-5.2 | 0.334 | 0.371 | 0.358 | 0.438 | 0.390 | 0.558 | **0.411** |
| **General** | InternVL3.5-8B | 0.239 | 0.295 | 0.193 | 0.552 | 0.371 | 0.389 | 0.358 |
| | InternVL3.5-38B | 0.298 | 0.306 | 0.224 | 0.571 | 0.515 | 0.510 | **0.418** |
| | QwenVL3-32B | 0.258 | 0.246 | 0.240 | 0.224 | 0.325 | 0.363 | 0.272 |
| | DeepSeek-VL-16B | 0.223 | 0.124 | 0.200 | 0.186 | 0.187 | 0.160 | 0.181 |
| | IDEFICS2-8B | 0.165 | 0.308 | 0.291 | 0.246 | 0.178 | 0.281 | 0.245 |
| **Medical** | Lingshu-7B | 0.230 | 0.260 | 0.165 | 0.189 | 0.194 | 0.324 | 0.223 |
| | Lingshu-32B | 0.221 | 0.247 | 0.214 | 0.167 | 0.290 | 0.388 | 0.247 |
| | MedGemma-4B | 0.174 | 0.196 | 0.301 | 0.281 | 0.183 | 0.259 | 0.237 |
| | MedGemma-27B | 0.215 | 0.351 | 0.254 | 0.429 | 0.214 | 0.255 | 0.299 |

---

## Citation

```bibtex
@misc{cho2026micxrbenchmarklongitudinalreasoning,
      title={MI-CXR: A Benchmark for Longitudinal Reasoning over Multi-Interval Chest X-rays}, 
      author={Sunghwan Steve Cho and Yunseok Han and Jaeyoung Do},
      year={2026},
      eprint={2605.15574},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2605.15574}, 
}
```
