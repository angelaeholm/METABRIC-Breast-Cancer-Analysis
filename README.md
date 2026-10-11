# METABRIC Breast Cancer Analysis

**Exploratory Data Analysis and Bayesian Logistic Regression**

**Author:** Angela Holm

## Project Overview

This project examines the relationships between breast cancer biomarkers, patient age at diagnosis, and recorded overall survival status using clinical data from the Molecular Taxonomy of Breast Cancer International Consortium (METABRIC).

The analysis combines exploratory data analysis (EDA) with Bayesian logistic regression to investigate how estrogen receptor (ER), progesterone receptor (PR), HER2 status, and age at diagnosis are associated with recorded mortality.

The project is divided into two parts, progressing from descriptive analysis and visualization to Bayesian statistical modeling and posterior interpretation.

## Research Question

How are ER status, PR status, HER2 status, and age at diagnosis associated with recorded overall survival status among patients in the METABRIC breast cancer dataset?

## Dataset

**Source:** METABRIC Breast Cancer Clinical Dataset, accessed through [cBioPortal](https://www.cbioportal.org/).

The dataset used in this analysis contains 500 patient records and 39 clinical variables.

Five variables were selected for the study:

- `AGE_AT_DIAGNOSIS` — Patient age at diagnosis
- `ER_STATUS` — Estrogen receptor status
- `PR_STATUS` — Progesterone receptor status
- `HER2_STATUS` — HER2 receptor status
- `OS_STATUS` — Recorded overall survival status

After excluding four observations with missing values, 496 complete records were retained for Bayesian modeling.

## Part 1: Exploratory Data Analysis

The first part of the project explores the distribution of clinical variables and differences in recorded mortality across patient groups.

The analysis includes descriptive statistics, missing-value assessments, biomarker frequency distributions, cross-tabulations, and visualizations of age and survival status.

Among the 496 patients with recorded survival outcomes, 288 (58.1%) were living and 208 (41.9%) were deceased.

The exploratory analysis provides context for understanding the clinical data before developing the Bayesian model.

**View Part 1:**

[Exploratory Data Analysis — Jupyter Notebook](METABRICstudy%20P1.ipynb)

[Exploratory Data Analysis — HTML Report](METABRICstudy%20P1.html)

## Part 2: Bayesian Logistic Regression

The second part applies Bayesian logistic regression using PyMC to examine the relationships between the four predictors and recorded mortality.

Categorical biomarkers were converted to binary variables, and age at diagnosis was standardized. The dependent variable was coded as living (0) or deceased (1).

The model used Normal prior distributions for the intercept and regression coefficients and a Bernoulli likelihood for the binary outcome.

Markov Chain Monte Carlo (MCMC) sampling was performed using the No-U-Turn Sampler (NUTS), with four chains, 1,000 tuning iterations, and 2,000 posterior draws per chain.

Posterior distributions were evaluated using ArviZ summaries, 95% highest density intervals (HDIs), trace plots, convergence statistics, and posterior predictive checks.

**View Part 2:**

[Bayesian Logistic Regression — Jupyter Notebook](METABRIC%20study%20P2.ipynb)

[Bayesian Logistic Regression — HTML Report](METABRIC%20study%20P2.html)

## Key Bayesian Findings

| Predictor | Posterior Mean | 95% HDI |
|---|---:|---|
| Age at diagnosis (standardized) | 0.991 | 0.766 to 1.215 |
| ER-positive status | -0.508 | -1.070 to 0.053 |
| PR-positive status | -0.212 | -0.697 to 0.260 |
| HER2-positive status | 0.721 | 0.028 to 1.415 |

Age at diagnosis demonstrated a positive association with recorded mortality. Its 95% HDI remained entirely above zero.

HER2-positive status also showed a positive association, although the relatively wide credible interval indicated uncertainty about the magnitude of the relationship.

ER-positive and PR-positive status had negative posterior mean coefficients, suggesting potentially lower mortality odds compared with receptor-negative patients. However, their 95% HDIs included zero, indicating greater uncertainty.

The MCMC convergence diagnostics were favorable, with R-hat values of 1.00 for all reported parameters.

## Technologies and Analytical Methods

**Programming and environment:** Python, Jupyter Notebook

**Data preparation:** Pandas, NumPy

**Bayesian modeling:** PyMC, NUTS, MCMC

**Statistical diagnostics:** ArviZ, posterior distributions, 95% HDIs, trace plots, effective sample size, R-hat, posterior predictive checks

**Visualization:** Matplotlib

## Study Limitations

This analysis uses recorded overall survival status as a binary outcome rather than modeling survival time.

Differences in follow-up duration, treatment, disease stage, and other clinical factors were not incorporated into the Bayesian model.

Therefore, the results should be interpreted as statistical associations with recorded mortality, not causal relationships or time-to-event survival estimates.

## Data Source and Acknowledgment

The clinical data were obtained from the METABRIC breast cancer study available through cBioPortal.

This project is an independent educational and portfolio analysis intended to demonstrate clinical data exploration, statistical modeling, and Bayesian interpretation in healthcare analytics.
