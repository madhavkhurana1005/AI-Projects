# 📊 Domain-Adaptive Pretraining with DistilBERT (MLM + Classification)

## 🚀 Overview

This project explores whether **domain-adaptive pretraining using Masked Language Modeling (MLM)** improves downstream performance on a sentiment classification task.

We fine-tune **DistilBERT** on the IMDB dataset in two stages:

1. **MLM fine-tuning (unsupervised)** on IMDB text
2. **Sentiment classification fine-tuning (supervised)**

We then compare performance against a **baseline DistilBERT model** trained directly on classification.

---

## 🎯 Objective

> Does domain-adaptive MLM fine-tuning improve sentiment classification performance?

---

## 🧠 Approach

### 🔹 Step 1: MLM Fine-tuning

* Model: `distilbert-base-uncased`
* Objective: Predict masked tokens
* Technique:

  * Concatenate text
  * Chunk into fixed-length sequences (256 tokens)
  * Apply dynamic masking (15%)

---

### 🔹 Step 2: Classification Fine-tuning

* Task: Binary sentiment classification (positive / negative)
* Dataset: IMDB (50k reviews)
* Model:

  * Baseline: DistilBERT (no MLM)
  * Proposed: MLM-adapted DistilBERT

---

### 🔹 Step 3: Evaluation

Metrics used:

* Accuracy
* F1 Score

---

## 📊 Results

| Model                       | Accuracy | F1 Score |
| --------------------------- | -------- | -------- |
| Baseline DistilBERT         | 91.27%   | 0.9128   |
| MLM + DistilBERT (2 epochs) | 91.27%   | 0.9132   |

---

## 🔍 Key Findings

* MLM fine-tuning **did not significantly improve performance**
* Both models performed nearly identically
* Slight variation in F1 is negligible

---

## 🧠 Core Insight

> **This experiment highlights that transfer learning gains are highly dependent on domain divergence rather than just additional pretraining.**

---

## 💡 Interpretation

### ✅ Why No Improvement?

* **Low domain gap**: IMDB reviews are similar to pretraining corpus
* **Strong baseline**: DistilBERT already captures sentiment well
* **Diminishing returns**: Additional MLM training adds limited value

---

## 🔥 What This Demonstrates

* Understanding of **self-supervised learning (MLM)**
* Application of **transfer learning**
* Ability to design **controlled experiments**
* Capability to interpret **non-improving results correctly**

---

## ⚠️ Limitations

* Limited domain diversity (movie reviews only)
* MLM training scale relatively small compared to original pretraining
* Binary classification (does not capture nuanced sentiment)

---

## 🚀 Future Work

* Apply MLM pretraining on **domain-specific datasets** (finance, legal, medical)
* Increase training scale (more data, more epochs)
* Explore larger models (BERT, RoBERTa)

---

## 🧪 Error Analysis (Summary)

Observed failure patterns:

* Sarcasm and contradictory phrases
* Mixed sentiment in long reviews
* Negation handling (“not bad”, “not great”)

---

## 🧭 Conclusion

This project demonstrates that:

* Domain-adaptive pretraining is **not universally beneficial**
* Effectiveness depends on **domain similarity and data distribution**
* Strong baselines can already capture general language patterns effectively

---

## 🛠️ Tech Stack

* Hugging Face Transformers
* PyTorch
* Datasets library
* Scikit-learn

---

## 📌 Key Takeaway

> Not every improvement comes from more training — sometimes the real insight is understanding *why it doesn’t*.

---
