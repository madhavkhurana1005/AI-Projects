# 📊 Domain-Adaptive Pretraining with DistilBERT (MLM + Classification)

## 🚀 Overview

This project investigates whether **domain-adaptive pretraining using Masked Language Modeling (MLM)** improves downstream performance on a sentiment classification task.

We fine-tune **DistilBERT** on the IMDB dataset in two stages:

1. **MLM fine-tuning (unsupervised)** on IMDB text
2. **Sentiment classification fine-tuning (supervised)**

We then compare results against a **baseline DistilBERT model** trained directly on classification.

---

## 🎯 Objective

> Does domain-adaptive MLM fine-tuning improve sentiment classification performance?

---

## 🧠 Approach

### 🔹 Step 1: MLM Fine-tuning

* Model: `distilbert-base-uncased`
* Objective: Predict masked tokens
* Technique:

  * Concatenate text samples
  * Chunk into fixed-length sequences (256 tokens)
  * Apply dynamic masking (15%)

---

### 🔹 Step 2: Classification Fine-tuning

* Task: Binary sentiment classification (positive / negative)
* Dataset: IMDB (50k reviews)
* Models:

  * **Baseline**: DistilBERT (no MLM)
  * **Proposed**: MLM-adapted DistilBERT

---

### 🔹 Step 3: Evaluation

Metrics:

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

* MLM fine-tuning showed **no significant improvement**
* Both models performed nearly identically
* Indicates strong baseline performance

---

## 🧠 Core Insight

> **Transfer learning gains depend more on domain difference than additional pretraining.**

---

## 💡 Interpretation

### ✅ Why No Improvement?

* **Low domain gap**: IMDB reviews are similar to pretraining corpus
* **Strong baseline**: DistilBERT already captures sentiment effectively
* **Diminishing returns**: Additional MLM training adds limited value

---

## 🧪 Error Analysis

The model exhibits consistent failure patterns across both baseline and MLM-adapted versions:

* **Sarcasm / Contradictory Tone**:
  The model struggles when positive words are used in a negative context (e.g., *“Great movie… I wasted 2 hours”*), indicating reliance on surface-level cues.

* **Negation Handling**:
  Phrases like *“not bad at all”* are often misclassified, showing limitations in understanding logical negation.

* **Mixed Sentiment**:
  Reviews containing both positive and negative opinions are difficult to classify due to binary labeling constraints.

* **Long Reviews (Truncation Issue)**:
  Important sentiment information appearing later in long reviews may be truncated due to fixed input length (256 tokens), leading to incorrect predictions.

These patterns were observed across both models, suggesting that MLM fine-tuning did not significantly improve handling of nuanced linguistic structures.

---

## ⚠️ Limitations

* Binary classification oversimplifies sentiment
* Input length constraints (truncation) affect long reviews
* Limited benefit from MLM due to domain similarity

---

## 🚀 Future Work

* Use domain-specific datasets (finance, legal, medical)
* Increase MLM training scale (more data, more epochs)
* Experiment with larger models (BERT, RoBERTa)
* Explore long-context models (Longformer, etc.)

---

## 🛠️ Tech Stack

* Hugging Face Transformers
* PyTorch
* Datasets library
* Scikit-learn

---

## 🧭 Conclusion

This project demonstrates that:

* Domain-adaptive pretraining is **not universally beneficial**
* Effectiveness depends on **domain similarity**
* Strong pretrained models already generalize well on common datasets

---

## 📌 Key Takeaway

> Not every improvement comes from more training — sometimes the real insight is understanding *why it doesn’t*.

---
