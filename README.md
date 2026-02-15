# Statistical Parameter Estimation for NO2 Data

## Project Overview
This repository contains a Python script designed to estimate statistical parameters from an air quality dataset (specifically Nitrogen Dioxide - NO2). The script applies a unique data transformation based on a student's **Roll Number** and calculates Maximum Likelihood Estimation (MLE) parameters including Lambda ($\lambda$), Mu ($\mu$), and a constant $c$.

## Methodology

### 1. Dynamic Coefficient Calculation
To ensure unique analysis per student, two coefficients are derived from the Roll Number ($r$):
- **$a_r$ (Amplitude Factor):** calculated as $0.05 \times (r \mod 7)$
- **$b_r$ (Frequency Factor):** calculated as $0.3 \times ((r \mod 5) + 1)$

### 2. Data Preprocessing
- The script loads `data.csv` (handling `latin-1` encoding).
- It automatically detects the column containing "no2" (case-insensitive).
- Data is cleaned by coercing errors to numeric values and removing non-positive values (keeping only $x > 0$).

### 3. Data Transformation
The raw NO2 data ($x$) is transformed into a new variable ($z$) using the calculated coefficients:
$$z = x + a_r \sin(b_r \cdot x)$$

### 4. Parameter Estimation (MLE)
The script calculates the final parameters based on the statistics of the transformed data $z$:
- **$\mu_{mle}$ (Mean):** $\frac{1}{n} \sum z_i$
- **$\sigma^2_{mle}$ (Variance):** $\frac{1}{n} \sum (z_i - \mu)^2$
- **$\lambda_{mle}$ (Precision):** $\frac{1}{2\sigma^2}$
- **$c_{mle}$ (Normalization Constant):** $\sqrt{\frac{\lambda}{\pi}}$

## Requirements
* Python 3.x
* Pandas
* NumPy

Install dependencies using:
```bash
pip install pandas numpy
