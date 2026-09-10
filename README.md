# ml-diabetes-prediction

This repository contains a machine learning project focused on predicting the onset of diabetes based on diagnostic measurements.

## Project Overview

The goal of this project is to build and evaluate a logistic regression model to predict whether a patient has diabetes. The project covers data loading, cleaning, preprocessing, model training, evaluation, and prediction on new data.

## Dataset

The dataset used is the Pima Indians Diabetes Database, sourced from Kaggle. It contains various diagnostic measurements and a binary outcome variable indicating whether the patient has diabetes (1) or not (0).

**Features include:**
*   `Pregnancies`: Number of times pregnant
*   `Glucose`: Plasma glucose concentration a 2 hours in an oral glucose tolerance test
*   `BloodPressure`: Diastolic blood pressure (mm Hg)
*   `SkinThickness`: Triceps skin fold thickness (mm)
*   `Insulin`: 2-Hour serum insulin (mu U/ml)
*   `BMI`: Body mass index (weight in kg/(height in m)^2)
*   `DiabetesPedigreeFunction`: Diabetes pedigree function
*   `Age`: Age (years)

**Target variable:**
*   `Outcome`: Class variable (0 or 1) indicating non-diabetic or diabetic.

## Methodology

1.  **Data Loading**: The dataset is loaded using pandas from a CSV file.
2.  **Exploratory Data Analysis (EDA)**: Initial checks on data shape, head, info, and descriptive statistics are performed.
3.  **Data Cleaning**: Missing values (represented as 0s in certain columns like Glucose, BloodPressure, SkinThickness, Insulin, and BMI) are imputed using the median of their respective columns.
4.  **Data Splitting**: The dataset is split into training and testing sets (80% training, 20% testing) using `stratify=y` to maintain the proportion of `Outcome` classes.
5.  **Feature Scaling**: `StandardScaler` is applied to standardize the features, ensuring that `X_test` is transformed using the `fit_transform` parameters derived from `X_train` to prevent data leakage.
6.  **Model Training**: A Logistic Regression model is trained on the scaled training data.
7.  **Model Evaluation**: The model's performance is evaluated using:
    *   Accuracy Score
    *   Confusion Matrix
    *   Classification Report (Precision, Recall, F1-score for each class)
8.  **Prediction**: The trained model is used to make predictions on new patient data.

## Results

After data cleaning and proper scaling, the logistic regression model achieved an **accuracy of 70.78%** on the test set.

### Confusion Matrix

The confusion matrix provides a breakdown of correct and incorrect predictions:

```
[[82 18]
 [27 27]]
```
*   **True Negatives (Not Sick correctly predicted as Not Sick):** 82
*   **False Positives (Not Sick incorrectly predicted as Sick):** 18
*   **False Negatives (Sick incorrectly predicted as Not Sick):** 27
*   **True Positives (Sick correctly predicted as Sick):** 27

### Classification Report

```
              precision    recall  f1-score   support

           0       0.75      0.82      0.78       100
           1       0.60      0.50      0.55        54

    accuracy                           0.71       154
   macro avg       0.68      0.66      0.67       154
weighted avg       0.70      0.71      0.70       154
```

**Key Observations from the Classification Report:**
*   The model performs better at identifying non-diabetic individuals (Class 0) with a recall of 82% compared to diabetic individuals (Class 1) with a recall of 50%.
*   This indicates that the model has a higher tendency to miss actual diabetic cases (False Negatives), which is a critical area for improvement in a medical diagnosis context.
