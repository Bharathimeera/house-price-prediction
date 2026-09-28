# House Price Prediction

A beginner machine learning project that uses Linear Regression to estimate house prices from a small tabular dataset. The notebook explores the data, trains a model with five input features, evaluates its predictions, and compares it with a second model using three features.

> **Note:** This is an educational exercise using only 10 records. The evaluation results are based on a test set of two records and should not be treated as evidence of reliable predictions for real properties.

## Project files

| File | Description |
|---|---|
| `house_prices.ipynb` | Notebook containing data inspection, model training, evaluation, and a feature-set comparison. |
| `house_prices.csv` | Dataset loaded by the notebook. |

Place the notebook and CSV in the same folder. The notebook reads the CSV using the relative filename `house_prices.csv`.

## Dataset

The dataset has 10 rows and six numeric columns. The notebook reports no missing values in the supplied CSV.

| Column | Use in notebook | Description |
|---|---|---|
| `area` | Feature | Property area; the unit is not specified in the files. |
| `bedrooms` | Feature | Number of bedrooms. |
| `bathrooms` | Feature | Number of bathrooms. |
| `age` | Feature | Property age; the unit is not specified in the files. |
| `location_score` | Feature | Numeric location score; its scale is not documented. |
| `price` | Target | House price; currency is not specified in the files. |

## Workflow

1. Load `house_prices.csv` with pandas.
2. Inspect sample rows, data types, summary statistics, and missing-value counts.
3. Select `area`, `bedrooms`, `bathrooms`, `age`, and `location_score` as the first model's features. Use `price` as the target.
4. Split the 10 records into 8 training rows and 2 test rows with `test_size=0.2` and `random_state=42`.
5. Fit a scikit-learn `LinearRegression` model on the training data.
6. Predict prices for the test rows and compare the predictions with the recorded actual prices.
7. Calculate regression metrics and plot actual versus predicted prices.
8. Train and score a second Linear Regression model using only `area`, `bedrooms`, and `location_score`.

The notebook also calls `dropna()`, `fillna(df.mean())`, and forward-fill methods while exploring missing-data handling. The CSV contains no missing values, and the returned DataFrames are not assigned back to `df`; these calls therefore do not change the data used by the models.

## Models and recorded results

Both models use scikit-learn's Linear Regression and the same train/test split.

| Model | Input features | Recorded R² on test set |
|---|---|---:|
| Model 1 | `area`, `bedrooms`, `bathrooms`, `age`, `location_score` | 0.9385 |
| Model 2 | `area`, `bedrooms`, `location_score` | 0.9876 |

For the five-feature model, the notebook records these test predictions and actual prices:

| Predicted price | Actual price |
|---:|---:|
| 4,015,185.95 | 3,750,000 |
| 2,058,615.70 | 2,150,000 |

The same model's recorded metrics are:

- **MAE:** 178,285.12
- **MSE:** 39,337,339,064.95
- **RMSE:** 198,336.43
- **R²:** 0.9385

These values are reproduced from the notebook output. The price unit is not given, so the README does not assign a currency to the error values. R² can be unstable with only two test examples; the higher score of the three-feature model is not enough to establish that it will perform better on new data.

## Libraries and environment

The notebook uses:

- Python (notebook metadata records Python 3.9.12)
- pandas for loading and inspecting tabular data
- scikit-learn for splitting data, fitting Linear Regression, and calculating metrics
- NumPy for the square root used to calculate RMSE
- Matplotlib for the actual-versus-predicted scatter plot
- Jupyter Notebook or JupyterLab to run the notebook

Install the packages used by the notebook with:

```bash
python -m pip install pandas scikit-learn numpy matplotlib jupyter
```

## Run the notebook

1. Keep `house_prices.ipynb` and `house_prices.csv` in the same directory.
2. Install the packages listed above in your Python environment.
3. Open the notebook in Jupyter Notebook or JupyterLab.
4. Run the cells in order.

## Limitations

This project is a learning demonstration, not a production pricing tool. The dataset contains only 10 rows, with 8 used for training and 2 for testing. The dataset source, geographic market, area and age units, location-score scale, and currency are not documented in the supplied files. The notebook does not use cross-validation or a separate larger evaluation dataset. Its metrics and feature comparison should therefore be interpreted cautiously.
