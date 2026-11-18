# Wk9 MLflow tracking

Install the Wk9 dependencies and run the training pipeline from this directory:

```bash
cd Wk9
python -m pip install -r requirements.txt
python -m src.components.data_ingestion
```

The trainer records one MLflow run per evaluated model in the
`student-performance-regression` experiment. Runs include tuned parameters,
test R2 and RMSE metrics, a `is_best_model` tag, and the fitted model artifact.
By default, run metadata is stored in `Wk9/mlflow.db` and model artifacts in
`Wk9/mlartifacts`. Set `MLFLOW_TRACKING_URI` to use a different MLflow tracking
server or store.

Start the UI in a separate terminal from `Wk9`:

```bash
python -m mlflow ui --backend-store-uri sqlite:///mlflow.db --host 127.0.0.1 --port 5000
```

Then open <http://127.0.0.1:5000> and select the
`student-performance-regression` experiment.

Model artifacts use CloudPickle for compatibility with the different estimator
libraries; only load artifacts from tracking stores you trust.
