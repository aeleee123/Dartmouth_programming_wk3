# Dartmouth_programming_wk3


# README — Automated Diabetes Analysis Pipeline

## 1. Project Overview

This project was developed for HSE751: Programming for Health Data Science at Dartmouth College. The objective is to execute and examine an automated data analysis pipeline using Python in Google Colab.

The analysis explores the characteristics of a diabetes dataset, evaluates relationships among clinical variables, and compares machine learning models for binary classification of diabetes outcomes. The workflow demonstrates automated preprocessing, conditional logic, model training, cross-validation, and performance evaluation.

## 2. Dataset Description

**Dataset:** `Example Dataset_Diabetes.csv`

The dataset contains 768 observations and nine variables, including eight predictors and one binary outcome.

**Predictor Variables:**
- Pregnancies
- Glucose
- D_BP (Diastolic Blood Pressure)
- Skin_Thickness
- Insulin
- BMI
- Pedigree
- Age

**Target Variable:** `Outcome`
- 0 = No Diabetes
- 1 = Diabetes

## 3. Software and Libraries

The analysis was performed in Google Colab using Python.

Major libraries include:

- `pandas` — Data manipulation and analysis
- `numpy` — Numerical operations
- `matplotlib` and `seaborn` — Data visualization
- `scipy` — Statistical analysis
- `scikit-learn` — Machine learning, preprocessing, cross-validation, and performance evaluation

Additional libraries may be required by earlier sections of the provided assignment notebook.

## 4. How to Run the Notebook

1. Open the assignment notebook in Google Colab.
2. Select **Runtime → Run all**.
3. When prompted, upload `Example Dataset_Diabetes.csv` from your computer.
4. Allow the notebook to execute the data validation, exploratory analysis, statistical analysis, and machine learning sections.
5. Review the generated tables, figures, and model performance metrics.

The modified data-loading process supports local file uploads instead of relying on a fixed Google Drive path.

## 5. Analytical Workflow

The notebook follows these major stages:

**Data Loading and Validation:** Load the dataset, inspect its dimensions and variable types, and perform validation checks.

**Exploratory Data Analysis:** Examine descriptive statistics, missing or potentially invalid values, distributions, and relationships among variables.

**Correlation Analysis:** Evaluate associations among variables using correlation methods, including Spearman correlation.

**Machine Learning:** Split the dataset into training (70%) and test (30%) sets, apply preprocessing, and train Logistic Regression and Decision Tree classifiers.

**Model Evaluation:** Assess accuracy, recall, precision, F1 score, confusion matrices, and ROC AUC.

**Model Optimization:** Use stratified cross-validation to select a Logistic Regression classification threshold and tune Decision Tree hyperparameters.

**Model Interpretation:** Visualize the tuned Decision Tree and examine feature importance.

## 6. Pipeline Modifications

Three modifications were made to improve flexibility, reproducibility, and interpretation.

### Modification 1: Flexible Data Loading

The original environment-dependent file path was replaced with a file-upload approach using `files.upload()`. This allows users to load the dataset directly into Google Colab without modifying a personal Google Drive path.

**Purpose:** Improve portability and simplify data loading across different users and environments.

### Modification 2: Reproducible Random Sampling

A fixed random state (`random_state=42`) was added to the random sampling operation.

**Purpose:** Ensure that the same sample is selected when the notebook is rerun, improving reproducibility.

### Modification 3: Configurable Correlation Threshold

A configurable threshold was introduced to identify variable pairs with Spearman correlation coefficients meeting a specified absolute-value cutoff.

**Purpose:** Allow users to adjust the strength of associations highlighted in the analysis and examine how different thresholds affect the reported variable pairs.

## 7. Key Machine Learning Results

### Logistic Regression

The Logistic Regression model achieved:

- Test accuracy: **74.46%**
- Test ROC AUC: **0.836**
- Cross-validation-selected classification threshold: **0.443**
- Training F1 at the selected threshold: **0.669**
- Test F1 at the selected threshold: **0.605**

At the selected threshold, the test confusion matrix contained 125 true negatives, 25 false positives, 35 false negatives, and 46 true positives.

### Tuned Decision Tree

The Decision Tree was optimized using five-fold stratified cross-validation and F1 scoring.

- Best mean cross-validation F1: **0.682**
- Selected maximum depth: **8**
- Selected maximum leaf nodes: **10**
- Selected minimum samples per leaf: **5**
- Selected class weight: **balanced**

The test confusion matrix contained 101 true negatives, 49 false positives, 16 false negatives, and 65 true positives.

The tuned Decision Tree achieved approximately **71.86% accuracy** and **80.25% sensitivity**, identifying more patients with diabetes than the Logistic Regression model evaluated at the selected threshold, but also producing more false positives.

## 8. Feature Importance

The tuned Decision Tree identified the following leading predictors:

| Feature | Importance |
|---|---:|
| Glucose | 46.4% |
| BMI | 26.5% |
| Age | 13.1% |
| Pedigree | 7.6% |
| Insulin | 6.3% |

Glucose, BMI, and Age collectively accounted for approximately 86% of total feature importance.

These importance values represent each feature's contribution to impurity reduction within the fitted Decision Tree and should not be interpreted as causal effects on diabetes risk.

## 9. Reproducibility

Reproducibility was supported through fixed random states, stratified data splitting, and the use of scikit-learn Pipelines.

Preprocessing operations, including median imputation and standardization, were fitted using training data only. Cross-validation procedures also fitted preprocessing independently within each training fold to reduce data leakage.

The dataset and notebook should be kept together when sharing or submitting the project. The analysis can be reproduced by uploading the dataset and executing the notebook sequentially in Google Colab.

## 10. Limitations

The dataset contains potentially invalid zero values in several clinical measurements, which require careful interpretation and handling.

Model performance was evaluated using a single held-out test set. Additional validation would be necessary before applying the models to other patient populations.

The analysis is intended for educational purposes and should not be used for clinical diagnosis or decision-making.

## 11. Conclusion

This project demonstrates how Python can automate data preparation, statistical exploration, machine learning, and model evaluation. The results highlight the importance of reproducible workflows, model-specific preprocessing, classification thresholds, and the trade-off between sensitivity and false-positive predictions.

The completed pipeline provides a foundation for understanding automated analytical decision-making in health data science.
