# Sustainable-Fashion-Discourse
### Beyond Greenwashing: A Topic-Emotion-Strategy Framework for Sustainable Fashion Marketing Communication<img width="468" height="51" alt="image" src="https://github.com/user-attachments/assets/4114b916-110d-4689-95c7-a162caee6b02" />


> **Syarafina Putri Adzhani Jogaswara · Andry Alamsyah · Dian Puteri Ramadhani**  
> School of Economics and Business, Telkom University, Bandung, Indonesia  
> *Submitted to Journal of Global Fashion Marketing (Taylor & Francis)*

---

## 📂 Repository Structure

```
Sustainable-Fashion-Discourse/
│
├── Dataset/
│   ├── stage1_sustainability_dimension.xlsx       ← Annotated: 5 sustainability dimensions
│   └── stage2_emotional_traits.xlsx               ← Annotated: 5 emotional traits
│
├── Codes/
│   ├── BERT/
│   │   ├── Stage 1 - Sustainability Dimension Classification/
│   │   └── Stage 2 - Emotional Trait Classification/
│   └── BERTopic/
│       ├── Environment Topic Modeling/
│       ├── Economic Topic Modeling/
│       └── Social Topic Modeling/
│
├── Prompt/
│   ├── prompt_stage1_sustainability_dimension.txt
│   └── prompt_stage2_emotional_trait.txt
│
├── requirements.txt
├── LICENSE                                        ← MIT License
├── CITATION.cff                                   ← Citation metadata
└── README.md
```

---

## 📘 Project Overview

This study addresses the **trust crisis in sustainable fashion marketing** by examining what consumers discuss, how they emotionally engage, and where brand communication fails to align — at the **topic level**, not only the dimensional level.

Using BERT-based classification and BERTopic modeling on **20,162 consumer discourse samples** from X (Twitter) and YouTube, the study:

1. Maps sustainability dimensions grounded in the **Triple Bottom Line (TBL)** framework
2. Profiles emotional responses grounded in **Cognitive Appraisal Theory (CAT)**
3. Identifies topic-level communication gaps through **Signaling Theory**
4. Synthesizes findings into the **Topic-Emotion-Strategy (TES) Framework**

Two complementary modeling approaches were applied:

- **Supervised BERT fine-tuning** (`bert-base-uncased`) for Stage 1 (multi-label sustainability dimensions) and Stage 2 (multi-label emotional traits) classification
- **Unsupervised BERTopic** for latent topic discovery within the three analytically dominant dimensions (Environment, Economic, Social)

---

## 📁 Dataset

Annotated datasets are in the `/Dataset` folder:

| File | Stage | N | Description |
|------|-------|---|-------------|
| `stage1_sustainability_dimension.xlsx` | Stage 1 | 20,162 | Consumer discourse annotated for 5 sustainability dimensions (multi-label, binary per dimension) |
| `stage2_emotional_traits.xlsx` | Stage 2 | 20,162 | Consumer discourse annotated for 5 emotional traits (multi-label, binary per trait) |

Raw corpora from X and YouTube are not redistributed due to platform terms of service. Contact the corresponding author for access.

### Stage 1 — Sustainability Dimensions (TBL-grounded)

| Label | Definition |
|-------|------------|
| `environment` | Environmental harm reduction: waste, pollution, renewable energy, sustainable materials |
| `economic` | Sustainable business models, supply chain economics, pricing, financial accountability |
| `social` | Labor rights, supply chain equity, forced labor, ethical production practices |
| `cultural` | Heritage preservation, cultural appropriation in fashion |
| `aesthetic` | Design longevity, emotionally durable design, slow fashion behaviors |

### Stage 2 — Emotional Traits (CAT-grounded)

| Label | Definition |
|-------|------------|
| `anger` | Moral outrage directed at identifiable agents (other-blame appraisal) |
| `skepticism` | Credibility uncertainty; greenwashing perception |
| `concern` | Apprehension about systemic harm from industry practices |
| `hopeful` | Positive future appraisal through innovation or collective action |
| `frustration` | Goal obstruction from perceived barriers (price, access, information gaps) |

---

## 🤖 Annotation Pipeline

Initial annotation was performed using the **Claude AI API (Anthropic)** with structured prompts grounded in the operational definitions above. See `/Prompt/` for the exact prompts used.

A stratified random sample was independently annotated by two researchers to validate automated labels:

| Stage | Sample Size | Cohen's Kappa | Interpretation |
|-------|-------------|---------------|----------------|
| Stage 1 | 178 samples | **κ = 0.8966** | Almost Perfect |
| Stage 2 | 700 samples | **κ = 0.6982** | Substantial |

