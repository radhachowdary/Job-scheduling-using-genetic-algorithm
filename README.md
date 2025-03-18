# Job-scheduling-using-genetic-algorithm
import pandas as pd
import numpy as np
data = {
    'Job ID': ['J1', 'J2', 'J3', 'J4'],
    'Processing Time': [5,2, 7, 4]
}
df = pd.DataFrame(data)
print("Raw Dataset:")
print(df)
df = df.sort_values(by='Processing Time', ascending=False).reset_index(drop=True)
print("\nPreprocessed Dataset (Sorted by Processing Time):")
print(df)
num_machines = 2
machines = [[] for _ in range(num_machines)]
machines_load = [0] * num_machines
for _, row in df.iterrows():
    job_id = row['Job ID']
    processing_time = row['Processing Time']
    min_load_index = np.argmin(machines_load)
    machines[min_load_index].append(job_id)
    machines_load[min_load_index] += processing_time
print("\nJob Assignment to Machines:")
for i, machine in enumerate(machines):
    print(f"Machine {i+1}: Jobs {machine}, Total Load: {machines_load[i]}")
makespan = max(machines_load)
print(f"\nTotal Makespan: {makespan}")
