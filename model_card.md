# Model Card – Customer Churn Prediction

## Model Details

**Model Type:** Classification Model
**Task:** Predict customer churn within the next 60 days

### Models Trained

1. Baseline Model: Logistic Regression
2. Final Model: Random Forest / XGBoost (replace with actual model)

The final model was selected based on stronger validation performance compared to the baseline.

---

## Intended Use

This model is designed for internal retention prioritization.

It should be used to:

* Identify customers at high churn risk
* Prioritize retention campaigns
* Support customer support and marketing teams

It should NOT be used to:

* Automatically block customers
* Make irreversible customer decisions
* Replace human judgment

---

## Data Used

Dataset used:

* Customer behavior features
* RFM-related signals
* Support activity
* Web/app engagement
* Campaign behavior

Target:

* Customer churn within the next 60 days

Only data available on or before the snapshot date was used to avoid data leakage.

---

## Performance

Evaluation metrics include:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

The final model outperformed the baseline model on validation/testing metrics.

See `metrics.json` for exact results.

---

## Feature Importance

Important predictive signals included:

* Recency
* Purchase frequency
* Total spend
* Support complaints
* Website/app activity

Feature importance was analyzed to improve interpretability.

---

## Limitations

* Customer behavior may change over time.
* External factors like pricing or competition are not included.
* Predictions are probabilistic and not guaranteed outcomes.

---

## Ethical Considerations

The model may introduce bias if customer behavior differs significantly across groups.

Retention offers should be reviewed carefully to avoid unfair targeting.

Predictions should assist human decisions rather than fully automate them.

---

## Monitoring Needs

After deployment, the following should be monitored:

* Data drift
* Prediction distribution changes
* Model performance decay
* Retention campaign effectiveness

Model retraining should be considered if performance drops significantly.
