2.7 — Data Normalization
We’ll normalize the selected features using Min‑Max scaling (values between 0 and 1).

Cell 1 — Import scaler
python
# Step 2.7.1 — Import MinMaxScaler
from sklearn.preprocessing import MinMaxScaler
Annotation:

MinMaxScaler rescales each feature to a range [0, 1].

This prevents sensors with large values (e.g., 9000) from dominating smaller ones (e.g., 0.03).

Cell 2 — Fit and transform features
python
# Step 2.7.2 — Apply MinMaxScaler to selected features

scaler = MinMaxScaler()

# Fit scaler on features and transform
normalized_features = scaler.fit_transform(features)

# Convert back to DataFrame for readability
features_normalized = pd.DataFrame(normalized_features, columns=features.columns)

print("Normalized dataset shape:", features_normalized.shape)
print("First 5 rows of normalized features:")
print(features_normalized.head())
Annotation:

fit_transform() learns min/max values for each column and rescales them.

Output is converted back into a DataFrame with the same column names.

Now all features lie between 0 and 1.

Cell 3 — Verify scaling
python
# Step 2.7.3 — Verify min and max values for each feature
print("Min values per feature:")
print(features_normalized.min())

print("\nMax values per feature:")
print(features_normalized.max())
Annotation:

Ensures every feature has min = 0 and max = 1.

Confirms normalization worked correctly.

Documentation (Future Reference)
Step 2.7 — Data Normalization

Imported MinMaxScaler from scikit‑learn.

Applied scaling to selected features.

Verified all features now lie between 0 and 1.

Insight: Normalization ensures fair comparison across sensors and prevents bias from large‑scale features.
