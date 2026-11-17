# Building Energy Load Forecaster

Estimate heating and cooling loads from building geometry and glazing characteristics.

## Dataset

[UCI Energy Efficiency dataset](https://archive.ics.uci.edu/dataset/242/energy%2Befficiency) (dataset ID 242), 768 records. The source is public and is fetched by the runner; the raw dataset is not committed.

## Run

```bash
python -m pip install -r requirements.txt
python main.py --output-dir artifacts
```

The runner saves `artifacts/metrics.json`, `artifacts/holdout_predictions.csv`, and `artifacts/model.joblib`. For SMS, the UCI CC BY 4.0 archive is downloaded to the ignored `data/` cache because the repository's importer does not currently expose that dataset. The raw messages are never written to the report.

## Holdout results

A random 75/25 split (seed 42) is used. Numeric inputs are median-imputed; a 400-tree random-forest regressor is compared with a median predictor. random 75/25 holdout; seed=42.

| Target | MAE | RMSE | R² | Median baseline MAE |
|---|---:|---:|---:|---:|
| Y1 | 0.347 | 0.493 | 0.998 | 9.458 |
| Y2 | 1.184 | 1.909 | 0.961 | 8.920 |

Full aggregate metrics and the exact split seed are in [`reports/benchmark.json`](reports/benchmark.json).

## Limits

This is an engineering simulation/design benchmark, not metered operational building data. The random holdout does not establish generalization to new buildings. These are one-time benchmark results, not service-level, production, or causal claims.

## Reproducibility

The model and split use seed 42. Re-running downloads source data from UCI and regenerates local artifacts. Model binaries, raw inputs, and row-level predictions are excluded from this public repository.
