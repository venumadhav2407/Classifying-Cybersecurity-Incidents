# Incident Triage Prediction: Machine Learning Pipeline

## Overview

This project aims to predict **Incident Grades** (True Positive, Benign Positive, False Positive) using machine learning techniques. By leveraging advanced feature engineering and classification models, the project helps in improving the efficiency of Security Operations Centers (SOCs) by automating incident triaging. 

The focus is on designing an end-to-end pipeline, including data preprocessing, feature selection, model training, evaluation, and deployment readiness.

---

## Goals and Objectives

- **Automate Incident Triage**: Predict `IncidentGrade` with high accuracy.
- **Handle Imbalanced Data**: Ensure the model performs consistently across all classes.
- **Explainability**: Identify significant features impacting the predictions.
- **Efficiency**: Optimize the pipeline for real-world SOC integrations.

---

## Project Pipeline

### 1. **Data Exploration and Understanding**
- Loaded the **train.csv** dataset with over 9 million records.
- Analyzed data types, distributions, and target class (IncidentGrade).
- Key Observations:
  - Dataset contains mixed data types (numerical, categorical, and timestamps).
  - Target variable `IncidentGrade` has three classes: True Positive (TP), Benign Positive (BP), and False Positive (FP).
  - Minor class imbalance was identified but not severe.

### 2. **Data Preprocessing**
- **Handling Missing Values**: 
  - Imputed or dropped missing values where appropriate.
- **Encoding Categorical Features**: 
  - Label encoding for categorical variables like `AccountSid`, `AlertId`, etc.
- **Feature Engineering**:
  - Derived time-based features: `Year`, `Month`, `Day`, `Time_in_seconds`.
  - Normalized numerical columns for better model performance.
- **Train-Validation Split**:
  - Stratified splitting was used to ensure class distribution consistency.

### 3. **Feature Selection**
- Calculated **Mutual Information (MI)** scores for feature importance.
  - Top features include `AlertId`, `IncidentId`, `OrgId`, `AlertTitle`, and `DetectorId`.
- Dropped less important features to optimize the model’s complexity and performance.

### 4. **Model Training**
- **Baseline Model**: 
  - Started with Logistic Regression to establish a baseline.
- **Advanced Model**:
  - Trained a Random Forest Classifier after tuning hyperparameters using grid search.
  - Chosen for its robustness, interpretability, and feature importance analysis.
- **Cross-Validation**:
  - Implemented k-fold cross-validation to ensure consistent performance and avoid overfitting.

### 5. **Model Evaluation**
- Evaluated model performance using key metrics:
  - **Accuracy**: 98% (Validation) and 91.4% (Test Data)
  - **Precision, Recall, and Macro F1**: Balanced performance across all classes.
- **Confusion Matrix Analysis**:
  - Identified and analyzed common misclassifications for further optimization.

### 6. **Test Dataset Evaluation**
- Model tested on unseen `test.csv` dataset.
- Achieved the following metrics:
  - Accuracy: **91.42%**
  - Precision: **91.10%**
  - Recall: **90.53%**
  - Macro F1 Score: **90.80%**

---

## Results

### **Key Metrics**

| Metric         | Validation Dataset | Test Dataset |
|----------------|--------------------|--------------|
| **Accuracy**   | 98.1%             | 91.42%       |
| **Precision**  | 98.0%             | 91.10%       |
| **Recall**     | 98.0%             | 90.53%       |
| **Macro F1**   | 98.0%             | 90.80%       |

### **Confusion Matrix**

| Predicted\Actual | TP (0)   | BP (1)   | FP (2)   |
|------------------|----------|----------|----------|
| **TP (0)**       | 609,430  | 3,931    | 3,071    |
| **BP (1)**       | 7,798    | 293,677  | 3,260    |
| **FP (2)**       | 8,168    | 3,657    | 486,801  |

---

## Setup Instructions

### 1. **Environment Setup**
- Install the required Python libraries:
  ```bash
  pip install pandas numpy scikit-learn matplotlib seaborn
