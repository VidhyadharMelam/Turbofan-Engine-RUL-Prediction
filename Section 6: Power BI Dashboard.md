# Turbofan Engine Health Monitoring — Section 6: Power BI Dashboard

## 6.1 Goal
Create an interactive Power BI dashboard to visualize:
- Engine health trends over cycles
- Predicted Remaining Useful Life (RUL) per engine
- Failure risk indicators
- Model accuracy summary

---

## 6.2 Prepare Data for Power BI
- Export processed dataset with predictions from Colab:
  ```python
  results = pd.DataFrame({
      'engine_id': X_test['engine_id'],
      'cycle': X_test['cycle'],
      'actual_RUL': y_test,
      'predicted_RUL_rf': y_pred_rf,
      'predicted_RUL_xgb': y_pred_xgb
  })

  results.to_csv("/content/drive/MyDrive/turbofan-engine-health-monitoring/data/processed/results_for_dashboard.csv", index=False)
Upload results_for_dashboard.csv into the dashboard/ folder.

6.3 Import Data into Power BI
Open Power BI Desktop.

Click Get Data → Text/CSV.

Select results_for_dashboard.csv.

Load data into Power BI.

6.4 Create Visuals
Engine Health Trends: Line chart of sensor values vs cycles.

Predicted RUL per Engine: Bar chart showing predicted vs actual RUL.

Failure Risk Indicators: Conditional formatting (red = high risk, green = safe).

Model Accuracy Summary: Table with RMSE, MAE, R² for each model.

6.5 Dashboard Layout
Arrange visuals into sections:

Top Left: Engine lifecycle trends.

Top Right: Predicted vs Actual RUL comparison.

Bottom Left: Failure risk indicators.

Bottom Right: Model performance summary.

6.6 Save Dashboard
Save file as rul_dashboard.pbix inside dashboard/.

Export screenshots to outputs/figures/ for README documentation.

🎯 Deliverables (Section 6)
Power BI dashboard (rul_dashboard.pbix) with:

Engine health trends

Predicted RUL per engine

Failure risk indicators

Model accuracy summary

Screenshots saved in outputs/figures/

Dashboard section documented in README
