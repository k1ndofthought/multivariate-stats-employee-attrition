# Multivariate Statistical Analysis — Employee Attrition

A multivariate statistics project applying Hotelling's T², Box's M test, MANOVA, and Exploratory Factor Analysis to an employee attrition dataset, using R.

## Overview

This project explores whether employees who leave a company ("Attrition = Yes") differ systematically from those who stay, and whether tenure-related variables can be reduced to a smaller number of underlying dimensions. All analysis was done in R using the `MVN`, `ICSNP`, `heplots`, `biotools`, and `psych` packages.

**Dataset:** `employee_attrition_train.csv` — includes employee demographics, income, tenure, and department, along with an attrition flag (Yes/No).

## Methodology & Results

### 1. Multivariate Normality
Tested whether four continuous variables (`Age`, `MonthlyIncome`, `DistanceFromHome`, `TotalWorkingYears`) jointly follow a multivariate normal distribution, using the Henze-Zirkler test and Mahalanobis distances (QQ-plot check for multivariate outliers).

### 2. One-Sample Hotelling's T² Test
Tested whether the observed mean vector of the four continuous variables differs from a reference vector (μ₀ = Age 35, Income 6000, Distance 10, Working Years 10).

- **T² = 21.863, df = (4, 780), p < 2.2e-16**
- The observed mean profile is significantly different from the reference vector.

### 3. Two-Sample Hotelling's T² Test (Attrition: Yes vs. No)
Before comparing groups, **Box's M test** checked whether the two groups share equal covariance structures:

- **Box's M: χ² = 29.188, df = 10, p = 0.0012** → covariance matrices are *not* homogeneous between groups

The two-sample Hotelling's T² test then compared the overall profile (age, income, distance from home, working years) of employees who left vs. stayed:

- **T² = 8.903, df = (4, 779), p = 4.95e-07**
- Employees who left and employees who stayed have significantly different multivariate profiles.

### 4. MANOVA — Differences Across Departments
Tested whether the four continuous variables differ jointly across departments, using Wilks' Lambda:

- **Wilks' Λ = 0.979, F(8, 1556) = 2.099, p = 0.033**
- Statistically significant, but Λ close to 1 indicates the effect size is weak — departments differ only slightly on these measures.

### 5. Exploratory Factor Analysis (EFA)
Examined whether four tenure-related variables (`YearsAtCompany`, `YearsInCurrentRole`, `YearsSinceLastPromotion`, `YearsWithCurrManager`) could be reduced to a smaller number of latent factors.

- **KMO = 0.82** (sampling adequacy: very good)
- **Bartlett's test: χ² = 1835.24, df = 6, p < 0.001** (correlation structure suitable for factor analysis)
- **Eigenvalues:** 2.95, 0.56, 0.28, 0.20 → only one factor exceeds 1 (Kaiser criterion), confirmed by the scree plot
- A single-factor solution (oblimin rotation, minres estimation) explained **66.3% of total variance**, with loadings:

| Variable | Loading |
|---|---|
| YearsAtCompany | 0.926 |
| YearsInCurrentRole | 0.857 |
| YearsWithCurrManager | 0.817 |
| YearsSinceLastPromotion | 0.627 |

All four tenure variables load strongly onto a single latent factor, best interpreted as **"career experience / organizational tenure."**

## Key Takeaways

- Employees who leave the company have a significantly different demographic/tenure profile than those who stay
- Departments differ only weakly on age, income, distance, and working years
- Four separate tenure-related HR metrics can be meaningfully reduced to one underlying "tenure" construct — useful for simplifying future HR models

## Tools Used

R — `MVN`, `ICSNP` (Hotelling's T²), `heplots` / `biotools` (Box's M, MANOVA), `psych` (KMO, Bartlett's test, factor analysis), `tidyverse`

## Repository Contents

| File | Description |
|---|---|
| `multivariate_analysis.Rmd` | Full R Markdown source code |
| `multivariate_analysis.html` / `.pdf` | Knitted report with output and plots |
| `employee_attrition_train.csv` | Dataset used (if shareable / public source) |

## Notes & Limitations

- Dataset is a standard public HR attrition dataset used for educational purposes
- Box's M test result (unequal covariances) means the Hotelling's T² result should be interpreted with some caution, as the test assumes equal covariance matrices
- Findings are descriptive/exploratory and not intended as causal claims about attrition drivers

## Author

**Salih Yasin Kedir**
[LinkedIn](https://www.linkedin.com/in/k1ndofthought/) · [GitHub](https://github.com/k1ndofthought)
