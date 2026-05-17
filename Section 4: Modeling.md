# Turbofan Engine Health Monitoring — Section 4: Modeling

## 4.1 Goal
Train machine learning models to predict Remaining Useful Life (RUL) using the preprocessed dataset.  
We will compare three models:
- Linear Regression (baseline)
- Random Forest (ensemble)
- XGBoost (gradient boosting)

---

## 4.2 Load Processed Data
```python
import pandas as pd

path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/processed/train_processed.csv"
data = pd.read_csv(path)

# Separate features and target
X = data.drop(columns=['RUL','max_cycle'])
y = data['RUL']
4.3 Train-Test Split
python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print(X_train.shape, X_test.shape)
4.4 Linear Regression (Baseline)
python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

lr = LinearRegression()
lr.fit(X_train, y_train)

y_pred_lr = lr.predict(X_test)

print("Linear Regression RMSE:", mean_squared_error(y_test, y_pred_lr, squared=False))
print("MAE:", mean_absolute_error(y_test, y_pred_lr))
print("R²:", r2_score(y_test, y_pred_lr))
4.5 Random Forest
python
from sklearn.ensemble import RandomForestRegressor

rf = RandomForestRegressor(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

y_pred_rf = rf.predict(X_test)

print("Random Forest RMSE:", mean_squared_error(y_test, y_pred_rf, squared=False))
print("MAE:", mean_absolute_error(y_test, y_pred_rf))
print("R²:", r2_score(y_test, y_pred_rf))
4.6 XGBoost
python
from xgboost import XGBRegressor

xgb = XGBRegressor(n_estimators=200, learning_rate=0.05, max_depth=5, random_state=42)
xgb.fit(X_train, y_train)

y_pred_xgb = xgb.predict(X_test)

print("XGBoost RMSE:", mean_squared_error(y_test, y_pred_xgb, squared=False))
print("MAE:", mean_absolute_error(y_test, y_pred_xgb))
print("R²:", r2_score(y_test, y_pred_xgb))
4.7 Save Models
python
import joblib

joblib.dump(lr, "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/linear_regression.pkl")
joblib.dump(rf, "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/random_forest.pkl")
joblib.dump(xgb, "/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/xgboost.pkl")
🎯 Deliverables (Section 4)
Notebook 03_modeling.ipynb containing:

Train-test split.

Training of Linear Regression, Random Forest, and XGBoost models.

Evaluation metrics printed for each model.

Saved trained models in outputs/models/.
