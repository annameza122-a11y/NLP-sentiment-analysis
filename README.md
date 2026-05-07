# Sentiment Analysis — Project Manual

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Dataset](#2-dataset)
3. [System Requirements](#3-system-requirements)
4. [How to Run](#4-how-to-run)
5. [Model Architecture](#5-model-architecture)
6. [Results](#6-results)
7. [Live Demo](#7-live-demo)
8. [Ethical Considerations](#8-ethical-considerations)

---

## 1. Project Overview

This project implements a **Sentiment Analysis system** using a Bidirectional LSTM neural network built with TensorFlow and Keras.

The system classifies product reviews as **Positive** or **Negative** based on the text content. It was trained on the Multi-Domain Sentiment Dataset from Johns Hopkins University, covering four product categories: Books, DVD, Electronics, and Kitchen & Housewares.

A live web interface is available for real-time sentiment prediction.

---

## 2. Dataset

- **Source:** [Multi-Domain Sentiment Dataset — Johns Hopkins University](https://www.cs.jhu.edu/~mdredze/datasets/sentiment/)
- **Categories:** Books, DVD, Electronics, Kitchen & Housewares
- **Total reviews loaded:** ~8,000
- **After cleaning and balancing:** ~6,000 (50% positive, 50% negative)

The dataset was balanced to ensure equal representation of both sentiment classes, avoiding model bias toward the majority class.

---

## 3. System Requirements

To run the notebook in Google Colab, no local installation is required. The following libraries are used:

| Library | Purpose |
|---|---|
| TensorFlow / Keras | Building and training the LSTM model |
| NLTK | Text tokenisation and stopword removal |
| BeautifulSoup | Parsing raw XML review files |
| Scikit-learn | Train/test split |
| Gradio | Web interface |
| Transformers (HuggingFace) | BERT benchmark comparison |
| Matplotlib / WordCloud | Visualisations |

---

## 4. How to Run

### Option A — Google Colab (Recommended)
1. Open the notebook in Google Colab
2. Click **Runtime → Run All**
3. Wait for training to complete (~2-3 minutes)
4. The model will be saved automatically

### Option B — Live Web App
Access the deployed app directly — no setup required:

🔗 **[https://huggingface.co/spaces/AnaM2027/sentiment-analysis]**

Enter any product review in the text field and click **Submit** to get a prediction.

---

## 5. Model Architecture

The model uses a **Bidirectional LSTM** architecture with the following layers:

### Preprocessing Pipeline
1. Lowercase and remove non-alphabetic characters
2. Remove stopwords — **negation words preserved** (not, no, never, but, however)
3. Generate bigrams (e.g. `not_bad`, `very_good`) to capture short-range context
4. Keras tokenizer with `vocab_size=10,000`
5. Pad/truncate sequences to `max_length=400`

### Training Configuration
| Parameter | Value |
|---|---|
| Vocab size | 10,000 |
| Max sequence length | 400 |
| Embedding dimensions | 100 |
| LSTM units | 64 (x2 bidirectional) |
| Batch size | 32 |
| Max epochs | 10 |
| Early stopping patience | 3 |
| Optimiser | Adam |
| Loss function | Binary Crossentropy |

---

## 6. Results

| Metric | Value |
|---|---|
| Best validation accuracy | ~0.80 |
| Best validation loss | ~0.44 |
| Epochs trained | 4-5 (early stopping) |

### Training Behaviour
The model reaches its best performance at epoch 1-2 and then begins to overfit — training accuracy climbs to ~98% while validation accuracy plateaus around 80%. Early stopping automatically restores the best weights.

### BERT Benchmark Comparison
The model was benchmarked against **DistilBERT** (Google), a pre-trained transformer fine-tuned on millions of examples. DistilBERT represents near-state-of-the-art performance and serves as an upper-bound reference for this task.

| Model | Approach | Accuracy |
|---|---|---|
| Our LSTM | Trained from scratch | ~80% |
| DistilBERT | Pre-trained + fine-tuned | ~95%+ |

---

## 7. Live Demo

The sentiment analysis system is deployed as a web application on Hugging Face Spaces:

🔗 **[https://huggingface.co/spaces/AnaM2027/sentiment-analysis]**

**How to use:**
1. Enter any product review in the text box
2. Click **Submit**
3. The model returns either **Positive review** or **Negative review** with a confidence score

---

## 8. Ethical Considerations

### 8.1 Dataset Bias
The training data covers only four product categories (Books, DVD, Electronics, Kitchen & Housewares) from a specific time period. The model may perform poorly on reviews from other domains such as food, travel, or healthcare. Any deployment outside these categories should be validated carefully.

### 8.2 Class Balancing
The dataset was deliberately balanced to contain an equal number of positive and negative reviews. Without this step, a model trained on imbalanced data could develop a bias toward the majority class, achieving high accuracy simply by always predicting the most common label — without actually understanding sentiment.

### 8.3 Negation and Ambiguity
The model struggles with ambiguous or nuanced language such as double negatives ("not bad"), sarcasm ("oh great, another broken product"), and cultural expressions. Misclassifying these cases in a real-world application — such as automated customer feedback routing — could lead to incorrect business decisions.

### 8.4 Language and Cultural Bias
The model was trained exclusively on English text. It will produce unreliable results on reviews written in other languages or dialects. Deploying this system in multilingual environments without adaptation would be inappropriate.

### 8.5 Transparency and Explainability
The LSTM model is a black box — it produces a prediction without explaining which words or phrases drove the decision. In high-stakes applications (e.g. flagging negative reviews for human escalation), the lack of explainability could undermine user trust and accountability.

### 8.6 Privacy
Product reviews may contain personally identifiable information (PII) such as names, addresses, or order details. Any system processing real customer reviews must comply with relevant data protection regulations such as GDPR and must not store or log user inputs without consent.

### 8.7 Misuse Potential
A sentiment classifier could be misused to automatically suppress or filter negative reviews, censor user feedback, or manipulate perceived product ratings. Responsible deployment requires human oversight and clear policies on how predictions are used.

### 8.8 Model Limitations vs Human Judgment
With ~80% accuracy, the model misclassifies approximately 1 in 5 reviews. It should be used as a **decision support tool**, not as a fully autonomous system. Human review remains essential for edge cases and high-impact decisions.

---


