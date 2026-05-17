# Turbofan Engine Health Monitoring — Section 5: Evaluation

## 5.1 Goal
Evaluate the trained models (Linear Regression, Random Forest, XGBoost) using appropriate metrics and visualizations.  
We will compare performance and identify the best model for RUL prediction.

---

## 5.2 Load Models and Predictions
```python
import joblib

# Load saved models
lr = joblib.load("/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/linear_regression.pkl")
rf = joblib.load("/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/random_forest.pkl")
xgb = joblib.load("/content/drive/MyDrive/turbofan-engine-health-monitoring/outputs/models/xgboost.pkl")

# Generate predictions
y_pred_lr = lr.predict(X_test)
y_pred_rf = rf.predict(X_test)
y_pred_xgb = xgb.predict(X_test)
5.3 Evaluation Metrics
Compute RMSE, MAE, and R² for each model.

python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

def evaluate_model(y_true, y_pred, model_name):
    rmse = mean_squared_error(y_true, y_pred, squared=False)
    mae = mean_absolute_error(y_true, y_pred)
    r2 = r2_score(y_true, y_pred)
    print(f"{model_name} -> RMSE: {rmse:.2f}, MAE: {mae:.2f}, R²: {r2:.2f}")

evaluate_model(y_test, y_pred_lr, "Linear Regression")
evaluate_model(y_test, y_pred_rf, "Random Forest")
evaluate_model(y_test, y_pred_xgb, "XGBoost")
5.4 Predicted vs Actual RUL Plot
Visualize how well predictions match actual RUL values.

python
import matplotlib.pyplot as plt

plt.figure(figsize=(10,6))
plt.scatter(y_test, y_pred_rf, alpha=0.5, label="Random Forest")
plt.scatter(y_test, y_pred_xgb, alpha=0.5, label="XGBoost")
plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 'r--', label="Perfect Prediction")
plt.xlabel("Actual RUL")
plt.ylabel("Predicted RUL")
plt.title("Predicted vs Actual RUL")
plt.legend()
plt.show()
5.5 Model Comparison Table
Document results in a table format:

Model	RMSE	MAE	R² Score
Linear Regression	TBD	TBD	TBD
Random Forest	TBD	TBD	TBD
XGBoost	TBD	TBD	TBD


(Fill in actual values after running evaluation.)

5.6 Save Evaluation Outputs
Save plots into outputs/figures/.

Update results table in README.

Document findings in 04_evaluation.ipynb.

🎯 Deliverables (Section 5)
Notebook 04_evaluation.ipynb containing:

Evaluation metrics for all models.

Predicted vs Actual RUL plots.

Model comparison table.

Plots saved in outputs/figures/.

Results updated in README.
