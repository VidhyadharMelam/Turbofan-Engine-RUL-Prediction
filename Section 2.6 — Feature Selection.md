2.6 — Feature Selection
We’ll do this step by step with annotated code cells.

Cell 1 — Remove non‑informative columns
python
# Step 2.6.1 — Drop identifiers that are not predictive features
# 'engine_id' is just an identifier, not useful for prediction
# 'cycle' will be used later for time-series modeling, but not as a direct feature here

features = train.drop(columns=['engine_id'])
print("Shape after dropping identifiers:", features.shape)
Annotation:

engine_id is an identifier, not a predictive variable.

cycle is temporal, used later in modeling, but not treated as a static feature.

This leaves us with settings and sensors.

Cell 2 — Check variance of features
python
# Step 2.6.2 — Remove features with zero or near-zero variance
low_variance = features.var()[features.var() == 0].index.tolist()

print("Features with zero variance:", low_variance)

# Drop them
features = features.drop(columns=low_variance)
print("Shape after dropping low-variance features:", features.shape)
Annotation:

Features with no variation across cycles provide no predictive power.

Example: some sensors may remain constant at 100.0 for all rows.

We drop those to reduce dimensionality.

Cell 3 — Correlation-based feature reduction
python
# Step 2.6.3 — Drop one of each pair of highly correlated features
corr_matrix = features.corr().abs()

# Select upper triangle of correlation matrix
upper = corr_matrix.where(np.triu(np.ones(corr_matrix.shape), k=1).astype(bool))

# Find columns with correlation > 0.95
to_drop = [column for column in upper.columns if any(upper[column] > 0.95)]

print("Features to drop due to high correlation:", to_drop)

# Drop them
features = features.drop(columns=to_drop)
print("Final shape after correlation-based reduction:", features.shape)
Annotation:

We compute absolute correlation values.

If two features are >0.95 correlated, they carry redundant information.

We drop one of them to simplify the dataset.

Cell 4 — Final feature list
python
# Step 2.6.4 — Print final selected features
print("Final selected features:")
print(features.columns.tolist())
Annotation:

This gives the cleaned list of features.

Typically, you’ll end up with ~15–18 sensors plus the 3 settings.

These are the most informative features for RUL prediction.

Documentation (Future Reference)
Step 2.6 — Feature Selection

Dropped non‑informative identifiers (engine_id).

Removed low‑variance features (constant sensors).

Reduced redundancy by dropping highly correlated features (|corr| > 0.95).

Final feature set includes operational settings and selected sensors.

Insight: This streamlined feature set improves model efficiency and avoids overfitting.
