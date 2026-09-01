# Experiment 06 — Time-Series Forecasting of Reported Crime Incidents (AR / ARIMA)

**Course:** MDI3003 — Advanced Predictive Analytics
**Student:** Avinash A | Integrated M.Tech CSE (Data Science), VIT Vellore
**Faculty:** Dr. Durgesh Kumar, Assistant Professor (Senior), SCOPE
**Semester:** Fall 2026-2027

## What this is

`Lab06_TimeSeries_Crime_Forecasting.ipynb` is a runnable, already-executed Jupyter notebook that
reproduces the analysis described in the accompanying lab report: building weekly reported-incident
series for two Chicago-style police districts (District 1 — Central, District 12 — Near West),
diagnosing stationarity and seasonality, fitting AR and ARIMA models on a leakage-safe chronological
split, and evaluating them on a locked 12-week holdout against a naive persistence baseline.

## Data note

The live Chicago Police Department **"Crimes — 2001 to Present"** Socrata portal
(`data.cityofchicago.org`) is not reachable from this environment. As documented in the report
(Section 2), the notebook generates an **instructor-style frozen synthetic extract** locally —
same schema, same general seasonality/trend/COVID-break/autocorrelation shape as the real District 1
and District 12 series — so the pipeline runs end-to-end and produces real, self-consistent outputs.

**This synthetic data must be replaced with the live Socrata extract before any non-classroom use.**
Because the exact random seed/generating process behind the original report figures isn't
recoverable, the specific numbers in this notebook (ADF statistics, AIC values, MAE/RMSE, etc.)
won't match the report exactly — but every test, model, and diagnostic is genuinely computed and
internally consistent.

## Contents / structure

| Section | What it does |
|---|---|
| 1–2 | Imports, random seed, synthetic weekly series generation for both districts |
| 3 | Chronological train/test split (last 12 weeks locked as test) |
| 4 | Descriptive statistics and exploratory plots (Figure 1) |
| 5 | Augmented Dickey-Fuller stationarity tests (training data only) |
| 6 | ACF / PACF diagnostics (Figure 2) |
| 7 | ARIMA order grid search (AIC-minimizing) + AR(4) baseline fit |
| 8 | Forecasts and MAE/RMSE on the locked test period (Figure 3) |
| 9 | Residual diagnostics + Ljung-Box test (Figures 4–5) |
| 10 | Rolling-origin (walk-forward) backtest |
| 11 | Summary and responsible-use notes |

## Requirements

- Python 3.11+
- `numpy`, `pandas`, `matplotlib`, `scipy`, `statsmodels`, `nbformat`/`jupyter`

Install with:
```bash
pip install numpy pandas matplotlib scipy statsmodels jupyter
```

## How to run it yourself

```bash
jupyter nbconvert --to notebook --execute --inplace \
  Lab06_TimeSeries_Crime_Forecasting.ipynb
```
or open it directly in Jupyter Lab / Notebook / VS Code and run all cells. All outputs (tables,
printed test statistics, and plots) are already embedded in the file as delivered, so you can also
just open and read it without re-running anything.

## Responsible-use reminder (carried over from the report)

Forecasts describe **reported/recorded incident counts**, not underlying crime prevalence or
individual behavior. This notebook must not be used for patrol allocation, individual risk scoring,
or any real-world deployment — it is a classroom exercise built on simulated stand-in data.
