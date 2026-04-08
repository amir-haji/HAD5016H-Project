# 🏥 CultureCareBench: A Dataset of Clinically Cultural Context

This repository contains the code, data, and resources for **CultureCareBench**, a benchmark designed to evaluate how medical Large Language Models (LLMs) incorporate **cultural context** into clinical reasoning.

---

## 📌 Overview

Medical LLMs are increasingly used in healthcare decision-making, but they often struggle with **culturally grounded reasoning**. While prior work focuses on demographic bias (e.g., race, gender), this project addresses a critical gap:

> ❓ *Can LLMs correctly incorporate culturally relevant information into medical reasoning?*

To answer this, we introduce **CultureCareBench**, a dataset of **multiple-choice medical questions** where cultural context can **change the correct answer**.

---

## 🧠 Key Contributions

* 📚 A curated dataset of **60 culturally grounded medical MCQs**
* 🌏 Focus on **three cultural groups**:

  * Japanese
  * Chinese
  * Arabic
* ⚖️ Paired evaluation:

  * **Base question** (no cultural context)
  * **Cultural question** (includes cultural signal)
* 🔍 Evaluation of LLM reasoning under cultural variation
* ⚙️ End-to-end pipeline:

  * Cultural signal extraction
  * Case retrieval (PubMed)
  * LLM-based question generation

---

## 🗂️ Project Structure

```
.
├── Code
│   ├── model_inference.ipynb     # Model evaluation and inference
│   ├── NLP_pipeline.ipynb        # Cultural snippet generation & processing
│   └── retrieval.ipynb           # FAISS-based case retrieval
├── Data
│   ├── cultural_constraints.json # Extracted cultural snippets
│   ├── generated_dataset.json    # Final MCQ dataset
│   ├── Llama-3.1-8B-Instruct_no_results.jsonl
│   ├── Llama-3.1-8B-Instruct_yes_results.jsonl
│   ├── Qwen2.5-7B-Instruct_no_results.jsonl
│   ├── Qwen2.5-7B-Instruct_yes_results.jsonl
│   └── references.csv            # Source references (PubMed cases)
├── Fig
│   ├── ML_figure.key             # Pipeline figure (Keynote)
│   └── ml_health_wordcloud.png   # NLP word cloud visualization
└── README.md
```

---

## ⚙️ Methodology

The pipeline consists of three main stages:

### 1️⃣ Cultural Signal Construction

* AI agents extract culturally relevant medical factors:

  * Diet
  * Communication
  * Family decision-making
  * Beliefs/preferences
* ~65 snippets per group, manually validated

### 2️⃣ Medical Case Retrieval

* Source: ~167K **PubMed case reports**
* Embedding: MiniLM
* Retrieval: **FAISS vector search**
* Top-K (K=30) relevant cases per cultural snippet

### 3️⃣ Dataset Generation

* LLM (GPT-based) generates:

  * **Base MCQ** (no culture)
  * **Cultural MCQ** (with cultural signal)
* Same answer choices, but **correct answer may differ**

---

## 📊 Results

### Overall Performance

| Model                 | Cultural Accuracy | Base Accuracy |
| --------------------- | ----------------- | ------------- |
| Llama-3.1-8B-Instruct | 84%               | 95%           |
| Qwen2.5-7B-Instruct   | 88%               | 94%           |

👉 Key insight:

> Models perform worse when cultural context is introduced, despite being capable of reasoning. 

---

### Performance by Cultural Group

| Model                 | Japanese | Chinese | Arabic |
| --------------------- | -------- | ------- | ------ |
| Llama-3.1-8B-Instruct | 80%      | 88%     | 94%    |
| Qwen2.5-7B-Instruct   | 77%      | 82%     | 91%    |

👉 Observations:

* Arabic group performs best
* Japanese group shows lowest accuracy (possibly due to:

  * limited English-language cultural data
  * complex socio-cultural reasoning)

---

## 🔬 Key Insights

* ✅ LLMs can incorporate cultural reasoning
* ⚠️ Performance **drops with cultural complexity**
* 📉 Cultural signals can **confuse or mislead reasoning**
* 🌐 Language and data availability strongly affect outcomes

---

## 🚧 Limitations

* Small dataset size (60 questions)
* Cultural snippets generated via AI (require expert validation)
* Limited number of cultural groups
* Evaluation based on MCQs (not full clinical workflows)

---

## 🚀 Future Work

* Scale dataset generation (semi-automated pipeline)
* Add more cultural groups and regions
* Expert validation of clinical correctness
* Extend beyond MCQ → real-world clinical reasoning tasks

---

## 📖 References

See `Data/references.csv` and full citations in the project report.

---

## 🤝 Acknowledgments

Developed as part of:

**Applied Machine Learning for Health Data (HAD5016H)**
University of Toronto – Winter 2026
