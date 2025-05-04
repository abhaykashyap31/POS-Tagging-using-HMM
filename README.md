

# 🧠 Part-of-Speech Tagging Using Hidden Markov Models (HMM)

This project implements Part-of-Speech (PoS) tagging using various configurations of Hidden Markov Models (HMMs) from scratch — no external NLP libraries involved. It explores the effects of model order and tag granularity on performance using the Viterbi algorithm.

---

## 📘 Overview

Part-of-Speech tagging assigns grammatical categories (like noun, verb, adjective) to words in a sentence. It's a core task in NLP pipelines.
This project compares different HMM variants:

* First-order HMM
* Second-order HMM
* First-order HMM with previous word context
  Using two tag granularities:
* Full Penn Treebank (36 tags)
* Collapsed categories (4 tags)

---

## 📊 Dataset Summary

| 📌 Metric               | 📈 Value    |
| ----------------------- | ----------- |
| Total Sentences         | 3,914       |
| Average Sentence Length | 20.73 words |
| Max Sentence Length     | 171 words   |
| Min Sentence Length     | 1 word      |
| Vocabulary Size         | 16,458      |
| Total Words             | 81,147      |
| Unique PoS Tags         | 41          |
| Train-Test Split        | 80:20       |

---

## ⚙️ Model Variants & Results

### 🔹 First-Order HMM

> Assumes word depends only on current tag

| Tag Set    | Accuracy | Precision | Recall | F1-Score |
| ---------- | -------- | --------- | ------ | -------- |
| 🏷️ 36-Tag | 82.22%   | 78.83%    | 77.86% | 77.78%   |
| 🔢 4-Tag   | 78.33%   | 84.28%    | 78.19% | 80.53%   |

---

### 🔹 Second-Order HMM

> Assumes word depends on current and previous tags

| Tag Set    | Accuracy | Precision | Recall | F1-Score |
| ---------- | -------- | --------- | ------ | -------- |
| 🏷️ 36-Tag | 81.45%   | 78.46%    | 69.75% | 72.49%   |
| 🔢 4-Tag   | 79.14%   | 84.52%    | 78.73% | 81.01%   |

---

### 🔹 First-Order HMM + Previous Word

> Assumes word depends on current tag and previous word

| Tag Set    | Accuracy | Precision | Recall | F1-Score |
| ---------- | -------- | --------- | ------ | -------- |
| 🏷️ 36-Tag | 50.26%   | 64.74%    | 33.69% | 40.76%   |
| 🔢 4-Tag   | 53.98%   | 70.52%    | 47.16% | 51.60%   |

---

## 🧩 Tag Granularity

### 🏷️ 36-Tag Model

* Full Penn Treebank tagset
* High specificity but more sparsity
* Challenges: Rare tags (e.g., `FW`, `SYM`) poorly predicted
* Strengths: High accuracy on punctuation and function words

### 🔢 4-Tag Collapsed Model

| Category | Included Tags                 | Accuracy (Range) |
| -------- | ----------------------------- | ---------------- |
| N        | All nouns                     | 86.11–86.55%     |
| V        | All verbs                     | 80.14–80.22%     |
| A        | Adjectives and adverbs        | 75.10–75.15%     |
| O        | All other tags (e.g., TO, CC) | 71.34–73.08%     |

* Fewer transitions (16 vs. 1,296)
* Reduces misclassifications
* Better generalization

---

## 🔍 Analysis & Observations

### ✅ High Accuracy Tags

* `DT`, `CC`, `TO`: >97%
* `NNP` (Proper Noun): \~89%
* Punctuation tags: perfect accuracy

### ⚠️ Challenging Cases

* `RBR` (Comparative Adverbs): 20–52%
* Rare tags (`FW`, `LS`, `SYM`): 0%
* Verbs in 4-tag model: only 33.22% accuracy with word-context model

### 🧪 Error Patterns

* Confusions often occur between syntactically similar tags
* Collapsed 4-tag model reduces ambiguity
* Word-dependent model overfits due to sparse combinations

---

## 🔑 Key Takeaways

1. **🔁 Simpler tag sets generalize better:**
   The 4-tag model outperforms the 36-tag model due to reduced sparsity.

2. **📈 More context helps, but not always:**
   Second-order HMM slightly improves performance.
   Word-based context adds complexity but degrades results without sufficient data.

3. **⚖️ Trade-offs exist between specificity and accuracy:**
   Fine-grained models capture nuance but struggle with rare categories.

---

## 🚀 Future Directions

* ✨ Apply **smoothing techniques** (e.g., Laplace, backoff models)
* 🧠 Combine **word and tag dependencies** using hybrid HMMs
* 📚 Integrate **neural word embeddings** for better context modeling
* 🌐 Test cross-domain generalization with different datasets
* 🧮 Explore **ensemble or backoff strategies** for rare tags

---
