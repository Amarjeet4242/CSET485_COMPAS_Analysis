# CSET485 COMPAS Analysis

## Overview

This repository contains the Jupyter Notebook for **CSET485 -- AI and
Society, Assignment 1**. The project analyzes the COMPAS recidivism
dataset and examines model predictions, subgroup relationships,
omitted-variable sensitivity, confident prediction errors, and fairness
metrics.

## Project objectives

-   Load and inspect the COMPAS dataset.
-   Preprocess selected demographic and case-related features.
-   Train and evaluate a Linear Regression model for `decile_score`.
-   Train and evaluate a Logistic Regression model for `is_recid`.
-   Compare model-based classifications and measure disagreement.
-   Examine subgroup differences in the relationship between
    `priors_count` and recidivism.
-   Compare full and reduced logistic regression models to study
    sensitivity to omitting `age`.
-   Identify confident false-positive and false-negative predictions.
-   Calculate fairness ratios across decision thresholds and visualize
    trade-offs.

## Dataset and features

The analysis uses the COMPAS dataset. The reported dataset shape is
**7,214 rows and 53 columns**.

The target variables are:

-   `decile_score`: COMPAS risk score, with values from 1 to 10.
-   `is_recid`: binary recidivism outcome, with values 0 and 1.

Selected predictors used in the analysis include `age`, `priors_count`,
`sex`, `race`, and `c_charge_degree`.

> **Data note:** Add the dataset's original source, download link, and
> any licensing or citation information required by your course. Do not
> upload restricted or sensitive data unless permitted.

## Methods

### 1. Preprocessing and model evaluation

The notebook performs data checks, prepares the selected predictors, and
uses a 70/30 train-test split with `random_state=968`. Preprocessing
should be fitted on the training set and then applied to the test set to
avoid data leakage.

### 2. Model comparison

-   **Model A --- Linear Regression:** predicts `decile_score`.
-   **Model B --- Logistic Regression:** predicts `is_recid`.

The notebook compares classifications obtained from the two approaches
and reports their disagreement.

### 3. Subgroup analysis

The analysis compares the coefficient for `priors_count` across the full
model and the African-American and Caucasian subgroup models. An
interaction model is also used to test whether the estimated association
differs between these groups.

### 4. Omitted-variable sensitivity

A full logistic regression model is compared with a reduced model that
omits `age`. Coefficient changes are reported to show sensitivity to
model specification. These changes alone do not establish a causal
effect or prove causal omitted-variable bias.

### 5. Adversarial subset

The notebook identifies confident incorrect predictions using the
specified probability cutoffs, then examines a reproducible subset of up
to 50 cases.

### 6. Fairness analysis

The notebook calculates Demographic Parity (DP), Equalized Odds (EO),
and Predictive Parity (PP) ratios across decision thresholds and
visualizes the trade-offs. The interpretation depends on the precise
metric definitions used in the assignment.

## Results reported so far

The following values were observed in the notebook outputs shared during
the analysis. Re-run the complete notebook before treating them as
final.

  Metric                                                            Reported result
  -------------------------------------------------------- ------------------------
  Dataset shape                                                          7,214 × 53
  Test-set size                                                               2,165
  Logistic Regression accuracy                                               67.48%
  Linear/Logistic classification disagreements                                  213
  Disagreement rate                                                           9.84%
  Confident incorrect predictions                            76 (3.51% of test set)
  Selected adversarial cases                                                     50
  Interaction coefficient for `priors_count` × Caucasian                   0.043638
  Interaction p-value                                                      0.008613

The notebook also contains the coefficient comparison for the full and
reduced models, the adversarial-subset analysis, and the fairness
threshold table and chart.

## Repository contents

-   `CSET485_COMPAS_Analysis.ipynb` --- main notebook containing the
    analysis, code, and outputs.
-   `README.md` --- project overview and instructions.

Additional CSV files may be included if required by the assignment, such
as the adversarial subset, fairness metrics, and verification results.

## How to run

1.  Download or clone this repository.
2.  Open `CSET485_COMPAS_Analysis.ipynb` in Jupyter Notebook,
    JupyterLab, or Google Colab.
3.  Ensure the required dataset is available at the file path used in
    the notebook.
4.  Install any missing Python packages used by the notebook, such as
    `pandas`, `numpy`, `scikit-learn`, `statsmodels`, and `matplotlib`.
5.  Restart the kernel and run all cells from top to bottom.
6.  Check that the results reproduce without errors.

The exact dataset filename and file path depend on the dataset location
configured in the notebook.

## Limitations and responsible use

This is an academic analysis of a high-stakes prediction setting.
Statistical associations do not establish causation. Accuracy alone does
not determine whether a model is fair or suitable for deployment.
Fairness metrics may conflict, and results can depend on model
specification, threshold selection, data quality, and the chosen outcome
definition. The model should not be treated as a definitive judgment
about any individual.

## Reproducibility and submission

The notebook uses `random_state=968` for the specified reproducible
split and adversarial sampling where applicable. For final submission,
restart the notebook kernel and run all cells in order, verify every
reported number, and include the repository URL in the course report.

## Author

**Student:** Amarjeet\
**Course:** CSET485 -- AI and Society\
**Assignment:** Assignment 1 --- COMPAS Analysis
