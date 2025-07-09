# Student Performance Prediction using ML (Logistic Regression, Random Forest, SMOTE)
Overview
This project uses machine learning to predict student academic performance based on personal, social, and academic attributes. The dataset was taken from the UCI Machine Learning Repository and includes detailed student data from Portuguese secondary schools.

The goal was to:

Predict final student performance (grades) as a multi-class classification task

Compare results across Logistic Regression and Random Forest

Handle class imbalance using SMOTE

Improve model performance by grading final scores (G3) into 5 performance categories

I separated the grades into categories of 0 (fail), 1 , 2 , 3 , 4.
where 
0 -> 0 to 9
1 -> 10 to 11
2 -> 12 to 14
3 -> 15 to 17
4 -> 18 to 20

Dataset

source : [UCI DATASET](https://archive.ics.uci.edu/ml/datasets/student+performance)


The dataset includes 33 features such as:

Demographics: age, gender, parental education

Study behavior: study time, failures, past grades (G1, G2)

Social: going out, internet access, romantic relationship

Support: school/family support, paid classes



Problem Statement

Original target: G3 (final grade) → a numeric score from 0 to 20

Transformed into 5 performance categories (G3_category):

0: Very Poor

1: Poor

2: Average

3: Good

4: Excellent

This made it a multi-class classification problem with imbalanced target classes.



Models Used

Logistic Regression

Random Forest Classifier

I applied:

Preprocessing using ColumnTransformer

Feature scaling for numerical columns

One-hot encoding for categorical columns

SMOTE (Synthetic Minority Oversampling Technique) on the training set for combacting low recall value for grade "4" due to fewer examples.


Pipeline Setups:

before I was using sklearn.pipeline but we can't use smot inbetween steps and i was preprocessing in the pipeline so i switched to pipeline from imblearn.pipeline


the model results and accuracy improved drastically when i divided g3 into grades or categories 



Results Summary

Model	Accuracy

Logistic Regression ->	0.30

poor performance , maybe the data didnt had much linear relationship so i switched to randomforest


Random Forest	-> 0.43	
Better generalization but poor recall on minority classes


RF + G3 Category Conversion	-> 0.78	
Major boost after transforming target into categories or grades


RF + G3 Category + SMOTE	0.81	
Best performance — improved recall and balance


Key Features
Top features impacting student performance included:

G1, G2 (past grades)

absences

goout, age, health

Parental education levels


Author

Priyansh Khare
B.Tech Ece undergraduate at IIITDM Jabalpur
GitHub : https://github.com/pryanz


References
UCI Machine Learning Repository

Scikit-learn documentation

Imbalanced-learn (SMOTE)

Thank You !!