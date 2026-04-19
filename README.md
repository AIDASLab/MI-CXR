# MI-CXR: A Benchmark for Longitudinal Reasoning over Multi-Interval Chest X-rays

## Overview

Longitudinal chest X-ray (CXR) interpretation requires reasoning over disease evolution across multiple patient visits, yet most existing medical VQA benchmarks focus on single images or short-horizon image pairs.

We introduce **MI-CXR**, a benchmark for standardized evaluation of **M**ulti-**I**nterval longitudinal reasoning over multi-visit **CXR** sequences, without requiring free-form report generation or additional clinical context.  
MI-CXR comprises five-way multiple-choice questions constructed over five-visit patient timelines and instantiates three complementary task families:

- **Temporal Event Localization (TEL)**  
- **Interval-wise Change Reasoning (ICR)**  
- **Global Trajectory Summarization (GTS)**  

These tasks are designed to assess clinically grounded visual reasoning over time.

Evaluations on 14 state-of-the-art vision–language models (VLMs) reveal low overall performance (29.3% accuracy), only modestly above random guessing.  
Using a stage-wise diagnostic probing framework, we find that models often produce locally plausible interval-level descriptions but fail to enforce temporal constraints or compose evidence into globally consistent decisions across the full timeline.

Together, these results highlight key limitations of current VLMs and position MI-CXR as a principled benchmark for longitudinal medical reasoning.

---

## Notice
- Our paper has been accepted to ACL 2026 Findings.
- We will be updating our arxiv and huggingface link shortly, once everything is finalized.

---

## Usage
* **File description**
  * `micxr_test.jsonl`: The MI-CXR test cases, containing ~5k examples.
 
* **Data Description**
  Each entry in the `micxr_test.jsonl` files contains the following fields:

  - `qid`: Unique identifier for each question instance.
  - `group_type`: High-level task category that defines the overall reasoning objective. Each group represents a distinct type of temporal reasoning task (e.g., event localization, interval reasoning, trajectory summarization).
  - `qtype`: Fine-grained question type within each group_type. Specifies the exact reasoning pattern required (e.g., emergence, resolution, interval summary).
  - `images`: A sequence of temporally ordered medical images (e.g., T1–T5) representing the patient’s longitudinal studies. Each key corresponds to a specific time point in the sequence.
  - `question`: The natural language question that requires reasoning over the temporal sequence of images.
  - `choices`: Multiple-choice answer options. Each option describes a possible interpretation of temporal changes or events across the image sequence.
  - `answer`: The correct answer choice corresponding to the question.

---

## Images (MIMIC-CXR-JPG)

MI-CXR uses chest X-ray images from the **MIMIC-CXR-JPG** dataset.

To obtain the images, please request access and download the dataset from:  
https://physionet.org/content/mimic-cxr-jpg/2.1.0/

After downloading, you may either:
- create a symbolic link from this repository’s `files/` directory to the corresponding `files/` directory in MIMIC-CXR-JPG, or  
- modify the image paths in the dataset configuration to match your local setup.

---

## Report-Derived Information and Access Restrictions

MI-CXR is constructed on top of **MIMIC-CXR-JPG** and **MIMIC-Ext-CXR-QBA**, both of which are distributed under PhysioNet’s credentialed access framework.

As a result, radiology report content and derived textual annotations are subject to access restrictions and cannot be redistributed independently through this repository.  
Users are expected to obtain appropriate PhysioNet credentials and comply with the original data usage agreements when working with MI-CXR.
