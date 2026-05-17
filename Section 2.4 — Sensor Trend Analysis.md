🔹 Step 2.4 — Sensor Trend Analysis
We’ll do this step by step with annotated code cells.

Cell 1 — Select a sample engine
python
# Step 2.4.1 — Select one engine to analyze sensor trends
sample_engine = train[train['engine_id'] == 1]

print("✅ Sample engine shape:", sample_engine.shape)
print("✅ First 5 rows of sample engine:")
print(sample_engine.head())
Annotation:

We filter dataset for engine_id == 1.

This gives us all cycles for Engine 1.

We’ll use this subset to visualize sensor trends.

Cell 2 — Plot sensor trends
python
import matplotlib.pyplot as plt

# Step 2.4.2 — Plot selected sensors over cycles
plt.figure(figsize=(12,6))

# Example: plot sensor_2 and sensor_3
plt.plot(sample_engine['cycle'], sample_engine['sensor_2'], label='Sensor 2')
plt.plot(sample_engine['cycle'], sample_engine['sensor_3'], label='Sensor 3')

plt.xlabel("Cycle")
plt.ylabel("Sensor Reading")
plt.title("Sensor Trends for Engine 1")
plt.legend()
plt.show()
Annotation:

We plot sensor values against cycle number.

This shows how readings evolve as the engine approaches failure.

Some sensors remain stable, while others drift over time.

Cell 3 — Generalize for multiple sensors
python
# Step 2.4.3 — Plot multiple sensors to compare trends
plt.figure(figsize=(14,8))

for sensor in ['sensor_2', 'sensor_3', 'sensor_4', 'sensor_7']:
    plt.plot(sample_engine['cycle'], sample_engine[sensor], label=sensor)

plt.xlabel("Cycle")
plt.ylabel("Sensor Reading")
plt.title("Selected Sensor Trends for Engine 1")
plt.legend()
plt.show()
Annotation:

We loop through a list of sensors and plot them together.

This helps identify which sensors show degradation patterns.

Example: Some sensors may increase steadily, others fluctuate.

📘 Documentation (Future Reference)
Step 2.4 — Sensor Trend Analysis

Selected one engine (engine_id = 1) for trend analysis.

Plotted sensor values against cycles to visualize degradation.

Observed that some sensors remain stable, while others drift over time.

Insight: Identifying sensors with strong degradation trends is key for Remaining Useful Life (RUL) prediction.
