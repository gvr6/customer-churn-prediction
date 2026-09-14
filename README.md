# Customer Churn Prediction

A machine learning classification project that predicts whether a customer is likely to churn based on customer tenure, product usage, and support activity.

## Overview

Customer churn is an important business problem for subscription-based companies. When customers stop using a service, businesses can experience recurring revenue loss and increased customer acquisition costs.

This project applies machine learning classification techniques to predict whether a customer is likely to churn or remain with the service. The prediction is based on customer tenure, total usage, and support ticket activity.

The project also compares multiple classification models and evaluates their performance using accuracy, precision, recall, and F1-score.

## Business Problem

Subscription-based businesses need to identify customers who are at risk of leaving so that appropriate retention strategies can be applied.

A simple rule based on a single customer attribute may not capture the combined patterns associated with churn. Machine learning allows multiple customer-related features to be analyzed together to generate churn predictions.

The predicted results can be used to prioritize customers for targeted communication, additional support, and retention offers.

## Project Objective

The objective of this project is to:

- Predict whether a customer is likely to churn or remain with the service.
- Analyze customer tenure, usage, and support activity.
- Compare different classification models.
- Evaluate model performance using multiple classification metrics.
- Generate churn predictions for previously unseen customers.

## Dataset

The project uses five datasets:

| Dataset | Rows | Columns |
|---|---:|---:|
| `account_master.csv` | 392 | 5 |
| `usage_logs.csv` | 4,715 | 5 |
| `support_tickets.csv` | 1,161 | 5 |
| `churned_labeled.csv` | 334 | 2 |
| `churned_to_predict.csv` | 58 | 1 |

### Target Variable

The target variable is `churn`.

| Class | Percentage | Customers |
|---|---:|---:|
| No Churn | 75.15% | 251 |
| Churn | 24.85% | 83 |

The dataset therefore contains a noticeable class imbalance.

### Features Used

| Feature | Type | Description |
|---|---|---|
| `tenure_months` | Numerical | Number of months the customer has been with the service |
| `total_usage` | Numerical | Total usage of the service by the customer |
| `ticket_count` | Numerical | Number of support tickets raised by the customer |

Missing values in usage and support-ticket features were handled by replacing them with zero, assuming that the absence of a record represented no recorded usage or tickets.

## Project Workflow

The project follows the following workflow:

1. Load the customer datasets.
2. Inspect the datasets and identify data quality issues.
3. Handle missing values.
4. Combine account, usage, and support-ticket information using the customer identifier.
5. Aggregate usage and support information at customer level.
6. Perform exploratory data analysis.
7. Prepare the features and target variable.
8. Split the data into training and testing sets.
9. Train multiple classification models.
10. Evaluate model performance.
11. Select the final model.
12. Generate predictions for new customers.

## Exploratory Data Analysis

The analysis focused on understanding relationships between customer behaviour and churn.

Key observations included:

- Churned customers showed lower average weekly login activity compared with non-churned customers.
- Churn rates varied across different plan tiers.
- The dataset contained more non-churn customers than churn customers.

These observations helped identify customer engagement and account characteristics that may be associated with churn.

## Machine Learning Models

The following classification models were evaluated:

| Model | Accuracy |
|---|---:|
| K-Nearest Neighbors | 72.28% |
| Logistic Regression | 75.25% |
| Random Forest | 76.24% |

A Dummy Classifier was also used as a baseline model.

### Final Model

Random Forest was selected as the final model because it achieved the highest accuracy among the three main classification models.

**Final Model Accuracy: 76.24%**

However, accuracy alone does not provide a complete picture of churn prediction performance because the dataset is imbalanced.

## Model Evaluation

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

Special attention was given to recall and F1-score for the Churn class.

Accuracy can be misleading when the target classes are imbalanced. Recall is particularly important for this project because missing customers who are actually likely to churn can reduce the effectiveness of retention strategies.

## Model Performance

The final Random Forest model achieved:

- Accuracy: 76.24%
- Correctly classified test customers: 77 out of 101
- Churn recall: 16%

The model correctly identified 4 out of 25 actual churn customers.

This indicates that although Random Forest achieved the highest overall accuracy, there is still significant room for improvement in identifying actual churn customers.

## Challenges

### 1. Class Imbalance

The dataset contained more No Churn customers than Churn customers.

An initial Logistic Regression approach had difficulty identifying churn customers. A balanced Logistic Regression model using `class_weight='balanced'` improved churn recall to 48%, although Random Forest was later selected as the final model based on overall accuracy.

### 2. Combining Multiple Data Sources

Customer information was distributed across account, usage, and support-ticket datasets.

The datasets were combined using `account_id`, and usage and ticket information was aggregated at customer level.

This produced a consolidated dataset containing customer tenure, total usage, and ticket count.

### 3. Model Selection

Different classification models produced different results.

KNN, Logistic Regression, and Random Forest were compared using accuracy, precision, recall, and F1-score to understand their strengths and weaknesses.

Random Forest achieved the highest overall accuracy and was selected as the final model.

## Limitations

The project has several limitations:

- The final model does not reliably identify every customer who will churn.
- Churn recall is relatively low at 16%.
- The model uses only three main predictive features.
- The labeled dataset contains only 334 customer accounts.
- The limited dataset size may affect how well the model generalizes to a larger customer base.

## Future Improvements

With additional time and data, the following improvements could be implemented:

1. Tune the classification threshold and model parameters to improve churn recall.
2. Use additional customer information such as satisfaction, contract details, and historical churn patterns.
3. Increase the size of the labeled dataset.
4. Build an interactive dashboard for viewing churn predictions, high-risk customers, and model metrics.

## Tech Stack

- Python 3.10.6
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

````markdown
### Project Structure

```text
customer-churn-prediction/
│
├── account_master.csv
├── usage_logs.csv
├── support_tickets.csv
├── churned_labeled.csv
├── churned_to_predict.csv
├── final_churn_predictions.csv
├── saas_churn_final.ipynb
├── ML Mini Project - Final.docx
├── README.md
├── requirements.txt
└── .gitignore
```

### How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/gvr6/customer-churn-prediction.git
cd customer-churn-prediction
```
