# Credit Card Customer Churn Prediction

## Overview

This project focuses on predicting customer churn for a consumer credit card bank. Customer churn occurs when a customer closes their account or stops using the service. Accurately identifying customers who are likely to churn allows the bank to take early action and improve customer retention.

The problem is framed as a **binary classification task**, where the goal is to distinguish between customers who remain with the bank and those who eventually leave.

---

## Dataset

The dataset used in this project was obtained from Kaggle and contains information on approximately 10,000 credit card customers. It includes:

* Customer demographics (e.g., age, gender, income category)
* Account-related information
* Transaction and usage behavior

The target variable indicates whether a customer is an existing customer or an attrited (churned) customer.

---

## Methodology

The analysis uses a logistic regression model due to its interpretability and suitability for binary classification. Key steps include:

* Train–test splitting with stratification to preserve class balance
* Feature preprocessing using standard scaling for numeric variables and one-hot encoding for categorical variables
* Model training using a pipeline to prevent data leakage
* Hyperparameter tuning using cross-validation
* Evaluation using ROC–AUC, precision–recall analysis, and confusion matrices
* VIF / Multicollinearity:We checked multicollinearity using VIF. Credit_Limit, Total_Revolving_Bal, and Avg_Open_To_Buy exhibit perfect linear dependence (accounting identity), leading to infinite VIF. These were removed to stabilize coefficient interpretation.

---

## Model Evaluation & Validation

The final model was evaluated on a held-out test set using multiple metrics.
Performance was assessed beyond accuracy to account for class imbalance.

- ROC AUC: ~0.92
- KS Statistic: ~0.66
- Precision–Recall tradeoff analyzed across thresholds
- Final decision threshold selected based on recall for churn detection

A threshold of 0.4 was chosen to prioritize early identification of customers
at risk of attrition.

---

## Results

The final model achieves strong predictive performance on the test set:

* **ROC–AUC:** approximately 0.92
* The model successfully identifies a large proportion of customers who eventually churn

A decision threshold lower than the default value was chosen to prioritize identifying at-risk customers, reflecting the higher cost of missing a churned customer compared to flagging a loyal one.

---

## Business Implications

The results suggest that customer churn is strongly influenced by transaction behavior, such as spending patterns and usage frequency. The model can be used by the bank to proactively target customers who are likely to churn through retention strategies such as personalized offers or outreach campaigns.

---

## Limitations and Future Work

While the model demonstrates strong performance, several limitations should be noted. First, the analysis is based on historical customer data and assumes that past behavior patterns will continue into the future. Changes in customer preferences, market conditions, or bank policies may affect the model’s accuracy over time.

Digital transaction behavior is only partially represented by aggregate variables; more granular digital engagement signals (e.g., app logins, digital payment adoption, channel usage) were not available.

Missing value imputation was not performed because the dataset was already pre-cleaned/imputed.

Second, the dataset does not include information on customer lifetime value or the financial cost of churn. As a result, the model treats all churned customers equally, even though some customers may be more valuable to retain than others.

Additionally, the analysis uses a single train-test split. Although cross-validation was used during model tuning, future work could incorporate time-based validation to better reflect how churn prediction models are deployed in practice.

Future extensions of this project could explore cost-sensitive learning, where different misclassification errors are weighted according to their business impact. Incorporating customer lifetime value, temporal trends, or alternative models such as tree-based methods may also provide further insight and improve performance.