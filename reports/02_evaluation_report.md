# Evaluation Report

Run info: seed=42  primary model=lightgbm  calibration=isotonic

## Classification (test fold)

| metric | value |
|---|---|
| pr_auc | 0.8834 |
| roc_auc | 0.9928 |
| precision | 0.5982 |
| recall | 0.4379 |
| f1 | 0.5057 |
| brier | 0.005 |
| ece | 0.00111 |

## Reliability

- Brier score: **0.005**
- Expected calibration error (ECE): **0.00111**

## Alert operations

| metric | value |
|---|---|
| total_transactions | 23928 |
| alerts_generated | 336 |
| alert_rate_pct | 1.4042 |
| high_risk_alerts | 71 |
| review_alerts | 265 |
| monitor_logged | 1705 |
| alert_precision | 0.5982 |
| alert_recall | 0.4379 |
| alerts_per_caught_fraud | 1.67 |

## Cohorts

| cohort | n_rows | n_fraud | fraud_rate | PR-AUC | ROC-AUC | recall@2% | precision@2% | novelty_AUROC | FNR@0.9 |
|---|---|---|---|---|---|---|---|---|---|
| all | 23928 | 459 | 0.019 | 0.8834 | 0.9928 | 0.8322 | 0.7975 | 0.1575 | 0.0727 |
| known_customers | 11729 | 0 | 0.000 | None | None | 0.0 | 0.0 | None | 0.0687 |
| unseen_customers | 12199 | 459 | 0.038 | 0.8894 | 0.9903 | 0.8322 | 0.7975 | 0.1706 | 0.0767 |
| first_time_customers | 1509 | 131 | 0.087 | 0.5889 | 0.9301 | 0.9466 | 0.2589 | 0.1562 | 0.0 |
| new_devices | 455 | 7 | 0.015 | 0.4515 | 0.9785 | 1.0 | 0.0154 | 0.1086 | 0.0 |
| new_merchants | 20 | 0 | 0.000 | None | None | 0.0 | 0.0 | None | 0.0 |

## First-time false positives

- first_time_customer: legit rows=1,378, FP alerts=71, FP rate=0.0515
- first_time_device: legit rows=448, FP alerts=9, FP rate=0.0201
- first_time_merchant: legit rows=20, FP alerts=0, FP rate=0.0
- first_time_any: legit rows=1,656, FP alerts=72, FP rate=0.0435

## Leakage & data-quality checks

- **temporal_integrity**: time-based splits, no shuffle
- **unseen_customer_holdout**: 1,660 customers removed from train only
- **priors_fit_on**: train
- **features_computed_as_of**: point-in-time, commit after scoring
- **raw_ids_in_features**: False
- **velocity_8min_match_rate**: 1.0
- **amount_spike_match_rate**: 0.9962

## Feature availability (cold-start rate)

- customer_history_available_rate: 0.8167
- first_time_customer_rate: 0.0631
- new_device_rate: 0.019
- new_merchant_rate: 0.0008