Per-label Kappa values are reported in the paper's supplementary materials.

---

## 🧠 Model Training

### BERT Classification (Codes/BERT/)

`bert-base-uncased` fine-tuned with sigmoid activation for multi-label assignment.

| Stage | Task | Macro F1 | Precision | Recall |
|-------|------|----------|-----------|--------|
| Stage 1 | Sustainability Dimensions | 0.81 | 0.86 | 0.78 |
| Stage 2 | Emotional Traits | 0.77 | 0.81 | 0.74 |

Best hyperparameters: `batch_size = 16`, `learning_rate = 2e-5`, `epochs = 2`

### BERTopic Topic Modeling (Codes/BERTopic/)

Applied separately to three dimension-specific corpora:

| Dimension | Corpus Size | Valid Clusters | Key Parameters |
|-----------|-------------|----------------|----------------|
| Environment | 5,410 docs | 27 topics | min_cluster_size=25 |
| Economic | 6,101 docs | 33 topics | min_cluster_size=25 |
| Social | 4,658 docs | 35 topics | min_cluster_size=25 |

Embedding model: `all-mpnet-base-v2` · UMAP: `n_neighbors=15, n_components=5` · HDBSCAN: `min_samples=10`

---

## 🔑 Key Findings

| Finding | Detail |
|---------|--------|
| 📊 Economic ≥ Environmental | Economic (36.5%) slightly exceeds environmental (31.4%) — challenging common assumptions |
| 😠 Social → Anger dominant | Social topics activate anger at 58.0%, nearly 2× other dimensions |
| 🌱 Environmental → Hope | Hope dominates environmental discourse (31.4%), linked to consumer agency |
| 💸 Pricing ≠ primary barrier | Pricing/affordability = only 4.8% of economic discourse |
| 🏭 Structural critique ignored | Forced labor + accountability (25.2%) virtually absent from brand messaging |
| ♻️ Eco-innovation mismatch | Eco-innovation = 6.5% of consumer discourse vs. dominant in brand messaging |

### The TES Framework

| Dimension | Consumer Priority | Dominant Emotion | Brand Gap | Recommended Strategy |
|-----------|------------------|-----------------|-----------|----------------------|
| Environmental | Pollution & toxics reduction | Hope (31.4%) | Eco-innovation over-messaging | **Amplification** — support actionable consumer behavior |
| Economic | Supply chain transparency | Skepticism (24.0%) | Pricing assumed as #1 barrier | **Credibility-building** — disclose cost structures |
| Social | Structural accountability | Anger (58.0%) | Systemic critique unaddressed | **Accountability-signaling** — name labor issues directly |

---

## 🔁 Reproducibility

- Stratified 80/20 train-test splits with fixed random seed (`seed=42`)
- BERT fine-tuning via Hugging Face Transformers (`bert-base-uncased`)
- BERTopic stochastic UMAP step: minor variation across hardware is expected and does not affect substantive findings
- CUDA-enabled GPU recommended for BERT notebooks

```bash
git clone https://github.com/syarafinadzh/Sustainable-Fashion-Discourse.git
cd Sustainable-Fashion-Discourse
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 🤗 Pre-trained Models

Fine-tuned BERT classifiers will be uploaded to Hugging Face Hub upon manuscript acceptance. Links will be updated here after publication.

---

## ⚖️ License

- **Code** (notebooks and scripts): [MIT License](LICENSE)
- **Annotated data** (`Dataset/`): [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

---

## 📄 Citation

```bibtex
@article{jogaswara2025beyondgreenwashing,
  title     = {Beyond Greenwashing: Mapping Consumer Discourse Priorities and
               Topic-Emotion-Strategy Communication Gaps in Sustainable Fashion Marketing},
  author    = {Jogaswara, Syarafina Putri Adzhani and
               Alamsyah, Andry and
               Ramadhani, Dian Puteri},
  journal   = {Journal of Global Fashion Marketing},
  year      = {2025},
  publisher = {Taylor \& Francis},
  note      = {Under review}
}
```

---

## 📬 Contact

Open a [GitHub Issue](../../issues) or contact the corresponding author:  
📧 `andrya@telkomuniversity.ac.id`

---

## 🙏 Acknowledgements

We acknowledge the developers of [BERTopic](https://github.com/MaartenGr/BERTopic), [Hugging Face Transformers](https://github.com/huggingface/transformers), and [Anthropic Claude](https://www.anthropic.com) on which this analysis depends.
