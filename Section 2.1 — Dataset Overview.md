# Section 2.1 — Dataset Overview

## 🎯 Goal
Understand the raw dataset structure before analysis:
- How many rows and columns exist.
- What each column represents.
- Identify extra or empty columns.

---

## 📜 Code
```python
import pandas as pd

# Path to dataset in Google Drive
path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/raw/train_FD001.txt"

# Load dataset
train = pd.read_csv(path, sep=" ", header=None)

# Inspect first few rows
print(train.head())

# Check dataset shape (rows, columns)
print(train.shape)
📝 Explanation
sep=" " → The dataset is space-separated (not comma-separated).

header=None → No column names in the file, so we’ll assign them later.

train.head() → Displays the first 5 rows to confirm loading worked.

train.shape → Shows dataset dimensions (rows, columns).

Observation: Extra empty columns (NaN values) appear at the end (e.g., columns 26, 27). These will be dropped later.

📘 Documentation (Future Reference)
Successfully loaded raw dataset into pandas.

Verified dataset shape and inspected first few rows.

Confirmed presence of empty columns at the end.

Next step: Renaming columns to meaningful names (engine_id, cycle, setting_1–3, sensor_1–21).

📝 Output
Dataset shape: (20631, 28) → 20,631 rows and 28 columns.

Preview shows columns labeled 0–27 with numerical values.

Extra empty columns (NaN) appear at the end — will be dropped later.
