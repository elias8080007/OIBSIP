# Credit Card Fraud Detection

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/elias8080007/OIBSIP/blob/main/DataAnalytics-L2-FraudDetection/Elias_Ibrahim_Elias_Task3.ipynb)

A supervised machine learning project completed for the **Oasis Infobyte Data Analytics Internship — Level 2, Task 3**.

## Project Information

* **Author:** Elias Ibrahim Elias
* **Organization:** Oasis Infobyte
* **Track:** Data Analytics
* **Level:** Level 2
* **Task:** Task 3 — Fraud Detection
* **Environment:** Google Colab
* **Language:** Python

## Project Objective

The objective of this project is to build and evaluate a machine learning pipeline capable of detecting fraudulent credit card transactions in a severely imbalanced dataset.

The project focuses on:

* Understanding the rarity of fraudulent transactions
* Examining transaction amount and time patterns
* Preventing data leakage
* Handling class imbalance
* Comparing two classification models
* Evaluating fraud detection using appropriate metrics
* Understanding the precision–recall trade-off
* Discussing production scalability

## Dataset

The project uses the public [Credit Card Fraud Detection dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud).

The original dataset contains:

* **284,807 transactions**
* **31 columns**
* **492 fraudulent transactions**
* Transactions collected over approximately two days

### Columns

* `Time`: Seconds elapsed since the first transaction
* `Amount`: Financial value of the transaction
* `V1`–`V28`: Anonymized transformed numerical features
* `Class`: Prediction target

  * `0`: Legitimate transaction
  * `1`: Fraudulent transaction

The notebook downloads the dataset automatically using KaggleHub. The original CSV file is therefore not stored in this repository.

## Data Quality and Cleaning

The data-quality assessment examined:

* Missing values
* Duplicate rows
* Infinite numerical values
* Invalid target labels
* Negative transaction amounts
* Negative transaction times
* Column data types

Exact duplicate records were removed before modelling to reduce repeated observations and prevent identical transactions from appearing in both training and testing data.

After duplicate removal, the dataset contained:

* **283,726 transactions**
* **283,253 legitimate transactions**
* **473 fraudulent transactions**
* Fraud rate of approximately **0.1667%**

This corresponds to approximately 599 legitimate transactions for every fraudulent transaction.

## Exploratory Data Analysis

The exploratory analysis includes:

1. Fraud-class distribution
2. Transaction amount statistics for fraud and legitimate classes
3. Log-transformed amount-distribution comparison
4. Relative hour calculation from elapsed transaction time
5. Fraud rate by relative hour
6. Identification of the relative periods with the highest observed fraud rates

A logarithmic scale is used in selected visualizations to make the extremely small fraud class and highly skewed transaction amounts easier to examine. The transformation is used only for visualization and does not replace the original transaction values.

## Why Accuracy Is Misleading

Fraudulent transactions represent less than 0.2% of the dataset.

A model predicting every transaction as legitimate could achieve an accuracy above 99.8% while detecting no fraud. Therefore, accuracy alone is not an appropriate measure of fraud-detection performance.

The project emphasizes:

* **Precision:** How many fraud alerts were genuinely fraudulent
* **Recall:** How many actual fraud cases were detected
* **F1-score:** Balance between precision and recall
* **ROC-AUC:** Overall ability to distinguish the two classes
* **Average Precision:** Performance focused on the rare fraud class

## Data Preparation

The modelling workflow uses:

* An 80/20 train/test split
* Stratification to preserve the fraud percentage
* `RobustScaler` for the `Time` and `Amount` features
* Training-only scaler fitting to prevent data leakage
* Balanced class weights to address class imbalance

The `V1`–`V28` features were already numerically transformed in the original dataset.

## Class-Imbalance Strategy

Balanced class weights were selected instead of oversampling.

This approach:

* Assigns a larger training penalty to errors involving fraud
* Retains all original observations
* Avoids creating synthetic financial records
* Requires less memory than full oversampling
* Can be applied directly to both selected classifiers

## Machine Learning Models

Two models were trained and compared:

### Logistic Regression

Logistic Regression provides an interpretable baseline for binary classification. It was trained using:

```python
class_weight="balanced"
```

### Random Forest

Random Forest combines multiple decision trees and can identify non-linear patterns. It was trained using:

```python
class_weight="balanced_subsample"
```

Tree depth and minimum leaf size were controlled to reduce overfitting and maintain practical training time.

## Model Results

