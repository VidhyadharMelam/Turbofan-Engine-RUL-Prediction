# Turbofan Engine Health Monitoring — Section 3: Preprocessing

## 3.1 Goal
Prepare the raw dataset for machine learning by:
- Creating the **Remaining Useful Life (RUL)** target column.
- Normalizing sensor values.
- Removing non-informative sensors.
- Smoothing noisy signals.
- Splitting into training and test sets.
- Saving processed data for modeling.

---

## 3.2 Create RUL Column
For each engine:
- Find the maximum cycle number.
- Subtract current cycle from max cycle → gives Remaining Useful Life.

```python
# Calculate RUL
rul = train.groupby('engine_id')['cycle'].max().reset_index()
rul.columns = ['engine_id', 'max_cycle']

train = train.merge(rul, on='engine_id', how='left')
train['RUL'] = train['max_cycle'] - train['cycle']

print(train[['engine_id','cycle','RUL']].head())
3.3 Normalize Sensor Values
Use Min-Max scaling to bring sensor values into a consistent range (0–1).

python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
sensor_cols = [col for col in train.columns if 'sensor_' in col]

train[sensor_cols] = scaler.fit_transform(train[sensor_cols])
3.4 Remove Low-Variance Sensors
Drop sensors that don’t change much (flat lines).

python
low_variance = train[sensor_cols].var()[train[sensor_cols].var() < 1e-5].index
train = train.drop(columns=low_variance)
print("Dropped sensors:", list(low_variance))
3.5 Smooth Signals (Rolling Average)
Apply rolling window averages to reduce noise.

python
for col in sensor_cols:
    train[col] = train[col].rolling(window=5, min_periods=1).mean()
3.6 Train-Test Split
Split dataset into training and test sets.

python
from sklearn.model_selection import train_test_split

X = train.drop(columns=['RUL','max_cycle'])
y = train['RUL']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print(X_train.shape, X_test.shape)
3.7 Save Processed Data
Save cleaned dataset for modeling.

python
train.to_csv("/content/drive/MyDrive/turbofan-engine-health-monitoring/data/processed/train_processed.csv", index=False)
🎯 Deliverables (Section 3)
Notebook 02_preprocessing.ipynb with:

RUL column creation.

Normalized sensor values.

Dropped low-variance sensors.

Smoothed signals.

Train-test split.

Processed dataset saved in data/processed/.
