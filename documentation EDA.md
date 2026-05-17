🔹 Step 2.1 — Dataset Overview
What we’re doing:
Before analyzing, we need to understand the dataset’s structure:

How many rows and columns it has.

What each column represents.

Whether there are extra or empty columns.

This step ensures we know exactly what data we’re working with.

Code
python
import pandas as pd

# Path to dataset in Google Drive
path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/raw/train_FD001.txt"

# Load dataset
train = pd.read_csv(path, sep=" ", header=None)

# Inspect first few rows
print(train.head())

# Check dataset shape (rows, columns)
print(train.shape)
Explanation
sep=" " → The dataset is space-separated, not comma-separated.

header=None → The file doesn’t have column names, so we’ll assign them ourselves later.

train.head() → Shows the first 5 rows to confirm loading worked.

train.shape → Tells us how many rows (observations) and columns (features) exist.

You’ll notice some NaN columns at the end (like 26, 27 in your screenshot). These are empty and will be dropped later.

Documentation (for future reference)
Step 2.1 — Dataset Overview

Loaded raw dataset into pandas.

Verified dataset shape and inspected first few rows.

Confirmed presence of empty columns at the end.

Next step will be renaming columns to meaningful names (engine_id, cycle, setting_1–3, sensor_1–21).
