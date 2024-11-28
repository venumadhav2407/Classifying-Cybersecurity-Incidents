# Incident Triage Prediction: Machine Learning Pipeline


## Project Overview
This project aims to predict **incident triage grades** (`True Positive (TP)`, `Benign Positive (BP)`, and `False Positive (FP)`) using hierarchical security data. The dataset comprises evidence, alerts, and incidents with historical customer annotations. The goal is to build an efficient and interpretable machine learning model to aid in security operations center (SOC) workflows.

## Dataset Details
The dataset has three hierarchies:
1. **Evidence:** Metadata-level details such as IP addresses, email, and user data.
2. **Alert:** Consolidates multiple pieces of evidence into broader categories.
3. **Incident:** Represents a collection of alerts as a single cohesive threat narrative.

---

## Goals and Objectives

- **Automate Incident Triage**: Predict `IncidentGrade` with high accuracy.
- **Handle Imbalanced Data**: Ensure the model performs consistently across all classes.
- **Explainability**: Identify significant features impacting the predictions.
- **Efficiency**: Optimize the pipeline for real-world SOC integrations.

---

### Steps Executed

#### **1. Data Exploration and Understanding**
- **Dataset Structure**: The train dataset contains approximately 9 million rows and multiple features, with the target variable being `IncidentGrade`.
- **Target Variable Classes**: The dataset includes three target classes:
  - **True Positive (TP)**
  - **Benign Positive (BP)**
  - **False Positive (FP)**
- **Class Imbalance**: Some degree of imbalance was observed among the classes, which was considered during modeling.

#### **2. Feature Selection**
- **Mutual Information (MI) Scores**: 
  - Used the `mutual_info_classif` method to calculate the MI score for each feature concerning the target variable (`IncidentGrade`).
  - Top features were selected based on their MI scores, such as `AlertId`, `IncidentId`, `OrgId`, `AlertTitle`, and `DetectorId`.

#### **3. Data Preprocessing**
- **Handling Categorical Features**: 
  - Categorical variables were encoded using appropriate techniques (e.g., Label Encoding) to make them suitable for machine learning models.
- **Feature Engineering**: 
  - Created meaningful features, such as `Time_in_seconds`, `Year`, `Month`, and `Day`, from timestamps to capture temporal patterns.
- **Train-Test Split**: 
  - Stratified splitting was performed on the train dataset to ensure similar class distribution across training and validation sets.

#### **4. Model Training**
- **Random Forest Classifier**:
  - Trained a Random Forest model, which is robust for both classification and feature importance analysis.
  - Used hyperparameter tuning (e.g., number of trees, depth) to optimize performance.
- **Cross-Validation**:
  - Employed cross-validation to validate model performance and reduce overfitting risks.

#### **5. Model Evaluation**
- **Evaluation Metrics**:
  - Metrics used to evaluate model performance: 
    - **Accuracy**
    - **Precision**
    - **Recall**
    - **F1-score (Macro)**: Macro-averaging was applied to balance the importance of all classes, especially in the presence of imbalanced data.
- **Confusion Matrix**:
  - Analyzed the confusion matrix to understand true positives, false positives, and false negatives for each class.
  - Most predictions were accurate, with very few misclassifications.

#### **6. Testing on Unseen Data**
- Evaluated the trained Random Forest model on the test dataset (`test.csv`).
- **Test Results**:
  - **Accuracy**: 91.42%
  - **Precision**: 91.10%
  - **Recall**: 90.53%
  - **Macro F1 Score**: 90.80%

---

### Key Findings
- **Feature Importance**:
  - Features like `AlertId`, `IncidentId`, and `OrgId` showed the highest importance, indicating their strong influence in predicting `IncidentGrade`.
- **Class Imbalance**:
  - The model performed well despite minor imbalances, as evidenced by high precision and recall scores across all classes.
- **Model Robustness**:
  - The Random Forest model was chosen for its ability to handle both categorical and numerical data and its interpretability through feature importance.

---

## Train and Test Results

### Train Results
| Metric      | Score     |
|-------------|-----------|
| **Accuracy**   | 98.0%    |
| **Precision**  | 98.0%    |
| **Recall**     | 98.0%    |
| **Macro F1**   | 98.0%    |

### Test Results
| Metric      | Score     |
|-------------|-----------|
| **Accuracy**   | 91.42%   |
| **Precision**  | 91.10%   |
| **Recall**     | 90.53%   |
| **Macro F1**   | 90.80%   |

### Confusion Matrix - Test Data
| **Actual \ Predicted** | **0**        | **1**        | **2**        |
|-------------------------|--------------|--------------|--------------|
| **0 (TP)**             | 609430       | 3931         | 3071         |
| **1 (BP)**             | 7798         | 293677       | 3260         |
| **2 (FP)**             | 8168         | 3657         | 486801       |

---

## Key Insights and Future Work
- **Feature Importance:** Key features like `AlertId`, `IncidentId`, and `OrgId` contributed the most to model predictions.
- **Model Performance:** Random Forest performed well, achieving a Macro F1-score of 90.80% on test data.
- **Future Improvements:**
  - Address remaining misclassifications by exploring ensemble techniques.
  - Experiment with deep learning models for higher accuracy.
  - Automate feature engineering and preprocessing pipelines for scalability.
