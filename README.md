# Sustainable-Fashion-Discourse

## 📌 Overview

This repository contains the annotated datasets, classification prompts, model training notebooks, BERTopic outputs, and reproducibility materials for the paper:

> **"Beyond Greenwashing: Mapping Consumer Discourse Priorities and Topic-Emotion-Strategy Communication Gaps in Sustainable Fashion Marketing"**

---

## 📂 Repository Structure

```
sustainable-fashion-discourse/
│
├── data/
│   ├── stage1_sustainability_dimensions_annotated.xlsx     ← BERT Stage 1 labeled data
│   └── stage2_emotional_traits_annotated.xlsx             ← BERT Stage 2 labeled data
│
├── prompts/
│   ├── prompt_stage1_sustainability_dimensions.txt        ← Claude API annotation prompt (Stage 1)
│   └── prompt_stage2_emotional_traits.txt                 ← Claude API annotation prompt (Stage 2)
│
│   ├── bert_stage1_sustainability.ipynb               ← BERT fine-tuning: sustainability dimensions
│   ├── bert_stage2_emotions.ipynb                     ← BERT fine-tuning: emotional traits
│   ├── bertopic_environment.ipynb                     ← BERTopic: environment corpus (n=5,410)
│   ├── bertopic_economic.ipynb                        ← BERTopic: economic corpus (n=6,101)
│   └── bertopic_social.ipynb                          ← BERTopic: social corpus
(n=4,658)
│
├── requirements.txt
├── LICENSE
├── CITATION.cff
└── README.md
```

---

## 📘 Project Overview

### The Problem

Sustainable fashion brands increasingly adopt sustainability messaging, yet consumer trust continues to erode. Existing research has diagnosed this at the *dimensional* level (e.g., "brands over-emphasize environmental concerns").

### The Approach: Three-Layer Analytical Framework

| Layer | Method | Research Question |
|-------|--------|-------------------|
| **Layer 1** | BERT-based multi-label classification | What sustainability dimensions and emotions dominate consumer discourse? |
| **Layer 2** | BERTopic within-dimension topic modeling | Which specific topics are consumers most concerned about? |

---

## 📁 Dataset

Annotated datasets are available in the `/data` folder:

| File | Stage | Description |
|------|-------|-------------|
| `stage1_sustainability_dimensions_annotated.xlsx` | Stage 1 | 20,162 samples annotated for 5 sustainability dimensions (multi-label binary per dimension) |
| `stage2_emotional_traits_annotated.xlsx` | Stage 2 | 20,162 samples annotated for 5 emotional traits (multi-class) |

**Note on raw data:** Raw corpora from X and YouTube are not redistributed due to platform terms of service. The annotated label columns are included alongside preprocessed text.

---

## 🔁 Reproducibility

- Data splits use stratified random sampling (80/20)
- Fixed random seeds: `set_seed(42)` for BERT notebooks; `random_state=42` for UMAP/HDBSCAN in BERTopic
- BERTopic involves a stochastic UMAP step; minor variation across hardware is expected and does not affect substantive findings
- A CUDA-enabled GPU is recommended for Notebooks 02–06

To install dependencies and run locally:

```bash
git clone https://github.com/[your-username]/sustainable-fashion-discourse.git
cd sustainable-fashion-discourse
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 🔗 Links

- 📄 **Paper:** *Submitted — link will be added upon acceptance*
- 📁 **GitHub Repository:** [this repository]
- 🤗 **Fine-tuned Models:** *Will be uploaded to Hugging Face Hub upon acceptance*

---

## ⚖️ License

- **Code** (notebooks and scripts): [MIT License](LICENSE)
- **Annotated data** (`data/`): [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

---

## 📬 Contact

For questions about the code, data, or methodology, please open a [GitHub Issue](../../issues) or contact the corresponding author indicated in the manuscript
---

## 🙏 Acknowledgements

We acknowledge the developers of [BERTopic](https://github.com/MaartenGr/BERTopic), [Hugging Face Transformers](https://github.com/huggingface/transformers), and [Anthropic Claude](https://www.anthropic.com) whose tools made this research possible.
