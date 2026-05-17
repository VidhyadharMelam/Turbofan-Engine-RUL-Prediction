# Turbofan Engine Health Monitoring & Failure Prediction — Project Roadmap

## 1. Setup
- Create clean folder structure:
  - `data/raw`, `data/processed`
  - `notebooks` (EDA, preprocessing, modeling, evaluation)
  - `src` (preprocess.py, model.py)
  - `outputs/figures`, `outputs/models`
  - `dashboard`
- Add `requirements.txt` with dependencies.
- Mount Google Drive in Colab for permanent dataset storage.
- Download NASA C-MAPSS FD001 dataset and place in `data/raw`.
- Initial commit to GitHub with README + structure.

---

## 2. Exploratory Data Analysis (EDA)
- Load dataset into pandas.
- Rename columns (`engine_id`, `cycle`, `setting_1–3`, `sensor_1–21`).
- Explore dataset size, number of engines, cycles per engine.
- Plot sensor trends for one engine (line plots).
- Identify sensors with meaningful degradation vs flat sensors.
- Save plots into `outputs/figures`.

---

## 3. Preprocessing
- Create **RUL target column**: `max_cycle_per_engine - current_cycle`.
- Normalize sensor values (Min-Max scaling).
- Drop low‑variance sensors.
- Apply rolling averages to smooth noisy signals.
- Split into training and test sets.
- Save processed dataset into `data/processed`.

---

## 4. Modeling
- Train baseline **Linear Regression** model.
- Train **Random Forest** model.
- Train **XGBoost** model.
- Save trained models into `outputs/models`.
- Document training process in `03_modeling.ipynb`.

---

## 5. Evaluation
- Compute metrics: RMSE, MAE, R².
- Plot predicted vs actual RUL for test engines.
- Compare models side by side.
- Save evaluation plots into `outputs/figures`.
- Document results in `04_evaluation.ipynb`.

---

## 6. Power BI Dashboard
- Import processed dataset + predictions into Power BI.
- Create visuals:
  - Engine health trends over cycles.
  - Predicted RUL per engine.
  - Failure risk indicators.
  - Model accuracy summary.
- Save dashboard as `dashboard/rul_dashboard.pbix`.

---

## 7. Documentation
- Update README with:
  - Project overview.
  - Dataset details.
  - Methodology (EDA → Preprocessing → Modeling → Evaluation → Dashboard).
  - Results table with metrics.
  - Screenshots of plots/dashboard.
- Add comments in notebooks for clarity.
- Ensure repo looks professional for recruiters.

---

## 8. Final Polish
- Push all notebooks, scripts, outputs, and dashboard to GitHub.
- Add `requirements.txt` and `environment.yml` (optional).
- Ensure commits are clean and descriptive.
- Verify repo runs end‑to‑end in Colab.
- Share GitHub link in resume.

---

## 🎯 Key Deliverables
- **Clean GitHub repo** with structured folders.
- **4 Jupyter notebooks** (EDA, preprocessing, modeling, evaluation).
- **Saved models + plots** in outputs.
- **Power BI dashboard** for business visualization.
- **Updated README** with results and screenshots.
