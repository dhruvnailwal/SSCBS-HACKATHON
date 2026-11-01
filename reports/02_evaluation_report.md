# Evaluation Report

Run info: seed=42  primary model=random_forest  calibration=isotonic

## Classification (test fold)

| metric | value |
|---|---|
| pr_auc | 0.8492 |
| roc_auc | 0.9927 |
| precision | 0.7302 |
| recall | 0.5011 |
| f1 | 0.5943 |
| brier | 0.0062 |
| ece | 0.00205 |

## Reliability

- Brier score: **0.0062**
- Expected calibration error (ECE): **0.00205**

## Alert operations

| metric | value |
|---|---|
| total_transactions | 23928 |
| alerts_generated | 315 |
| alert_rate_pct | 1.3164 |
| high_risk_alerts | 106 |
| review_alerts | 209 |
| monitor_logged | 1815 |
| alert_precision | 0.7302 |
| alert_recall | 0.5011 |
| alerts_per_caught_fraud | 1.37 |

## Cohorts

| cohort | n_rows | n_fraud | fraud_rate | PR-AUC | ROC-AUC | recall@2% | precision@2% | novelty_AUROC | FNR@0.9 |
|---|---|---|---|---|---|---|---|---|---|
| all | 23928 | 459 | 0.019 | 0.8492 | 0.9927 | 0.8083 | 0.7745 | 0.2258 | 0.0775 |
| known_customers | 11729 | 0 | 0.000 | None | None | 0.0 | 0.0 | None | 0.0697 |
| unseen_customers | 12199 | 459 | 0.038 | 0.8507 | 0.989 | 0.8083 | 0.7745 | 0.2104 | 0.0853 |
| first_time_customers | 1509 | 131 | 0.087 | 0.553 | 0.9273 | 0.9466 | 0.2589 | 0.1612 | 0.0 |
| new_devices | 455 | 7 | 0.015 | 0.458 | 0.9624 | 1.0 | 0.0154 | 0.089 | 0.0 |
| new_merchants | 26 | 1 | 0.038 | 1.0 | 1.0 | 1.0 | 0.0385 | 0.0 | 0.0 |

## First-time false positives

- first_time_customer: legit rows=1,378, FP alerts=56, FP rate=0.0406
- first_time_device: legit rows=448, FP alerts=8, FP rate=0.0179
- first_time_merchant: legit rows=25, FP alerts=0, FP rate=0.0
- first_time_any: legit rows=1,662, FP alerts=56, FP rate=0.0337

## Leakage & data-quality checks

- **temporal_integrity**: time-based splits, no shuffle
- **unseen_customer_holdout**: 1,660 customers removed from train only
- **priors_fit_on**: train
- **features_computed_as_of**: point-in-time, commit after scoring
- **raw_ids_in_features**: False
- **velocity_8min_match_rate**: 0.6091
- **amount_spike_match_rate**: 0.9962

## Feature availability (cold-start rate)

- customer_history_available_rate: 0.8167
- first_time_customer_rate: 0.0631
- new_device_rate: 0.019
- new_merchant_rate: 0.0011