# Sustainable-Fashion-Discourse: A Topic-Emotion-Strategy Framework for Sustainable Fashion Communication

This repository contains the annotated datasets, model training notebooks, and reproducibility materials for the paper titled:

> **"Beyond Greenwashing: Topic-Emotion Gaps in Consumer Discourse on Sustainable Fashion Marketing"**

---

## 📂 Repository Structure
sustainable-fashion-discourse/
```
│
├── dataset/
│   ├── stage1_sustainability_dimension.xlsx
│   └── stage2_emotional_traits.xlsx
│
├── codes/
│   ├── BERT/
│   │   ├── Stage 1 - Sustainability Dimension Classification/
│   │   └── Stage 2 - Emotional Trait Classification/
│   └── BERTopic/
│       ├── Environment Topic Modeling/
│       ├── Economic Topic Modeling/
│       └── Social Topic Modeling/
│
├── prompt/
│   ├── prompt_stage1_sustainability_dimension/
│   ├── prompt_stage2_emotional_trait/
│
├── requirements.txt
├── LICENSE
└── CITATION.cff
```
---

## 📘 Project Overview

This project introduces a multi-layer computational framework to analyze how sustainable fashion is:

* **Discussed** (Stage 1: Sustainability Dimension Classification — mapping discourse to economic, social, environmental, cultural, and aesthetic dimensions)
* **Felt** (Stage 2: Emotional Trait Classification — identifying anger, skepticism, concern, hope, and frustration in consumer discourse)
* **Structured** (Topic Modeling: unsupervised BERTopic analysis within the three analytically dominant dimensions)

The analysis culminates in the **Topic-Emotion-Strategy (TES) framework**, which links consumer-prioritized topics with dominant emotional responses to diagnose communication gaps between brand sustainability messaging and consumer concerns.

Two complementary modeling approaches were applied:

* **Supervised BERT fine-tuning** (`bert-base-uncased`) for Stage 1 (multi-label sustainability dimensions) and Stage 2 (multi-label emotional traits) classification
* **Unsupervised BERTopic** for latent topic discovery within the environment, economic, and social dimensions

---

## 📁 Dataset

Labeled datasets are available in the `/dataset` folder, with one file per classification stage:

| File | Stage | Description |
| --- | --- | --- |
| `stage1_sustainability_dimension.xlsx` | Stage 1 | Consumer discourse documents annotated for five sustainability dimensions (multi-label, binary per dimension) |
| `stage2_emotional_traits.xlsx` | Stage 2 | Consumer discourse documents annotated for five emotional traits (multi-class) |

Each file contains preprocessed text data drawn from X (formerly Twitter) and YouTube. The **raw corpora** are not redistributed due to platform terms of service; please contact the corresponding author for access requests.

---

## 🧠 Model Training Notebooks

The `/codes` folder contains all notebooks for fine-tuning BERT and running the BERTopic pipeline:

* Use notebooks in `codes/BERT/Stage 1` or `codes/BERT/Stage 2` for supervised classification training and evaluation
* Use notebooks in `codes/BERTopic` for the unsupervised topic modeling pipeline, run separately per dimension
* Fine-tuning configurations (batch size, learning rate, epochs) follow the best-performing setups reported in the paper

| # | Notebook | Stage | Input | Main Outputs |
| --- | --- | --- | --- | --- |
| 01 | `Stage 1 - Sustainability Dimension` | Stage 1 — Multi-label BERT | `stage1_sustainability_dimension.xlsx` | Fine-tuned classifier, classification report, predictions |
| 02 | `Stage 2 - Emotional Trait` | Stage 2 — Multi-label BERT | `stage2_emotional_traits.xlsx` | Fine-tuned classifier, classification report, predictions |
| 03 | `BERTopic Environment` | Topic Modeling | Pre-cleaned environment corpus | Topic info, distributions, keyword scores, HTML visualizations |
| 04 | `BERTopic Economic` | Topic Modeling | Pre-cleaned economic corpus | Topic info, distributions, keyword scores, HTML visualizations |
| 05 | `BERTopic Social` | Topic Modeling | Pre-cleaned social corpus | Topic info, distributions, keyword scores, HTML visualizations |

---

## 🔁 Reproducibility

* Data splits were stratified with a fixed random seed for the BERT notebooks
* BERT classifiers were fine-tuned using the Hugging Face Transformers library with `bert-base-uncased`
* BERTopic uses sentence-transformer embeddings with UMAP dimensionality reduction and HDBSCAN clustering (`min_cluster_size = 25`, `min_samples = 10`)
* BERTopic involves a stochastic UMAP step; minor variation across hardware is expected and does not affect the substantive findings
* A CUDA-enabled GPU is recommended for the BERT training notebooks

To install dependencies and run locally:

​```
git clone https://github.com/syarafinadzh/Sustainable-Fashion-Discourse.git
cd Sustainable-Fashion-Discourse
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
​```

---

## 🤖 Pre-trained Models

Fine-tuned BERT classifiers will be uploaded to the Hugging Face Hub upon manuscript acceptance. Links will be added here after publication.

---

## ⚖️ License

* **Code** (notebooks and scripts): MIT License
* **Annotated data** (`dataset/`): Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## 📬 Contact

For questions about the code, data, or methodology, please open a [GitHub Issue](../../issues) or contact the corresponding author indicated in the manuscript

---

## 🙏 Acknowledgements

We acknowledge the developers of [BERTopic](https://github.com/MaartenGr/BERTopic) and [Hugging Face Transformers](https://github.com/huggingface/transformers), on which this analysis depends.
