# Distillation Column Soft Sensor — Dashboard

A small Streamlit app that predicts top-product (ethanol) mole fraction from tray
temperatures and flow rates, using the Random Forest and XGBoost models trained and
validated in the project notebooks.

## Setup

```bash
pip install -r requirements.txt
```

## Run

```bash
streamlit run app.py
```

Then open the URL Streamlit prints (usually `http://localhost:8501`) in a browser.

## What's inside

- `app.py` — the dashboard
- `rf_model.pkl`, `xgb_model.pkl` — Random Forest and XGBoost models, refit on the full
  4,408-row dataset using the hyperparameters selected via group-aware cross-validation
  in `03_Model_Training_Comparison.ipynb`
- `feature_stats.json` — min/max/mean per feature, used to set slider ranges and defaults

## Notes

- Both models were validated with a **group-aware train/test split** (see the project
  report for why this matters) and reached Test R² \u2248 0.999 with a train-test gap under
  0.001 — this is the evidence for trusting them enough to deploy.
- These models were trained on clean, noise-free simulation data covering 13 operating
  points. Treat predictions for inputs far outside the slider ranges (which are set from
  the training data's actual min/max) with appropriate caution.
- This is a prediction demo, not a control system — it doesn't connect to a live plant
  historian or DCS.
