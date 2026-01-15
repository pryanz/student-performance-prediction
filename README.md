# Student Performance Prediction

## Overview
This project leverages machine learning to predict student academic performance based on personal, social, and academic attributes. Using data from the UCI Machine Learning Repository (Portuguese secondary schools), the model forecasts final grades through multi-class classification.

The project explores various algorithms and optimization techniques, culminating in a **Random Forest model with SMOTE** that achieves **81% accuracy**.

## Problem Statement & Objective
The original dataset predicts a numeric final grade ($G3$) ranging from 0 to 20. To create a more actionable classification tool, this project:
1.  **Transformed targets:** Converted continuous scores into 5 distinct performance categories.
2.  **Addressed imbalance:** Utilized Synthetic Minority Oversampling Technique (SMOTE) to handle underrepresented grade classes.
3.  **Pipeline Optimization:** Solved pipeline compatibility issues by migrating from `sklearn.pipeline` to `imblearn.pipeline` to correctly integrate resampling steps.

### Target Class Transformation
The final grade ($G3$) was binned into the following categories:

| Category | Label | Score Range | Performance |
| :--- | :--- | :--- | :--- |
| **0** | Very Poor | 0 - 9 | Fail |
| **1** | Poor | 10 - 11 | Borderline |
| **2** | Average | 12 - 14 | Satisfactory |
| **3** | Good | 15 - 17 | Good |
| **4** | Excellent | 18 - 20 | Distinction |

## Dataset
**Source:** UCI Machine Learning Repository
The dataset contains 33 features covering:
* **Demographics:** Age, gender, parental education levels.
* **Study Behavior:** Weekly study time, past class failures, previous grades ($G1$, $G2$).
* **Social Factors:** Frequency of going out, alcohol consumption, romantic relationships, internet access.
* **Support Systems:** Family educational support, extra paid classes.

## Methodology
### 1. Preprocessing
* **ColumnTransformer:** Applied specific transformations to different data types.
* **Numerical Features:** Standardized using Feature Scaling.
* **Categorical Features:** Transformed using One-Hot Encoding.

### 2. Handling Imbalance
The dataset suffered from a low recall value for the highest grade category ("4") due to fewer examples. **SMOTE** was applied strictly within the training folds to generate synthetic samples for minority classes without leaking information to the test set.

*Technical Note:* Switched from `sklearn.pipeline` to `imblearn.pipeline` to enable resampling (SMOTE) as a step within the cross-validation workflow.

### 3. Models Evaluated
* **Logistic Regression:** Baseline linear model.
* **Random Forest Classifier:** Ensemble method to capture non-linear relationships.

## Results
The performance improved significantly through iterative optimization:

| Experiment Configuration | Accuracy | Observation |
| :--- | :--- | :--- |
| **Logistic Regression (Baseline)** | 30% | Poor performance due to non-linear data relationships. |
| **Random Forest (Raw Targets)** | 43% | Better generalization but struggled with raw numeric targets. |
| **Random Forest + Category Binning** | **78%** | Major improvement after converting regression to classification. |
| **Random Forest + Binning + SMOTE** | **81%** | **Best Model.** Improved recall on minority classes (Grade 4). |

## Key Features
Feature importance analysis revealed the top factors influencing student performance:
1.  **Past Grades (G1, G2):** The strongest predictors of final success.
2.  **Absences:** High correlation with lower performance.
3.  **Go Out:** Frequency of going out with friends.
4.  **Parental Education:** Mother's and Father's education levels.
5.  **Age & Health:** Demographic factors.

## Tech Stack
* **Language:** Python
* **Libraries:** Scikit-learn, Pandas, NumPy, Imbalanced-learn (SMOTE)
* **Tools:** Jupyter Notebook

## Author
**Priyansh Khare**
B.Tech CSE Undergraduate, IIITDM Jabalpur
[GitHub Profile](https://github.com/pryanz)
