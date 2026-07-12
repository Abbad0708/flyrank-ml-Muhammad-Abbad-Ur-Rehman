# FlyRank Refresh Opportunity Model Report

This report is generated from the bundled anonymized starter dataset (`data/raw/content_refresh_anonymized.csv`).
The model ranks existing content for refresh review. It does not use titles, URLs, client names, domains, or keywords.

## Data

- Rows scored: 30,000
- Declining-label rows: 16,262
- Declining-label rate: 0.542
- Split strategy used for validation: client_holdout
- Target: `is_declining_label`

## Model Comparison

Best model: `random_forest` selected by `precision_at_50`.

| Model | ROC AUC | Avg precision | Precision@50 | Recall | F1 |
|---|---:|---:|---:|---:|---:|
| decision_tree | 0.742 | 0.575 | 0.540 | 0.716 | 0.634 |
| logistic_regression | 0.700 | 0.522 | 0.400 | 0.567 | 0.566 |
| random_forest | 0.750 | 0.618 | 0.740 | 0.744 | 0.640 |
| baseline_rules | 0.627 | 0.468 | 0.240 | - | - |

## Final Queue

- High-confidence items: 3,605
- Medium-confidence items: 11,395
- Low-confidence items: 15,000
- `monitor` items: 13,093
- `refresh` items: 8,178
- `refresh_and_review_ctr` items: 6,657
- `refresh_and_review_engagement` items: 1,990
- `expand_and_refresh` items: 82

## Top Features

- `days_with_impressions`: 0.1578
- `log_impressions_90d`: 0.1282
- `avg_position`: 0.1090
- `content_age_days`: 0.0955
- `char_count`: 0.0426
- `word_count`: 0.0397
- `log_clicks_90d`: 0.0346
- `ctr`: 0.0330
- `scroll_rate`: 0.0311
- `days_with_sessions`: 0.0280

## Top 10 Queue Preview

| Rank | Score | Model probability | Action | Reasons | Impressions | Sessions | Trend |
|---:|---:|---:|---|---|---:|---:|---|
| 1 | 81.6 | 0.782 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, low_engagement_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate, engagement_review_candidate | 12834 | 66 | down |
| 2 | 81.4 | 0.788 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 8064 | 23 | down |
| 3 | 81.4 | 0.847 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 2498 | 9 | down |
| 4 | 81.0 | 0.774 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 13790 | 27 | down |
| 5 | 80.9 | 0.815 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 3393 | 5 | down |
| 6 | 80.8 | 0.796 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 5811 | 14 | down |
| 7 | 80.6 | 0.846 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 1622 | 20 | down |
| 8 | 80.4 | 0.835 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 2621 | 10 | down |
| 9 | 80.4 | 0.843 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 1597 | 5 | down |
| 10 | 80.3 | 0.844 | refresh | declining_with_demand, model_decline_risk, visible_model_opportunity | 3867 | 5 | down |

## Generated Files

- `outputs/refresh_queue.csv`
- `outputs/model_results.json`
- `outputs/summary.json`
- `outputs/charts/action_mix.svg`
- `outputs/charts/confidence_mix.svg`
- `outputs/charts/top_reason_codes.svg`
- `outputs/charts/top_feature_importance.svg`
- `outputs/charts/trend_distribution.svg`

## Practical Use

Use the ranked queue as a reviewer aid, not as an automatic publishing decision.
The safest first production use is to inspect high-confidence rows, verify the page manually, and compare the recommendation against editorial context.


## Submission

Submission checklist and reproduction instructions for reviewers:

- Repository URL: https://github.com/your-username/your-repo  <!-- REPLACE with your public repo URL -->
- Commit: `<git commit hash>`  <!-- REPLACE with the commit hash you are submitting -->
- Notebooks executed (top→bottom): `notebooks/01_first_look_and_discovery.ipynb`, `notebooks/02_your_first_readable_model.ipynb`

Reproduce locally (recommended):

```bash
pip install -r requirements.txt
python -m pip install jupyter nbconvert
# to execute notebooks (creates executed notebook outputs in-place)
jupyter nbconvert --to notebook --execute notebooks/01_first_look_and_discovery.ipynb
jupyter nbconvert --to notebook --execute notebooks/02_your_first_readable_model.ipynb
# or run the pipeline script
python scripts/run_all.py
```

Quick links inside the repo (edit these after making the repo public):

- Notebook 1: `notebooks/01_first_look_and_discovery.ipynb`
- Notebook 2: `notebooks/02_your_first_readable_model.ipynb`
- This report: `outputs/model_report.md`

Notes for reviewers:

- The model was trained on the anonymized starter dataset (`data/raw/content_refresh_anonymized.csv`).
- Key metric used for selection: `Precision@50` (random_forest selected).
- Known limitations: small starter dataset, client-holdout split can still leak some temporal patterns, and results are illustrative.

If you want, I attached the executed notebooks and this report as a ZIP; otherwise reviewers can open the notebooks in the repo link above.
