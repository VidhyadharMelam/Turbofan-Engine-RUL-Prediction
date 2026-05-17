📊 Exploratory Data Analysis (EDA) — Detailed Checklist
2.1 Dataset Overview
Load dataset into pandas.

Rename columns (engine_id, cycle, setting_1–3, sensor_1–21).

Check dataset size:

python
print(train.shape)   # rows, columns
print(train.head())  # first 5 rows
Why: Confirms structure and ensures data is loaded correctly.

2.2 Engine Lifecycle Exploration
Count engines:

python
print(train['engine_id'].nunique())
Max cycles per engine:

python
print(train.groupby('engine_id')['cycle'].max().head())
Why: Shows how long each engine ran before failure.

2.3 Sensor Behavior
Plot one sensor for one engine:

python
import matplotlib.pyplot as plt

engine1 = train[train['engine_id'] == 1]
plt.plot(engine1['cycle'], engine1['sensor_2'])
plt.xlabel("Cycle")
plt.ylabel("Sensor 2 Reading")
plt.title("Engine 1 - Sensor 2 Trend")
plt.show()
Plot multiple sensors together:

python
sensors_to_plot = ['sensor_2', 'sensor_3', 'sensor_7']
for sensor in sensors_to_plot:
    plt.plot(engine1['cycle'], engine1[sensor], label=sensor)
plt.legend()
plt.show()
Why: Identifies which sensors degrade over time (useful for prediction).

2.4 Statistical Summary
Basic stats:

python
print(train.describe())
Correlation matrix:

python
corr = train.corr()
plt.imshow(corr, cmap='coolwarm', interpolation='none')
plt.colorbar()
plt.title("Sensor Correlation Heatmap")
plt.show()
Why: Helps detect redundant sensors and relationships.

2.5 Sensor Variance Check
Variance per sensor:

python
variances = train.var()
print(variances)
Why: Sensors with near‑zero variance don’t add value → drop later in preprocessing.

2.6 Save EDA Outputs
Save plots into outputs/figures/.

Document findings in 01_EDA.ipynb.

Why: Recruiters see you’ve done systematic exploration.

🎯 Deliverables from EDA
Clean dataset with proper column names.

Plots showing sensor degradation trends.

Stats + correlation heatmap.

Notes on which sensors are useful vs not.
