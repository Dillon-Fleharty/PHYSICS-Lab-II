import csv
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# Adding force measurements per distance set
force_measurements = np.array([
    [0.301, 0.304, 0.298],  # For distance 11.0
    [0.7, 0.701, 0.703],    # For distance 7.4
    [1.02, 1.03, 1.198],    # For distance 6.6
    [1.2, 1.206, 1.601],    # For distance 5.8
    [1.602, 1.598, 1.98],   # For distance 5.2
    [2.01, 2.00, 2.41],     # For distance 4.6
    [2.40, 2.405, 3.07],    # For distance 4.0
    [3.1, 3.11, 3.61],      # For distance 3.7
    [3.66, 3.59, 4.31],     # For distance 3.2
    [4.28, 4.305, 4.70],    # For distance 2.9
    [4.73, 4.69, 4.70]      # For distance 2.8 (new data)
])

distances = np.array([11.0, 7.4, 6.6, 5.8, 5.2, 4.6, 4.0, 3.7, 3.2, 2.9, 2.8])  # distance for each set

# Calculations
average_forces = np.mean(force_measurements, axis=1)
standard_deviations = np.std(force_measurements, axis=1, ddof=1)

# Define the CSV file path
csv_file_path = '../ResearchProject/Data/force_distance_data.csv'

# Writing to CSV
with open(csv_file_path, mode='w', newline='') as file:
    writer = csv.writer(file)
    # Writing the header
    writer.writerow(["Distance", "Average Force", "Standard Deviation", "Favg ± STD"])
    # Writing each row of data
    for d, avg_f, std in zip(distances, average_forces, standard_deviations):
        favg_std = f"{avg_f:.3f} ± {std:.3f}"  # Format Favg ± STD
        writer.writerow([d, avg_f, std, favg_std])

print(f"Data has been successfully written to {csv_file_path}")

# Define Coulomb's law function for fitting
def coulombs_law(d, a):
    return a / d**2

# Fitting the model
params, params_covariance = curve_fit(coulombs_law, distances, average_forces)
a_fit = params[0]

# Plotting
plt.errorbar(distances, average_forces, yerr=standard_deviations, fmt='o', label='Data with error bar')
plt.plot(distances, coulombs_law(distances, a_fit), label=f'Fit with a={a_fit:.2f}')
plt.xlabel('Distance (unit unknown)')
plt.ylabel('Force (unit unknown)')
plt.title('Coulomb’s Law Experiment Data Fit')
plt.legend()
plt.savefig('/mnt/data/coulombs_law_fit_updated.png')  # Save as PNG
plt.show()
