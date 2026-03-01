# 🍽️ Amazon Fine Food Reviews — Sentiment Analysis

![Word Cloud](sentiment_wordcloud_cover.png)

> **An NLP sentiment analysis pipeline on 568,454 Amazon food reviews, using the AFINN lexicon for sentiment labeling and comparing 4 machine learning models to classify review sentiment.**

---

## 📌 Project Overview

This project builds a complete **Natural Language Processing (NLP) pipeline** to classify Amazon Fine Food Reviews as Positive or Negative. Starting from raw text data, the pipeline covers text preprocessing, sentiment labeling using the AFINN lexicon, feature extraction via TF-IDF, and training and comparing 4 machine learning models.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **R** | Full NLP and ML pipeline |
| **tidytext** | Text tokenization and AFINN lexicon |
| **tm** | Text corpus and document-term matrix |
| **caret** | Model training and evaluation framework |
| **e1071** | Naive Bayes and SVM |
| **randomForest** | Random Forest (ranger implementation) |
| **glmnet** | Logistic Regression (sparse matrix) |
| **pROC** | ROC curves and AUC scoring |
| **wordcloud** | Word cloud visualizations |
| **ggplot2** | Model comparison and distribution plots |

---

## 📂 Repository Structure

```
📁 sentiment-analysis/
│
├── 📄 sentiment_analysis.R              ← Full R analysis script
├── 📄 reviews_with_sentiment.csv        ← Labelled dataset
├── 📄 model_comparison_report.csv       ← Model performance table
├── 📄 best_sentiment_model.rds          ← Best performing model
├── 📄 model_naive_bayes.rds             ← Saved Naive Bayes model
├── 📄 model_svm.rds                     ← Saved SVM model
├── 📄 model_logistic_regression.rds     ← Saved Logistic Regression
├── 📄 model_random_forest.rds           ← Saved Random Forest
├── 🖼️  sentiment_wordcloud_cover.png    ← README cover image
├── 🖼️  plot_afinn_scores.png            ← AFINN score distribution
├── 🖼️  plot_top_words.png               ← Top words by sentiment
├── 🖼️  plot_model_comparison.png        ← Model performance chart
├── 🖼️  plot_sentiment_distribution.png  ← Sentiment label counts
└── 📄 README.md
```

---

## 📊 Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | [Kaggle — Amazon Fine Food Reviews](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews) |
| **Total Reviews** | 568,454 |
| **Date Range** | October 1999 — October 2012 |
| **Key Columns** | Id, Score (1–5 stars), Summary, Text |
| **Sample Used** | ~50,000 (stratified sample for ML performance) |

---

## ⚙️ Analysis Pipeline

### Step 1 — Data Import & Cleaning
- Selected relevant columns: Id, Score, Summary, Text
- Removed duplicates and missing values
- Excluded neutral reviews (Score = 3) — ambiguous for binary classification
- Applied stratified sampling (~50,000 reviews)

### Step 2 — Sentiment Labeling (AFINN Lexicon)
- Tokenized review text word by word
- Joined tokens with AFINN lexicon (scores: −5 to +5)
- Aggregated scores per review:
  - AFINN Score > 0 → **Positive**
  - AFINN Score < 0 → **Negative**
  - AFINN Score = 0 → Excluded
- Validated labels against star ratings (cross-tabulation)

### Step 3 — Text Preprocessing
Applied the following cleaning steps via `tm` corpus:

| Step | Action |
|------|--------|
| Lowercasing | Convert all text to lowercase |
| Number removal | Remove all numeric characters |
| Punctuation removal | Strip all punctuation marks |
| Stopword removal | Remove common English stopwords |
| Whitespace stripping | Remove extra spaces |
| Stemming | Reduce words to root form |

### Step 4 — Class Imbalance Handling
- Checked positive/negative class ratio
- Applied **downsampling** if imbalance ratio > 1.5
- Rebuilt corpus after resampling

### Step 5 — Feature Creation
| Method | Description |
|--------|-------------|
| Bag of Words (BoW) | Baseline document-term matrix |
| TF-IDF | Term Frequency-Inverse Document Frequency weighting |
| Sparsity removal | Kept terms appearing in ≥ 0.5% of documents |

### Step 6 — Model Training
All 4 models trained with **5-fold cross-validation**:

| Model | Method | Key Parameter |
|-------|--------|--------------|
| Naive Bayes | naive_bayes | Probabilistic classifier |
| SVM | svmLinear | Linear kernel |
| Logistic Regression | glmnet | L1/L2 regularization |
| Random Forest | ranger | 100 trees |

---

## 📊 Model Performance

| Model | Accuracy | Precision | Recall | F1 Score | AUC |
|-------|---------|-----------|--------|---------|-----|
| Naive Bayes | — | — | — | — | — |
| SVM | — | — | — | — | — |
| Logistic Regression | — | — | — | — | — |
| Random Forest | — | — | — | — | — |

*Results vary based on random seed and sample — run the script to see your exact values in `model_comparison_report.csv`*

---

## 💡 Key Findings

**Top Positive Words:** delicious, love, great, perfect, amazing, excellent, fresh, tasty, wonderful, best

**Top Negative Words:** disappointed, terrible, awful, waste, horrible, disgusting, stale, bland, overpriced, nasty

**Business Insights:**
- Products with consistent positive sentiment signal strong brand loyalty and repeat purchase potential
- Negative reviews cluster around taste, packaging, delivery, and misleading descriptions
- Sentiment scores can be used to **prioritize customer service tickets** and **flag products** for quality review
- Top positive words can directly inform **product descriptions and marketing copy**

---

## 🚀 How to Run

```r
# 1. Install required packages (first run only)
install.packages(c("tidyverse", "tidytext", "textdata",
                   "tm", "caret", "e1071", "randomForest",
                   "glmnet", "pROC", "wordcloud",
                   "RColorBrewer", "doParallel"))

# 2. Set working directory
setwd("path/to/your/folder")

# 3. Place Reviews.csv in working directory
# Download from: https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews

# 4. Run the script
source("sentiment_analysis.R")

# Note: Training 4 models takes 15-30 minutes
# Parallel processing is enabled automatically
```

**Output files generated:**
- `reviews_with_sentiment.csv` — labelled dataset
- `model_comparison_report.csv` — all 4 models compared
- `best_sentiment_model.rds` — top performing model saved
- 4 visualization plots saved as PNG

---

## 👤 Author

**Olusanya Oluwatobi**
- GitHub: [@thibeex](https://github.com/thibeex)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

*Part of a 3-project Data Analytics Portfolio — Customer Segmentation (R) | Sentiment Analysis (R) | Financial Dashboard (R + Power BI)*
