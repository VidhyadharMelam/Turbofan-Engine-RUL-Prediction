🔹 Step 2.5 — Correlation Analysis
We’ll do this step by step with annotated code cells.

Cell 1 — Compute correlation matrix
python
# Step 2.5.1 — Compute correlation matrix for all numeric columns

corr_matrix = train.corr()

print("✅ Correlation matrix shape:", corr_matrix.shape)
print("✅ Preview of correlation matrix:")
print(corr_matrix.head())
Annotation:

train.corr() computes pairwise correlation between all numeric columns.

Values range from -1 (perfect negative correlation) to +1 (perfect positive correlation).

This matrix helps us see which sensors/settings move together.

Cell 2 — Visualize correlation matrix
python
import seaborn as sns
import matplotlib.pyplot as plt

# Step 2.5.2 — Plot heatmap of correlation matrix
plt.figure(figsize=(14,10))
sns.heatmap(corr_matrix, cmap="coolwarm", center=0)
plt.title("Correlation Heatmap of Sensors and Settings")
plt.show()
Annotation:

Heatmap shows correlations visually.

Red = strong positive correlation, Blue = strong negative correlation.

Helps identify clusters of sensors that behave similarly.

Cell 3 — Identify highly correlated sensors
python
# Step 2.5.3 — Find pairs of sensors with correlation > 0.9
high_corr = []

for i in range(len(corr_matrix.columns)):
    for j in range(i):
        if abs(corr_matrix.iloc[i, j]) > 0.9:
            high_corr.append((corr_matrix.columns[i], corr_matrix.columns[j], corr_matrix.iloc[i, j]))

print("✅ Highly correlated sensor pairs (|corr| > 0.9):")
for pair in high_corr:
    print(pair)
Annotation:

Loops through correlation matrix.

Collects pairs with correlation magnitude > 0.9.

These sensors may be redundant (carry similar information).

Example: sensor_2 and sensor_3 might be highly correlated.

📘 Documentation (Future Reference)
Step 2.5 — Correlation Analysis

Computed correlation matrix for all numeric columns.

Visualized correlations using heatmap.

Identified sensor pairs with strong correlation (|corr| > 0.9).

Insight: Highly correlated sensors may be redundant; selecting a subset can reduce dimensionality.
