🔹 Notebook Flow (Step by Step)
1. Mount Google Drive
Access dataset and outputs folder.

python
from google.colab import drive
drive.mount('/content/drive')
2. Load Processed Dataset
Bring in the cleaned turbofan dataset.

python
import pandas as pd

processed_path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/processed/fd001_processed.csv"
processed = pd.read_csv(processed_path)

print("Processed dataset loaded:", processed.shape)
print(processed.head())
3. Define Features and Target
Separate predictors and target (RUL).

python
X = processed.drop(columns=['RUL'])
y = processed['RUL']
4. Train/Test Split
Essential for evaluation.

python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
5. Safeguard: Load Models if Available
Avoid retraining every time.

python
import joblib, os

lr_path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/lr_model.pkl"
rf_path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/rf_model.pkl"
xgb_path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/xgb_model.pkl"

if os.path.exists(lr_path): lr_model = joblib.load(lr_path)
if os.path.exists(rf_path): rf_model = joblib.load(rf_path)
if os.path.exists(xgb_path): xgb_model = joblib.load(xgb_path)
6. Train & Save Baseline (Linear Regression)
Benchmark model.

python
from sklearn.linear_model import LinearRegression

lr_model = LinearRegression()
lr_model.fit(X_train, y_train)
joblib.dump(lr_model, lr_path)
7. Evaluate Baseline
python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import numpy as np

y_pred_lr = lr_model.predict(X_test)
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred_lr)))
print("MAE:", mean_absolute_error(y_test, y_pred_lr))
print("R²:", r2_score(y_test, y_pred_lr))
8. Train & Save Random Forest
python
from sklearn.ensemble import RandomForestRegressor

rf_model = RandomForestRegressor(n_estimators=200, random_state=42, n_jobs=-1)
rf_model.fit(X_train, y_train)
joblib.dump(rf_model, rf_path)
9. Evaluate Random Forest
python
y_pred_rf = rf_model.predict(X_test)
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred_rf)))
print("MAE:", mean_absolute_error(y_test, y_pred_rf))
print("R²:", r2_score(y_test, y_pred_rf))
10. Train & Save XGBoost
python
!pip install xgboost
from xgboost import XGBRegressor

xgb_model = XGBRegressor(
    n_estimators=300, learning_rate=0.05, max_depth=6,
    subsample=0.8, colsample_bytree=0.8, random_state=42, n_jobs=-1
)
xgb_model.fit(X_train, y_train)
joblib.dump(xgb_model, xgb_path)
11. Evaluate XGBoost
python
y_pred_xgb = xgb_model.predict(X_test)
print("RMSE:", np.sqrt(mean_squared_error(y_test, y_pred_xgb)))
print("MAE:", mean_absolute_error(y_test, y_pred_xgb))
print("R²:", r2_score(y_test, y_pred_xgb))
12. Hyperparameter Tuning (XGBoost)
python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_estimators': [200, 300, 400],
    'max_depth': [4, 6, 8],
    'learning_rate': [0.01, 0.05, 0.1],
    'subsample': [0.8, 1.0],
    'colsample_bytree': [0.8, 1.0]
}

grid_search = GridSearchCV(
    XGBRegressor(random_state=42, n_jobs=-1),
    param_grid, cv=3, scoring='neg_root_mean_squared_error', verbose=2
)
grid_search.fit(X_train, y_train)
print("Best parameters:", grid_search.best_params_)
13. Train & Save Best XGBoost
python
best_xgb_model = XGBRegressor(**grid_search.best_params_, random_state=42, n_jobs=-1)
best_xgb_model.fit(X_train, y_train)
joblib.dump(best_xgb_model, "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/xgb_model_best.pkl")
14. Compare All Models
python
results = {
    "Linear Regression": {"RMSE": rmse_lr, "MAE": mae_lr, "R²": r2_lr},
    "Random Forest": {"RMSE": rmse_rf, "MAE": mae_rf, "R²": r2_rf},
    "XGBoost": {"RMSE": rmse_xgb, "MAE": mae_xgb, "R²": r2_xgb}
}
print(results)
15. Feature Importance (Random Forest)
python
import matplotlib.pyplot as plt
import numpy as np

importances = rf_model.feature_importances_
indices = np.argsort(importances)[::-1]

plt.figure(figsize=(10,6))
plt.title("Random Forest Feature Importance")
plt.bar(range(X.shape[1]), importances[indices])
plt.xticks(range(X.shape[1]), X.columns[indices], rotation=90)
plt.show()
16. Sample Test Data for SHAP
python
X_sample = X_test.sample(200, random_state=42)
17. SHAP for Random Forest
python
import shap

explainer_rf = shap.TreeExplainer(rf_model)
shap_values_rf = explainer_rf.shap_values(X_sample)
shap.summary_plot(shap_values_rf, X_sample, plot_type="bar")
shap.summary_plot(shap_values_rf, X_sample)
18. SHAP for Best XGBoost
python
explainer_xgb = shap.TreeExplainer(best_xgb_model)
shap_values_xgb = explainer_xgb.shap_values(X_sample)
shap.summary_plot(shap_values_xgb, X_sample, plot_type="bar")
shap.summary_plot(shap_values_xgb, X_sample)
19. Local Explanation (Force Plot)
python
shap.initjs()  # load JS for visualization
engine_index = 0
shap.force_plot(
    explainer_xgb.expected_value,
    shap_values_xgb[engine_index,:],
    X_sample.iloc[engine_index,:]
)
🔹 What You Achieve
Train/test split ensures proper evaluation.

Safeguarding + saving models makes the pipeline reusable.

Hyperparameter tuning improves accuracy.

Comparison table shows model progression.

Feature importance + SHAP provide interpretability.

Local explanations make it real‑time and actionable for maintenance teams.
