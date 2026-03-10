# Experiment Summary: Increasing Lead Conversion

## Problem

In marketplace platforms, improving lead conversion is a key lever for increasing revenue and marketplace efficiency.

This project simulates a product experiment designed to test whether a behavioral product intervention can improve conversion rates in a lead funnel.

The experiment evaluates the causal impact of the treatment on downstream outcomes, including:

- Response rate
- Appointment rate
- Closed deals

---

# Experiment Design

Users (leads) are randomly assigned to one of two groups:

Control group  
Baseline product experience.

Treatment group  
A product intervention intended to increase engagement and conversion.

Randomization ensures unbiased estimation of the treatment effect.

The simulated marketplace funnel follows:

Lead → Responded → Appointment → Closed


Each stage depends on user characteristics and treatment exposure.

---

# Data Generating Process (DGP)

Conversion probabilities are generated using logistic models.

For example, the probability of a lead responding is modeled as:

```math
P(\mathrm{responded}_i = 1) =
\sigma(\beta_0 + \beta_1 \cdot \mathrm{lead\_quality}_i + \beta_2 \cdot \mathrm{treatment}_i)
```

where

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

is the logistic function.

Later funnel stages depend on earlier outcomes. For example:

```math
P(\mathrm{appointment}_i = 1) =
\sigma(\alpha_0 + \alpha_1 \cdot \mathrm{lead\_quality}_i + \alpha_2 \cdot \mathrm{baseline\_skill}_i + \alpha_3 \cdot \mathrm{treatment}_i)
```

conditional on the lead having responded.

This structure mimics common marketplace conversion pipelines.

---

# Power Analysis

Before running large-scale experiments, teams typically estimate the required sample size to ensure sufficient statistical power.

Given a baseline close rate of 3.0% and an expected treatment uplift to 4.5%, we compute the minimum sample size required to detect this effect with:

- significance level α = 0.05  
- power = 0.80  

The required sample size can be approximated using the standard two-proportion power calculation:

$$
n = \frac{(z_{1-\alpha/2}+z_{1-\beta})^2(p_1(1-p_1)+p_2(1-p_2))}{(p_2-p_1)^2}
$$

This step mirrors the planning stage of real-world experimentation platforms where teams estimate traffic requirements before launching experiments.

---

# Estimating Treatment Effects

The primary metric of interest is the treatment effect on **closed deals**.

The naïve estimator is the difference in means:

$$
\hat{\tau} =
\bar{Y}_{treatment} - \bar{Y}_{control}
$$

where

- \(Y\) is the outcome (closed deal)
- \(\bar{Y}\) is the sample mean

Statistical significance is evaluated using standard hypothesis tests.

---

# Variance Reduction

To improve statistical efficiency, the analysis demonstrates two variance reduction techniques.

## CUPED

CUPED (Controlled Experiments Using Pre-Experiment Data) reduces estimator variance using pre-period metrics.

The adjusted outcome is:

$$
Y_i^{CUPED} =
Y_i - \theta (X_i - \bar{X})
$$

where

- \(X_i\) is a pre-period metric
- \(\theta = \frac{Cov(Y, X)}{Var(X)}\)

This adjustment reduces noise while preserving unbiased treatment effect estimation.

---

## CUPAC (ML-based Adjustment)

CUPAC extends the CUPED idea using machine learning predictions.

First, a predictive model estimates:

$$
\hat{Y}_i = f(X_i)
$$

where \(f(\cdot)\) is a trained model (logistic regression in this case).

Cross-fitting is used to prevent overfitting bias.

The adjusted outcome becomes:

$$
Y_i^{adj} =
Y_i - \theta (\hat{Y}_i - \overline{\hat{Y}})
$$

This approach can substantially reduce variance in large-scale experiments.

---

# Key Results

The treatment improves conversion across the funnel.

| Metric | Control | Treatment | Uplift |
|------|------|------|------|
| Responded | 0.396 | 0.475 | +7.9 pp |
| Appointment | 0.142 | 0.197 | +5.4 pp |
| Closed | 0.030 | 0.046 | +1.5 pp |

The increase in closed deals is statistically significant.

Variance reduction techniques further improve estimation precision.

---

# Interpretation

The simulated results suggest that the treatment meaningfully improves lead engagement and downstream conversions.

In a real marketplace platform, this type of improvement could translate to:

- increased transactions
- improved marketplace liquidity
- higher platform revenue

The experiment demonstrates how product data scientists can combine experimentation, modeling, and variance reduction techniques to make more efficient product decisions.

---

# Reproducibility

The full analysis can be reproduced using the interactive notebook in this repository:

lead_conversion_experiment.ipynb

The notebook can also be executed directly in the browser using Binder.
