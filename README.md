# Part 3: Churn Prediction Model & Model Card

## Project Overview

This project develops a customer churn prediction system for a D2C personal-care brand. The objective is to identify customers who are likely to churn within the next 60 days so that the business can prioritize retention efforts efficiently instead of offering discounts to every customer.

The model is intended to support internal marketing, CRM, and customer-retention teams by identifying high-risk customers using historical behavioral patterns.

---

## Business Objective

Customer churn creates a significant loss in repeat revenue for D2C brands. Blind retention campaigns often waste budget on customers who would not churn anyway.

This project aims to:

* Understand churn-driving behavioral patterns
* Predict churn probability for individual customers
* Prioritize high-risk customers for retention interventions
* Reduce unnecessary marketing spend

---

## Dataset

The project uses the provided modeling snapshot dataset:

```text
data/rfm_modeling_snapshot.csv
```

The dataset contains customer-level features derived on or before the snapshot date.

### Feature Categories

#### Customer Attributes

* Age group
* City tier
* Acquisition channel
* Loyalty tier
* Preferred category
* Marketing consent

#### RFM Features

* Recency
* Frequency
* Monetary value

#### Behavioral Features

* Session activity
* Product views
* Cart additions
* Wishlist additions
* Email engagement
* Category diversity
* Discount usage

#### Support Features

* Customer ratings
* Complaint signals

### Target Variable

```text
churn_next_60d
```

Binary target:

* `1` → Customer churned within 60 days
* `0` → Customer retained

---

## Project Structure

```text
part3-churn-model/
│── README.md
│── requirements.txt
│── churn_model.ipynb
│── model.pkl
│── metrics.json
│── error_analysis.md
│── model_card.md
│── data/
│   └── rfm_modeling_snapshot.csv

```

---

## Data Preparation

### Leakage Prevention

To avoid target leakage, only features available on or before the snapshot date were used for modeling.

No post-snapshot information was included as input features.

### Train / Validation / Test Split

The dataset was split into:

* Training set: 72%
* Validation set: 14%
* Test set: 14%

This ensured fair model evaluation on unseen customer behavior.

---

## Models Trained

### 1. Baseline Model – Logistic Regression

A Logistic Regression model was used as a simple baseline for churn classification.

Performance:

* ROC-AUC: **0.8827**
* F1 Score: **0.7832**

---

### 2. Final Model – Random Forest

A Random Forest classifier was trained as the stronger model to capture non-linear customer behavior patterns.

Performance:

* Accuracy: **0.8244**
* Precision: **0.8045**
* Recall: **0.8571**
* F1 Score: **0.8300**
* ROC-AUC: **0.8846**

The Random Forest model was selected as the final model due to improved overall business performance and stronger recall for churn detection.

---

## Threshold Selection

The final decision threshold was set to:

```text
0.4
```

### Business Justification

A lower threshold was chosen to improve recall and identify more at-risk customers.

In churn prediction, missing an actual churner (false negative) is generally more expensive than contacting a customer who would have stayed (false positive).

This threshold helps retention teams intervene earlier and reduce lost customers.

---

## Feature Importance

Top predictive signals included:

1. Recency Days
2. Last Visit Days Ago
3. Monetary Value (180 days)
4. Purchase Frequency (180 days)
5. Category Diversity
6. Product Views (30 days)
7. Average Discount Percentage
8. Days Since Signup
9. Sessions (30 days)
10. Average Rating

Feature importance analysis improves interpretability and helps business teams understand churn drivers.

---

## Outputs

### Model Artifact

* `model.pkl`

### Metrics

* `metrics.json`

### Reports

* `error_analysis.md`
* `model_card.md`

### Visualizations

* Confusion Matrix
* ROC Curve
* Feature Importance Plot

Stored in:

```text
outputs/
```

---

## Installation

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
churn_model.ipynb
```

Run all cells to:

* preprocess data
* train models
* evaluate performance
* generate plots
* save model artifact
* export metrics

---

## Business Impact

This model enables retention teams to:

* Prioritize high-risk customers
* Optimize retention campaign spending
* Reduce customer churn
* Improve customer lifetime value

Instead of generic discounts, the company can focus intervention efforts where they are most needed.
