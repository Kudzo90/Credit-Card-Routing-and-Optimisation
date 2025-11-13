# Project Summary: Credit Card Transaction Success Prediction and PSP Optimization

## Overview

Many online businesses face revenue losses and customer churn caused by failed credit card payments. This project aims to tackle this challenge by building a practical machine learning model that predicts whether a transaction will succeed or fail. In addition, the project seeks to recommend the best Payment Service Provider (PSP) for each transaction, optimizing both success rates and transaction costs.

## Business Context

Payment failures are a persistent challenge for e-commerce businesses. Every failed transaction not only results in lost sales but can also cause customers to abandon the platform. By smartly routing payment attempts to the most appropriate PSP, businesses can improve transaction success, lower the costs linked to failed payments, and deliver a better experience to their customers.

## Project Goals

1. **Predict Transaction Success:** Create a reliable model that forecasts if a credit card transaction will go through or not.  
2. **Optimize PSP Selection:** Use the prediction to suggest the best PSP for each transaction, weighing both the chance of success and the related fees.  
3. **Minimize Costs:** Lower the total cost by choosing PSPs that offer reduced fees for successful payments.  
4. **Improve Customer Experience:** Make payments more likely to succeed, ensuring smoother checkouts and happier customers.

## Dataset

The dataset used for this project contains detailed information about credit card transactions, including:

- `tmsp`: Timestamp of the transaction.  
- `amount`: Transaction amount.  
- `PSP`: Payment Service Provider used for the transaction.  
- `3D_secured`: Indicates if 3D Secure authentication was used.  
- `repeated_transactions`: Flag for repeated transactions.  
- `is_first_attempt`: Indicates if it's the first attempt for a transaction.  
- `total_fees`: The total fees incurred for the transaction.  
- `attempts_within_one_minute`: Number of attempts within one minute.  
- `time_since_last_attempt_seconds`: Time elapsed since the last attempt.  
- `hour`, `day`: Time-based features extracted from the timestamp.  
- `country_Germany`, `country_Switzerland`: One-hot encoded country information.  
- `card_Master`, `card_Visa`: One-hot encoded card type information.  
- `hour_sin`, `hour_cos`, `day_sin`, `day_cos`, `month_sin`, `month_cos`, `day_of_week_sin`, `day_of_week_cos`: Cyclical features for time.  
- `success`: The target variable, indicating transaction success (`1`) or failure (`0`).
## NB: Most of these columns (features) are derived from the original dataset
## OROGINAL DATASET AVAILABILITY
Due to licensing issues the original data is not made available. However, I've provided a way around this challenge. The `synthetic date generator notebook` added can be used to generate synthetic data for this project.
## Methodology

### 1. Data Preprocessing
- Checked for missing values (none were found in the data).  
- Added cyclical time features (like `hour_sin` and `hour_cos`) to help the model learn time-based patterns.  
- Removed unnecessary columns (such as `tmsp`, `PSP`, `hour`, and `day`) since their information was either already included in other features or not useful for predicting success.

### 2. Model Development
- **Base Model (Logistic Regression):**  
  A Logistic Regression model was trained as a baseline. It reached about **81% accuracy** overall but struggled to correctly predict successful transactions due to class imbalance.  
- **Random Forest Classifier:**  
  A Random Forest model was then implemented, which achieved **~98% accuracy** on the test data, significantly improving prediction performance.

### 3. Evaluation
- **Accuracy:** Measures how often the model predicts correctly.  
- **Confusion Matrix:** Shows how many predictions were right or wrong for each outcome (success or failure).  
- **Classification Report:** Provides precision, recall, and F1-score for both classes, highlighting how well the model performs with imbalanced data.  

The Random Forest model performed strongly, with high scores for both precision and recall on successful and failed transactions, demonstrating its robustness to class imbalance.

## Key Findings

- The Random Forest model outperforms Logistic Regression for predicting transaction success.  
- Handling class imbalance is critical for accurate predictions across both classes.  
- Feature engineering—particularly cyclical time features and one-hot encoding—substantially improved model performance.

## Future Work & Deployment Considerations

- **Real-time Integration:** Deploy the model as a real-time API for instant PSP recommendations per payment attempt.  
- **A/B Testing:** Compare model-based PSP routing with existing business methods.  
- **Dynamic Fee Integration:** Include real-time PSP fee data for adaptive cost optimization.  
- **Continuous Monitoring:** Track model performance and retrain periodically as data patterns evolve.  
- **Explainability:** Use feature importance or SHAP analysis to clarify why specific PSPs are recommended, aiding decision transparency.

---

**In summary**, this project provides a practical solution to enhance credit card transaction routing, enabling online businesses to increase payment success rates while reducing costs from failed transactions.
