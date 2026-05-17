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
🔹 Step 2.2 — Cell 3 (Build Column Names)
Code
python
# Build descriptive column names

# First 5 columns are identifiers and settings
base_cols = ['engine_id', 'cycle', 'setting_1', 'setting_2', 'setting_3']

# Remaining columns are sensors
# train.shape[1] gives total number of columns after dropping NaNs
# Subtract 5 because we already accounted for engine_id + cycle + 3 settings
num_sensors = train.shape[1] - 5

sensor_cols = [f'sensor_{i}' for i in range(1, num_sensors + 1)]

# Combine both lists
col_names = base_cols + sensor_cols

# Preview
print("Total columns:", len(col_names))
print("First 10 column names:", col_names[:10])
print("Last 5 column names:", col_names[-5:])
Explanation
base_cols → These are the first 5 columns:

engine_id → identifies which engine the row belongs to

cycle → the time step (row number for that engine)

setting_1–3 → operational settings

num_sensors → We calculate how many sensor columns remain after the first 5.

Example: If dataset has 26 columns total → 26 - 5 = 21 sensors.

sensor_cols → We generate names dynamically:

sensor_1, sensor_2, … sensor_21

col_names → Combine both lists into one master list of names.

Preview → We print total count, first few names, and last few names to confirm.

Expected Output
Code
Total columns: 26
First 10 column names: ['engine_id', 'cycle', 'setting_1', 'setting_2', 'setting_3', 'sensor_1', 'sensor_2', 'sensor_3', 'sensor_4', 'sensor_5']
Last 5 column names: ['sensor_17', 'sensor_18', 'sensor_19', 'sensor_20', 'sensor_21']
📘 Documentation (Future Reference)
Step 2.2 — Cell 3 (Build Column Names)

Defined first 5 columns as identifiers and settings.

Calculated number of sensors (train.shape[1] - 5).

Generated sensor names dynamically (sensor_1 … sensor_21).

Combined into one list of 26 names.

Verified by printing total count, first 10, and last 5 names.

# Verify
print(train.head())
print(train.columns)
📝 Explanation
dropna(axis=1, how='all') → removes columns that are completely empty (NaN).

First 5 names: engine_id, cycle, setting_1–3.

Remaining names: sensor_1 through sensor_21.

Assigned new names with train.columns = col_names.
🔹 Step 2.2 — Cell 4 (Assign New Names)
Code
python
# Assign the new column names we built in Cell 3
train.columns = col_names

# Verify the changes
print("✅ First 5 rows with new column names:")
print(train.head())

print("\n✅ List of all column names:")
print(train.columns.tolist())
Line‑by‑Line Explanation
train.columns = col_names

This replaces the default numeric labels (0, 1, 2, …) with the descriptive names we created (engine_id, cycle, setting_1–3, sensor_1–21).

After this line, every column in the DataFrame has a meaningful name.

train.head()

Displays the first 5 rows of the dataset.

You should now see headers like:

Code
engine_id  cycle  setting_1  setting_2  setting_3  sensor_1  sensor_2 ...
train.columns.tolist()

Prints the full list of column names as a Python list.

This is a quick way to confirm that all 26 names are present and correctly ordered.

Expected Output
First 5 rows with headers:

Code
engine_id  cycle  setting_1  setting_2  setting_3  sensor_1  sensor_2 ...
1          1      -0.0007    -0.0004    100.0      518.67    641.82 ...
Column list:

Code
['engine_id', 'cycle', 'setting_1', 'setting_2', 'setting_3',
 'sensor_1', 'sensor_2', ..., 'sensor_21']
📘 Documentation (Future Reference)
Step 2.2 — Cell 4 (Assign New Names)

Applied descriptive column names to dataset.

Verified dataset now shows meaningful headers instead of numeric labels.

Confirmed total of 26 columns:

Identifiers: engine_id, cycle

Settings: setting_1–3

Sensors: sensor_1–21

Dataset is now clean and ready for analysis.

Verified by printing first rows and column names.

📘 Documentation (Future Reference)
Dropped empty columns at the end of dataset.

Renamed columns to meaningful names:

engine_id, cycle, setting_1–3, sensor_1–21.

Verified dataset now has clear, descriptive column names.