| Model               | Accuracy | Fraud Precision | Fraud Recall | Fraud F1 | ROC-AUC | Average Precision |
| ------------------- | -------: | --------------: | -----------: | -------: | ------: | ----------------: |
| Logistic Regression |   97.52% |           5.62% |       87.37% |   10.57% |  0.9657 |            0.6719 |
| Random Forest       |   99.94% |          88.46% |       72.63% |   79.77% |  0.9681 |            0.8057 |

### Confusion-Matrix Results

| Model               | Fraud Detected | Fraud Missed | False Alerts | Correct Legitimate |
| ------------------- | -------------: | -----------: | -----------: | -----------------: |
| Logistic Regression |             83 |           12 |        1,394 |             55,257 |
| Random Forest       |             69 |           26 |            9 |             56,642 |

## Model Selection

Random Forest was selected as the stronger overall model.

It achieved:

* **88.46% fraud precision**
* **72.63% fraud recall**
* **79.77% fraud F1-score**
* **0.9681 ROC-AUC**
* **0.8057 Average Precision**
* Only **9 false fraud alerts**

Logistic Regression detected more fraud cases, achieving a recall of 87.37%. However, its precision was only 5.62%, meaning that it incorrectly flagged a large number of legitimate transactions.

Random Forest therefore provides a substantially more practical balance between fraud detection and false-alert control.

## Precision–Recall Trade-Off

Recall is important because a false negative represents fraud the system failed to detect. However, maximizing recall without considering precision may create an excessive number of false alerts.

In a production environment, the classification threshold should be selected according to business costs:

* A lower threshold increases recall but creates more false alerts.
* A higher threshold increases precision but may miss more fraud.
* Medium-risk transactions could require additional authentication.
* High-risk transactions could be temporarily held for investigation.

## Feature Importance

Random Forest feature importance is used to rank the predictors contributing most strongly to classification.

Because `V1`–`V28` are anonymized transformations, their original business meanings are unavailable. Feature importance therefore identifies predictive relevance but does not establish a causal relationship with fraudulent behaviour.

The complete ranking is available in:

```text
outputs/random_forest_feature_importance.csv
```

## Scalability

One million transactions per hour corresponds to approximately 278 transactions per second on average.

A production implementation should include:

* Distributed streaming ingestion
* Reusable and versioned preprocessing
* A low-latency prediction service
* Horizontal service scaling
* Risk-based decision thresholds
* Automated monitoring
* Model-drift detection
* Periodic retraining
* Human review for high-impact decisions

The complete pipeline would require load testing before deployment to verify its latency and throughput during normal traffic and traffic peaks.

## Business Recommendations

1. Use Random Forest as the primary fraud-screening model.
2. Introduce multiple risk levels instead of one automatic rejection rule.
3. Investigate the characteristics of the 26 missed fraud cases.
4. Monitor precision, recall, alert volume and incoming feature distributions.
5. Retrain the model using newly verified transactions.
6. Retain human review for high-risk or irreversible decisions.

## Limitations

* The dataset covers only a short transaction period.
* Most features are anonymized.
* The experiment uses one stratified train/test split.
* No monetary cost was assigned to false positives and false negatives.
* The classification threshold was not optimized for a particular business objective.
* Production scalability was discussed but not load-tested.
* Historical results do not guarantee equivalent performance on future fraud patterns.

## Repository Structure

```text
DataAnalytics-L2-FraudDetection/
├── Elias_Ibrahim_Elias_Task3.ipynb
├── README.md
└── outputs/
    ├── README.md
    ├── fraud_class_distribution.png
    ├── transaction_amount_distribution.png
    ├── fraud_rate_by_relative_hour.png
    ├── logistic_regression_confusion_matrix.png
    ├── random_forest_confusion_matrix.png
    ├── roc_curve_comparison.png
    ├── precision_recall_curve_comparison.png
    ├── random_forest_feature_importance.png
    ├── model_comparison.csv
    └── random_forest_feature_importance.csv
```

## Running the Notebook

1. Open `Elias_Ibrahim_Elias_Task3.ipynb` in Google Colab.
2. Select **Runtime → Run all**.
3. The notebook will install KaggleHub and download the public dataset.
4. Allow the two models to complete their training.
5. Review the generated metrics, tables and visualizations.

The notebook should be run sequentially because later cells depend on variables and models created in earlier sections.

## Technologies

* Python
* pandas
* NumPy
* scikit-learn
* matplotlib
* seaborn
* KaggleHub
* Google Colab
* Git and GitHub

## Author

**Elias Ibrahim Elias**

Master’s Graduate in Computer and Communication Engineering
Artificial Intelligence, Machine Learning, Software Development and Data Analytics

[GitHub Profile](https://github.com/elias8080007)

