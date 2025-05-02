# Broadband Company Customer Churn Prediction

## Overview

This project focuses on predicting customer churn for a broadband company using a Random Forest Classifier. The analysis includes exploratory data analysis (EDA) and the development of a machine learning model to identify customers at risk of churning. The goal is to optimize the model for high accuracy and AUC (Area Under the ROC Curve) to support retention strategies.

## Objectives

- **Exploratory Data Analysis (EDA)**: Understand customer demographics, usage patterns, and billing information.  
- **Churn Prediction**: Build a Random Forest model to predict which customers are likely to churn.  
- **Model Optimization**: Use GridSearchCV to fine-tune hyperparameters for improved model performance.  
- **Performance Evaluation**: Assess the model using accuracy, precision, recall, F1-score, and AUC metrics.  
- **Business Insights**: Provide actionable insights to reduce churn based on model predictions.

## Dataset

The dataset contains 1,114 customer records with the following columns:

- `CUST_ID`: Unique customer identifier.  
- `GENDER`: Customer gender (0 or 1).  
- `AGE`: Customer age (18 to 76 years).  
- `TENURE`: Months of subscription (1 to 72 months).  
- `CHANNEL`: Acquisition channel (1 to 4).  
- `AUTOPAY`: Whether the customer uses autopay (0 or 1).  
- `ARPB_3M`: Average revenue per user over the last 3 months ($68 to $2,049).  
- `CALL_PARTY_CNT`: Number of unique parties called.  
- `DAY_MOU`: Minutes of use during the day.  
- `AFTERNOON_MOU`: Minutes of use in the afternoon.  
- `NIGHT_MOU`: Minutes of use at night.  
- `AVG_CALL_LENGTH`: Average call duration (in minutes).  
- `BROADBAND`: Whether the customer has broadband service (0 or 1).

**Key Details**:

- The dataset includes binary (`GENDER`, `AUTOPAY`, `BROADBAND`), categorical (`CHANNEL`), and numerical (`AGE`, `TENURE`, `ARPB_3M`, etc.) features.  
- The target variable (churn) is binary (0 for non-churn, 1 for churn), though not explicitly shown in the provided code snippet.  
- No missing values are assumed based on the EDA section.

## Key Steps

1. **Data Loading and Preprocessing**:  
     
   - The dataset is loaded using `pandas` and stored in a DataFrame (`df`).  
   - EDA is performed to explore customer demographics, usage patterns, and billing data.

   

2. **Model Development**:  
     
   - **Random Forest Classifier**: A Random Forest model is trained using `scikit-learn`.  
   - **GridSearchCV**: Hyperparameter tuning is performed using `GridSearchCV` to optimize the model. Two rounds of tuning are conducted:  
     - **First Round**:  
       - Parameters: `criterion` (entropy, gini), `max_depth` (5, 6, 7, 8), `max_features` (0.3, 0.4, 0.5), `min_samples_split` (4, 8, 12, 16), `n_estimators` (11, 13, 15).  
       - Best Parameters: `criterion='entropy'`, `max_depth=8`, `max_features=0.4`, `min_samples_split=4`, `n_estimators=11`.  
       - Performance: Accuracy \= 88%, AUC \= 0.8847.  
     - **Second Round (Fine-Tuning)**:  
       - Parameters: `criterion` (entropy, gini), `max_depth` (7, 8, 10, 12), `max_features` (0.4, 0.5, 0.6, 0.7), `min_samples_split` (2, 3, 4, 8, 12, 16), `n_estimators` (11, 13, 15, 17, 19).  
       - Best Parameters: `criterion='gini'`, `max_depth=12`, `max_features=0.6`, `min_samples_split=2`, `n_estimators=19`.  
       - Performance: Accuracy \= 90%, AUC \= 0.9003.

   

3. **Model Evaluation**:  
     
   - **Metrics**: The model is evaluated on the test set using:  
     - **Classification Report**: Precision, recall, F1-score for churn (1) and non-churn (0) classes.  
     - **AUC**: Area Under the ROC Curve to measure the model’s ability to distinguish between classes.  
   - **First Round Results**:  
     - Non-Churn (0): Precision \= 0.99, Recall \= 0.88, F1-score \= 0.93.  
     - Churn (1): Precision \= 0.45, Recall \= 0.89, F1-score \= 0.60.  
     - Accuracy: 88%, AUC: 0.8847.  
   - **Second Round Results**:  
     - Non-Churn (0): Precision \= 0.99, Recall \= 0.90, F1-score \= 0.94.  
     - Churn (1): Precision \= 0.53, Recall \= 0.90, F1-score \= 0.67.  
     - Accuracy: 90%, AUC: 0.9003.

     

---

