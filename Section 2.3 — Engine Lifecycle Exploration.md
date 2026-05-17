Cell 1 — Count total engines
python
# Count how many unique engines are present in the dataset
num_engines = train['engine_id'].nunique()

# Print result
print("✅ Total engines in dataset:", num_engines)
Explanation:

nunique() counts distinct values in the engine_id column.

This tells us how many engines were monitored in the FD001 dataset.

Expected output: 100 engines.

Cell 2 — Find maximum cycle per engine
python
# Group dataset by engine_id and find the maximum cycle for each engine
engine_cycles = train.groupby('engine_id')['cycle'].max()

# Print first few results
print("✅ Maximum cycle length per engine (first 5 engines):")
print(engine_cycles.head())
Explanation:

groupby('engine_id') → groups rows by each engine.

['cycle'].max() → finds the last cycle (lifespan) for each engine.

This shows how long each engine ran before failure.

Example output: Engine 1 → 192 cycles, Engine 2 → 287 cycles, etc.

Cell 3 — Summarize lifecycle statistics
python
# Summary statistics of engine lifecycles
print("✅ Lifecycle summary statistics:")
print(engine_cycles.describe())
Explanation:

describe() gives min, max, mean, and quartiles.

This helps us understand the distribution of engine lifespans.

Example output:

Min ≈ 128 cycles

Max ≈ 362 cycles

Mean ≈ 206 cycles

📘 Documentation (Future Reference)
Step 2.3 — Engine Lifecycle Exploration

Counted total number of engines → 100.

Calculated maximum cycle length for each engine.

Summarized lifecycle statistics:

Min cycle ≈ 128

Max cycle ≈ 362

Mean cycle ≈ 206

Insight: Engines fail at different cycle lengths, showing variability in lifespan.
