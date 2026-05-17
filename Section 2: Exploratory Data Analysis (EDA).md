2. Exploratory Data Analysis (EDA)
2.1 Dataset Overview
Load dataset into pandas:

python
import pandas as pd
path = "/content/drive/MyDrive/turbofan-engine-health-monitoring/data/raw/train_FD001.txt"
train = pd.read_csv(path, sep=" ", header=None)
Drop empty columns and rename:

python
train = train.drop(train.columns[[26, 27]], axis=1)
col_names = ['engine_id', 'cycle',
             'setting_1', 'setting_2', 'setting_3'] + \
            [f'sensor_{i}' for i in range(1, 22)]
train.columns = col_names
2.2 Engine Lifecycle Exploration
Number of engines:

python
train['engine_id'].nunique()
Max cycles per engine:

python
train.groupby('engine_id')['cycle'].max().head()
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
Plot multiple sensors:

python
sensors_to_plot = ['sensor_2', 'sensor_3', 'sensor_7']
for sensor in sensors_to_plot:
    plt.plot(engine1['cycle'], engine1[sensor], label=sensor)
plt.legend()
plt.show()
2.4 Statistical Summary
Basic stats:

python
train.describe()
Correlation heatmap:

python
corr = train.corr()
plt.imshow(corr, cmap='coolwarm', interpolation='none')
plt.colorbar()
plt.title("Sensor Correlation Heatmap")
plt.show()
2.5 Sensor Variance Check
Variance per sensor:

python
variances = train.var()
print(variances)
2.6 Save EDA Outputs
Save plots into outputs/figures/.

Document findings in 01_EDA.ipynb.

🎯 Deliverables (Sections 1 & 2)
Clean repo structure with dataset loaded.

Dataset renamed with meaningful columns.

EDA notebook (01_EDA.ipynb) containing:

Engine lifecycle exploration.

Sensor trend plots.

Statistical summaries.

Correlation heatmap.

Variance analysis.
