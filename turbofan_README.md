# Turbofan Engine Health Monitoring & Failure Prediction

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-1.6+-green.svg)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow.svg)
![Status](https://img.shields.io/badge/Status-In%20Progress-lightgrey.svg)

## 📌 Project Overview

This project applies machine learning techniques to predict the **Remaining Useful Life (RUL)** of aircraft turbofan engines using real sensor data from NASA's C-MAPSS dataset. The goal is to identify engine degradation patterns early, enabling proactive maintenance decisions before failure occurs.

Predictive maintenance is a critical challenge in the aerospace industry. Unplanned engine failures result in costly unscheduled maintenance, flight delays, and safety risks. By accurately forecasting how many operational cycles remain before an engine requires maintenance, airlines and MRO (Maintenance, Repair & Overhaul) facilities can optimise maintenance schedules, reduce downtime, and improve operational efficiency.

This project simulates the kind of data science work being done at aerospace companies like Honeywell, which builds AI-powered maintenance platforms such as Honeywell Forge Performance+ for commercial aerospace operations.

---

## 🎯 Problem Statement

Given multivariate time-series sensor readings from turbofan engines operating under different conditions, can we predict how many cycles remain before an engine fails?

- **Input:** Sensor readings, operational settings, engine ID, cycle number
- **Output:** Predicted Remaining Useful Life (RUL) in cycles
- **Type:** Supervised Regression Problem

---

## 📂 Dataset

**Source:** NASA C-MAPSS (Commercial Modular Aero-Propulsion System Simulation) Dataset  
**Link:** [Kaggle - NASA C-MAPSS](https://www.kaggle.com/datasets/behrad3d/nasa-cmaps)

The dataset contains four subsets (FD001–FD004), each representing different operating conditions and fault modes. This project uses **FD001** as the primary dataset.

| File | Description |
|---|---|
| `train_FD001.txt` | Training data with sensor readings per engine per cycle |
| `test_FD001.txt` | Test data — sensor readings up to a point before failure |
| `RUL_FD001.txt` | True RUL values for test engines |

### Dataset Features

| Feature | Description |
|---|---|
| `engine_id` | Unique engine identifier |
| `cycle` | Operational cycle number |
| `setting_1/2/3` | Operational settings |
| `sensor_1` to `sensor_21` | 21 sensor measurements (temperature, pressure, speed, etc.) |

**Dataset Size:**
- Training: 20,631 rows across 100 engines
- Test: 13,096 rows across 100 engines

---

## 🏗️ Project Structure

```
turbofan-engine-health-monitoring/
│
├── data/
│   └── raw/                        ← Place NASA C-MAPSS dataset files here
│
├── notebooks/
│   ├── 01_EDA.ipynb                ← Exploratory Data Analysis
│   ├── 02_preprocessing.ipynb      ← Feature Engineering & Data Preprocessing
│   ├── 03_modeling.ipynb           ← Model Training & Comparison
│   └── 04_evaluation.ipynb         ← Model Evaluation & Results
│
├── src/
│   ├── preprocess.py               ← Data preprocessing functions
│   └── model.py                    ← Model training and evaluation functions
│
├── dashboard/
│   └── rul_dashboard.pbix          ← Power BI Dashboard
│
├── outputs/
│   ├── figures/                    ← Saved plots and visualisations
│   └── models/                     ← Saved trained models
│
├── requirements.txt                ← Python dependencies
└── README.md                       ← Project documentation
```

---

## 🔬 Methodology

### 1. Exploratory Data Analysis (EDA)
- Analysed sensor reading distributions across engine lifecycles
- Identified sensor degradation trends over operational cycles
- Detected correlations between sensor readings and engine health
- Visualised engine lifecycle patterns across the fleet

### 2. Feature Engineering & Preprocessing
- Created **RUL target column** by calculating cycles remaining per engine
- Applied **Min-Max normalisation** to sensor readings
- Removed sensors with near-zero variance (non-informative sensors)
- Applied **rolling window averages** to smooth noisy sensor signals
- Split data into training and test sets

### 3. Modelling
Three models were built and compared:

| Model | Description |
|---|---|
| Linear Regression | Baseline model for RUL prediction |
| Random Forest | Ensemble model capturing non-linear degradation patterns |
| XGBoost | Gradient boosted model for improved prediction accuracy |

### 4. Evaluation
Models were evaluated using:
- **RMSE** (Root Mean Squared Error) — primary metric
- **MAE** (Mean Absolute Error)
- **R² Score** — goodness of fit
- Predicted vs Actual RUL plots per engine

---

## 📊 Results

| Model | RMSE | MAE | R² Score |
|---|---|---|---|
| Linear Regression | TBD | TBD | TBD |
| Random Forest | TBD | TBD | TBD |
| XGBoost | TBD | TBD | TBD |

*Results will be updated upon project completion.*

---

## 📈 Power BI Dashboard

The Power BI dashboard visualises:
- Engine health trends over operational cycles
- Predicted RUL per engine
- Failure risk indicators across the fleet
- Model prediction accuracy summary

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.8+ | Core programming language |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical computations |
| Scikit-learn | Machine learning models and evaluation |
| XGBoost | Gradient boosting model |
| Matplotlib / Seaborn | Data visualisation |
| Power BI | Interactive dashboard |
| Jupyter Notebook | Development environment |

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or Google Colab
- Power BI Desktop (for dashboard)

### Installation

```bash
# Clone the repository
git clone https://github.com/VidhyadharMelam/turbofan-engine-health-monitoring.git

# Navigate to project directory
cd turbofan-engine-health-monitoring

# Install required libraries
pip install -r requirements.txt
```

### Dataset Setup
1. Download the NASA C-MAPSS dataset from [Kaggle](https://www.kaggle.com/datasets/behrad3d/nasa-cmaps)
2. Place the downloaded files inside `data/raw/`
3. Run notebooks in order: 01 → 02 → 03 → 04

### Requirements
```
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
jupyter
```

---

## 🚀 How to Run

```bash
# Start Jupyter Notebook
jupyter notebook

# Open notebooks in order:
# 1. notebooks/01_EDA.ipynb
# 2. notebooks/02_preprocessing.ipynb
# 3. notebooks/03_modeling.ipynb
# 4. notebooks/04_evaluation.ipynb
```

---

## 🔑 Key Learnings

- Understanding time-series sensor data in an industrial context
- Importance of feature engineering (RUL calculation, rolling averages) in predictive maintenance
- Comparing regression models for lifecycle prediction
- Translating model outputs into business-readable dashboards

---

## 🏭 Industry Relevance

This project is directly relevant to real-world aerospace maintenance operations:

- **Honeywell Forge Performance+** uses AI/ML for predictive maintenance in MRO facilities
- **Airlines** use RUL prediction to reduce unscheduled maintenance events
- **Engine manufacturers** use sensor degradation analysis to improve engine design

---

## 📌 Project Status

🔄 **In Progress** — Notebooks and model training currently being developed. Results and dashboard will be updated upon completion.

---

## 👤 Author

**Vidhyadhar Melam**  
[LinkedIn](https://linkedin.com/in/vidhyadhar-melam) | [GitHub](https://github.com/VidhyadharMelam)  
vidhyadhar.melam@outlook.com
