# Raman Intensity Analysis for Arbitrary Crystal Rotation

This MATLAB project calculates and fits Raman scattering intensities for linearly polarized light in the xy-plane as a function of **crystal orientation**. It uses symbolic computations to rotate Raman tensors via **Euler angles**, and fits the resulting intensity functions to experimental Raman data.

---

## 🧪 Features

- Symbolic calculation of Raman intensities using **Jones matrix formalism**
- Support for **Z-X-Z Euler angle** rotation of tensors
- Fit symbolic Raman intensity expressions to experimental data
- Visualize angular dependence in **cartesian** or **half-polar plots**
- Flexible input for custom tensor parameters and polarization configurations

---

## ⚙️ Getting Started

### 1. Folder Structure

Ensure the following file/folder structure exists:

📂 your-project/
┣ 📂 data/
┃ ┣ 📂 Sample/                         ← Sample name (e.g., "Quartz")
┃ ┃ ┗ 📄 normalized_peak_heights.csv   ← Your Raman data
┣ 📄 raman_fit.mlx                     ← MATLAB script (one level below /data)

---

### 2. CSV File Format

The CSV file (your Raman data) must follow this structure:

- The first column must be named `theta` (in degrees).
- The remaining columns are Raman peak intensities, labeled by their corresponding **Raman shift** (in cm⁻¹).
- The first row contains headers.
- Each subsequent row corresponds to a measurement at a specific angle.
Example:

| theta | 127 cm⁻¹ | 208 cm⁻¹ | 396 cm⁻¹ | 1163 cm⁻¹ |
|-------|----------|----------|----------|-----------|
| 0     | 1.68     | 1.68     | 0.71     | 0.63      |
| 10    | 1.48     | 1.49     | 0.63     | 0.55      |
| 20    | 1.46     | 1.45     | 0.63     | 0.55      |
| 30    | 1.48     | 1.48     | 0.63     | 0.56      |
| 40    | 1.53     | 1.49     | 0.63     | 0.57      |
| 50    | 1.66     | 1.59     | 0.69     | 0.61      |


---

### 3. Configure Script

Open `raman_fit.mlx` and set your configuration:

🧭 *Rotation Angles*: If known, insert the Euler angles and phase offset for the Jones matrix.

```matlab
% Substitute known angles
J = subs(J, x, 0);       % e.g., zero phase difference
R_X = subs(R_X, Phi, 0); % e.g., crystal aligned with lab frame
R_Z2 = subs(R_Z2, phi2, 0);

🧪 *Raman Tensor*: Define the Raman tensors of your sample. For example:

  ```matlab
  syms theta phi1 Phi phi2 x a b c d real

  % Define a general 3x3 Raman tensor
  alpha = [a, 0, 0; 0, a, 0; 0, 0, b];
  E_x = [c, 0, 0; 0, -c, d; 0, d, 0];
  E_y = [0, -c, -d; -c, 0, 0; -d, 0, 0];

⚙️ *Basic Settings*: Set your sample folder and which Raman peak to analyze.

```matlab
selected_folder = "Quartz";        % Folder name under /data/
chosen_peak = 1163;                % Peak to analyze (cm⁻¹)
selected_mode = 'E';               % Mode: 'alpha' or 'E'
plot_type = "half-polar";          % 'normal' or 'half-polar'

✏️ *Parameter Initialization*: Set initial guesses and constraints for the fit parameters as needed.
(Parameters you omit will use default values.)  For example:

```matlab
custom_guesses = struct( ...
    'a', 3, ...
    'b', 6, ...
    'c', 1, ...
    'd', 1, ...
    'phi1', 0.9, ...
    'Phi', 0, ...
    'phi2', 0, ...
    'x', pi/4 ...
);

---

### 4. Run & Analyze

Run the script in MATLAB.

The script will:

- ✅ Load your data  
- 📈 Perform the nonlinear fit to your selected Raman mode  
- 📊 Plot the Raman intensity vs. rotation angle (Cartesian or half-polar)  
- 🧾 Print the optimized fit parameters (with angles shown in radians and degrees)  


