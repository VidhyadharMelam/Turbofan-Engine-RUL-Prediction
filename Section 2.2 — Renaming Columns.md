# Section 2.2 — Renaming Columns

## 🎯 Goal
Make dataset columns human‑readable and meaningful:
- Replace numeric labels (`0, 1, 2, …`) with descriptive names.
- Drop empty columns at the end.
- Prepare dataset for analysis with clear identifiers.

---

## 📜 Code
```python
import pandas as pd

# Reload dataset
path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/raw/train_FD001.txt"
train = pd.read_csv(path, sep=" ", header=None)

# Drop empty columns (NaN at the end)
train = train.dropna(axis=1, how='all')

# Rename columns
col_names = ['engine_id', 'cycle', 'setting_1', 'setting_2', 'setting_3'] + \
            [f'sensor_{i}' for i in range(1, train.shape[1]-4+1)]

train.columns = col_names

# Verify
print(train.head())
print(train.columns)
📝 Explanation
dropna(axis=1, how='all') → removes columns that are completely empty (NaN).

First 5 names: engine_id, cycle, setting_1–3.

Remaining names: sensor_1 through sensor_21.

Assigned new names with train.columns = col_names.

Verified by printing first rows and column names.

📘 Documentation (Future Reference)
Dropped empty columns at the end of dataset.

Renamed columns to meaningful names:

engine_id, cycle, setting_1–3, sensor_1–21.

Verified dataset now has clear, descriptive column names.
