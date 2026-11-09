# Predicting Differentiated Thyroid Cancer Recurrence

A machine learning project exploring whether patient demographics and clinical characteristics can help predict differentiated thyroid cancer recurrence. The analysis compares **Logistic Regression** and **Random Forest** classifiers, with particular attention to class imbalance, model evaluation, and clinical interpretation.

## Project motivation

I chose this dataset because of my interest in computational biology and healthcare data science. Predicting cancer recurrence is an important classification problem, and this project allowed me to work with both categorical and numerical clinical variables, practice data preprocessing, and evaluate machine learning models in a healthcare context.

## Research question

**Can demographic and clinical characteristics be used to predict whether a patient with differentiated thyroid cancer will experience recurrence?**

The analysis also examines recurrence rates across patient subgroups and considers the tradeoff between identifying recurrence cases (recall) and avoiding incorrect positive predictions (precision).

## Dataset

- **Name:** Differentiated Thyroid Cancer Recurrence
- **Source:** [UCI Machine Learning Repository, Dataset 915](https://archive.ics.uci.edu/dataset/915/differentiated+thyroid+cancer+recurrence)
- **Records analyzed:** 364
- **Observed recurrence rate:** 29.7%
- **Target:** Binary recurrence outcome (recurrence vs. no recurrence)
- **Example predictors:** Age, gender, smoking history, radiotherapy history, thyroid function, pathology, T/N/M staging, and risk classification

**Timing caveat:** Treatment response is excluded from the primary prediction pipeline because it may be recorded after diagnosis and could introduce information leakage. The timing of other clinical predictors, including staging and risk classification, should also be verified before claiming diagnosis-time prediction.


## Analytical workflow

1. **Import and validate data:** Check column names, missing values, duplicates, and target labels.
2. **Clean and preprocess:** Prepare numeric and categorical features; encode categories, impute missing values, and scale features where appropriate.
3. **Explore the dataset:** Review descriptive statistics, outcome balance, and recurrence rates across demographic and clinical categories.
4. **Visualize relationships:** Create stacked recurrence-outcome bar charts, a risk-by-stage heatmap, and a donut chart showing overall class distribution.
5. **Conduct inferential analysis:** Use chi-square tests with Cramér's V for categorical associations and a Mann–Whitney U test for age.
6. **Train classification models:** Compare Logistic Regression, Random Forest, and a majority-class baseline using a stratified train/test split and cross-validation.
7. **Evaluate and interpret:** Compare F1, precision, recall, ROC-AUC, and PR-AUC; examine feature importance and discuss limitations.

## Model results

**Best cross-validated model:** Random Forest, with mean F1 **0.787 ± 0.040**.

### Held-out test set

| Model | F1 | Recall | Precision | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|
| **Random Forest** | **0.778** | 0.778 | **0.778** | **0.917** | **0.869** |
| Logistic Regression | 0.759 | **0.815** | 0.710 | 0.887 | 0.839 |
| Majority-class baseline | 0.000 | 0.000 | 0.000 | 0.500 | 0.297 |

Results reflect the dataset, preprocessing pipeline, and random seeds used in the original analysis. Performance may vary if these settings are modified.

### Interpretation

Random Forest achieved the highest cross-validated F1 score and the strongest held-out F1, ROC-AUC, and PR-AUC. Logistic Regression nevertheless achieved **higher recall (0.815 versus 0.778)**, meaning it identified a greater proportion of actual recurrence cases at the evaluated decision threshold. This tradeoff matters in healthcare research, where missing a recurrence case may be more consequential than generating a false alarm. Neither model is ready for clinical decision-making.

## Modeling and Analysis Techniques

The analysis incorporates several techniques to improve reproducibility, model evaluation, and interpretability:

- **Data validation and preprocessing:** Schema validation, missing-value handling, categorical encoding, and feature scaling.
- **Leakage prevention:** Exclusion of treatment response from the primary prediction pipeline to reduce potential information leakage.
- **Statistical analysis:** Chi-square tests, Mann–Whitney U tests, and Cramér's V to examine relationships between clinical characteristics and recurrence.
- **Model evaluation:** Stratified train/test splitting, cross-validation, and comparison against a majority-class baseline.
- **Model interpretability:** Permutation importance to evaluate feature contributions.
- **Reproducibility:** Consistent random seeds and automated model performance summaries.

## How to run in Google Colab

1. Download the original dataset from the UCI Machine Learning Repository.
2. Open the project notebook in Google Colab using its GitHub URL.
3. Upload the dataset as Thyroid_Diff.csv to the Colab runtime.
4. Run the notebook cells sequentially to reproduce the analysis.

## Limitations and responsible use

- This is an observational, single-source dataset with a relatively small sample (364 records); results may not generalize to other populations.
- Potential selection bias and class imbalance can affect performance estimates.
- Some clinical variables require verification that they were available at the intended prediction time.
- Associations and feature importance are **not evidence of causation**.
- The models have **not** been externally validated or prospectively evaluated.
- Clinical application would require additional temporal verification, calibration, subgroup/fairness assessment, external validation, and clinical oversight.

**This project is educational and research-oriented, not a medical diagnostic or treatment tool.**

## Tools

Python, pandas, NumPy, matplotlib, seaborn, SciPy, scikit-learn, Jupyter Notebook, and Google Colab.

## Data attribution

Differentiated Thyroid Cancer Recurrence dataset, [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/915/differentiated+thyroid+cancer+recurrence). Please follow the dataset page's citation and licensing requirements when redistributing the data.
