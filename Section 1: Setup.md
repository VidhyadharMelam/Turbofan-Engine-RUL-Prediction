# Turbofan Engine Health Monitoring — Section 1: Setup

## 1.1 Folder Structure
Create the following directories:
turbofan-engine-health-monitoring/
│
├── data/
│   ├── raw/          ← raw dataset files
│   └── processed/    ← cleaned/preprocessed files
│
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_evaluation.ipynb
│
├── src/
│   ├── preprocess.py
│   └── model.py
│
├── outputs/
│   ├── figures/
│   └── models/
│
├── dashboard/
│   └── rul_dashboard.pbix
│
├── requirements.txt
└── README.md

Code

---

## 1.2 Environment Setup
- Install Python 3.8+  
- Use **Google Colab** for development (no local installation needed).  
- Mount Google Drive in Colab for permanent dataset storage:
  ```python
  from google.colab import drive
  drive.mount('/content/drive')
1.3 Dataset
Download NASA C-MAPSS FD001 dataset from Kaggle.

Place files (train_FD001.txt, test_FD001.txt, RUL_FD001.txt) into data/raw/.

Verify dataset is accessible in Colab:

python
!ls /content/drive/MyDrive/turbofan-engine-health-monitoring/data/raw
1.4 Requirements File
Create requirements.txt with the following dependencies:

Code
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
jupyter
🎯 Deliverables (Section 1)
Clean repo structure created.

Dataset downloaded and stored in Google Drive (data/raw).

Requirements file ready for installation.

Initial commit to GitHub with README + structure.
