# Product Experiment: Increasing Lead Conversion in a Marketplace Funnel

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/youqingzhou/product-experiment-lead-conversion/HEAD?urlpath=%2Fdoc%2Ftree%2Flead_conversion_experiment.ipynb)

Click the Binder badge above to launch the interactive notebook and reproduce the full analysis.

---

# Overview

This project simulates a product experiment designed to improve lead conversion in a marketplace-style funnel.

The goal is to evaluate whether a product intervention (treatment) increases downstream conversions compared to the control experience.

The notebook demonstrates common workflows used by Product Data Scientists, including:

- A/B testing
- Funnel analysis
- Conversion segmentation
- Logistic regression modeling
- CUPED variance reduction
- ML-based CUPAC adjustment

---

# Experiment Design

Users are randomly assigned to two groups:

**Control**

- Baseline product experience

**Treatment**

- Product intervention designed to improve lead engagement

The simulated conversion funnel follows a typical marketplace flow:

Lead → Responded → Appointment → Closed


Each stage depends on user and lead characteristics such as:

- lead_quality
- baseline_skill
- treatment exposure

These factors influence conversion probabilities throughout the funnel.

---

# Key Results

The treatment improves conversion across the funnel:

| Metric | Control | Treatment | Uplift |
|------|------|------|------|
| Responded | 0.396 | 0.475 | +7.9 pp |
| Appointment | 0.142 | 0.197 | +5.4 pp |
| Closed | 0.030 | 0.046 | +1.5 pp |

The improvement in **closed deals** is statistically significant.

---

# Methods Demonstrated

The notebook walks through several common product analytics techniques.

## Funnel Analysis

Visualizes conversion rates at each stage of the marketplace funnel.

## Segmentation

Examines heterogeneous treatment effects across lead quality segments.

## Logistic Regression

Estimates treatment effects while controlling for lead characteristics.

## CUPED

Uses pre-period metrics to reduce variance in treatment effect estimation.

## CUPAC (ML-based adjustment)

Uses a machine learning prediction model with cross-fitting to generate covariate adjustments that further improve statistical efficiency.

---

# Running the Notebook

You can run the analysis interactively using Binder.

Click the Binder badge at the top of this page to launch an executable environment in the browser.

The notebook will open automatically and can be executed cell by cell.

---

# Repository Structure

product-experiment-lead-conversion
│
├── README.md
├── experiment_summary.md
├── requirements.txt
└── lead_conversion_experiment.ipynb

---

# Skills Demonstrated

This project demonstrates several skills commonly required for Product Data Science roles:

- Experiment design
- A/B testing analysis
- Funnel analytics
- Statistical modeling
- Variance reduction techniques
- Machine learning based adjustments
- Reproducible research with Binder

---

# Youqing Zhou

Data science portfolio project demonstrating product experimentation and causal inference techniques.
