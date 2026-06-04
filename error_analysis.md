# Error Analysis

## Objective

This report analyzes incorrect predictions made by the churn model to understand failure cases and business trade-offs.

The analysis focuses on:

* False Positives
* False Negatives
* Customer-level interpretation
* Business implications

The final model uses a probability threshold of **0.4**.

---

# False Positives

False positives are customers predicted as likely to churn but who ultimately did not churn.

These cases may increase retention spending unnecessarily but are generally less harmful than missing true churners.

| Customer ID | Actual Churn | Predicted | Probability | Interpretation                                         |
| ----------- | -----------: | --------: | ----------: | ------------------------------------------------------ |
| CUST00044   |            0 |         1 |       0.471 | Borderline churn probability due to inactivity signals |
| CUST00109   |            0 |         1 |       0.566 | Likely predicted due to weaker engagement              |
| CUST00335   |            0 |         1 |       0.654 | High churn-like behavior but customer retained         |
| CUST00437   |            0 |         1 |       0.880 | Strong churn indicators despite retention              |
| CUST00491   |            0 |         1 |       0.583 | Customer behavior resembled churn profile              |

### Observations

Common patterns among false positives:

* Reduced engagement
* Lower session activity
* Higher recency values
* Churn-like browsing behavior

Business interpretation:

These customers may still benefit from light-touch retention campaigns instead of expensive discounts.

---

# False Negatives

False negatives are customers predicted as retained but who actually churned.

These are more expensive mistakes because churned customers receive no intervention.

| Customer ID | Actual Churn | Predicted | Probability | Interpretation                                    |
| ----------- | -----------: | --------: | ----------: | ------------------------------------------------- |
| CUST00184   |            1 |         0 |       0.086 | Historically stable customer unexpectedly churned |
| CUST00247   |            1 |         0 |       0.344 | Moderate churn signal below threshold             |
| CUST00414   |            1 |         0 |       0.380 | Close to threshold but missed                     |
| CUST00438   |            1 |         0 |       0.317 | Limited observable warning signals                |
| CUST00531   |            1 |         0 |       0.365 | Churn behavior insufficiently captured            |

### Observations

Common patterns among false negatives:

* Sudden behavior changes
* Previously loyal customers
* Missing behavioral warning signals
* Probability values close to threshold

Business interpretation:

These cases suggest the model may benefit from additional signals such as:

* customer complaints
* return history
* campaign interactions
* support sentiment

---

# Business Trade-Off

The threshold of **0.4** intentionally prioritizes recall.

This means:

### Accepted Cost

More false positives

### Avoided Cost

Missing actual churners

Because losing customers is typically more expensive than sending unnecessary retention messages, this trade-off is justified for the business objective.

---

# Recommendations

To improve future performance:

1. Add richer customer support features
2. Include campaign interaction behavior
3. Monitor prediction drift over time
4. Retrain model periodically
5. Experiment with Gradient Boosting or XGBoost models
