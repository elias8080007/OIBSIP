# OIBSIP — Data Analytics Internship Projects

Data Analytics projects completed as part of the **Oasis Infobyte Internship Program**.

## Intern Information

* **Name:** Elias Ibrahim Elias
* **Track:** Data Analytics
* **Organization:** Oasis Infobyte
* **Internship Mode:** Remote
* **Repository:** [OIBSIP](https://github.com/elias8080007/OIBSIP)

## Projects

| Project                                   |            Level | Main Techniques                                                                    | Status    |
| ----------------------------------------- | ---------------: | ---------------------------------------------------------------------------------- | --------- |
| Exploratory Data Analysis on Retail Sales | Level 1 — Task 1 | Data cleaning, descriptive statistics, time-series analysis and visualization      | Completed |
| Customer Segmentation Analysis            | Level 1 — Task 2 | RFM analysis, feature scaling, K-Means clustering and customer profiling           | Completed |
| Credit Card Fraud Detection               | Level 2 — Task 3 | Imbalanced classification, Logistic Regression, Random Forest and model evaluation | Completed |

---

## Task 1 — Exploratory Data Analysis on Retail Sales Data

This project performs exploratory data analysis on a retail sales dataset containing **50,000 transactions**.

The analysis examines:

* Monthly and quarterly revenue trends
* Customer age and gender distributions
* Best-selling products
* Revenue by product category
* Correlations between numerical variables
* Delivery time and customer satisfaction
* Actionable business recommendations

### Selected Findings

* Customers aged 25–44 represented approximately **68.6%** of the customer base.
* Electronics generated approximately **77% of total revenue**.
* Delivery time had a strong negative relationship with customer ratings.
* Ratings declined substantially when delivery required more than 10 days.

**Tools:** Python, pandas, matplotlib, seaborn and Google Colab

[View Task 1](./DataAnalytics-L1-EDARetailSales/)

---

## Task 2 — Customer Segmentation Analysis

This project uses **RFM analysis and K-Means clustering** to divide retail customers into meaningful behavioural segments.

The analysis includes:

* Data-quality assessment and cleaning
* Recency, Frequency and Monetary feature engineering
* Log transformation and standardization
* Elbow Method and Silhouette Score evaluation
* K-Means clustering with four customer segments
* Cluster profiling and visualization
* Segment-specific marketing strategies

### Customer Segments

* **Champions:** Highly active, frequent and financially valuable customers
* **Regular Customers:** Moderately active customers with established purchasing behaviour
* **Promising:** Recently active customers with growth potential
* **Hibernating:** Inactive customers requiring re-engagement

### Selected Findings

* Champions represented approximately **16.1%** of customers but generated **64.45% of revenue**.
* Hibernating customers formed the largest segment at approximately **37.7%**.
* Four clusters were selected to provide more actionable customer profiles than a two-cluster solution.

**Tools:** Python, pandas, NumPy, scikit-learn, matplotlib, seaborn and Google Colab

[View Task 2](./DataAnalytics-L1-CustomerSegmentation/)

---

## Task 3 — Credit Card Fraud Detection

This project develops a supervised machine learning pipeline for identifying fraudulent credit card transactions in a highly imbalanced dataset.

The project includes:

* Data-quality assessment and duplicate removal
* Fraud-class imbalance analysis
* Transaction amount and relative-time analysis
* Stratified train/test splitting
* Robust feature scaling
* Balanced class weights
* Logistic Regression and Random Forest models
* Precision, recall, F1-score and ROC-AUC evaluation
* Precision-Recall curve analysis
* Confusion matrices
* Random Forest feature importance
* Scalability and deployment considerations

### Selected Results

| Model               | Fraud Precision | Fraud Recall | Fraud F1 | ROC-AUC | Average Precision |
| ------------------- | --------------: | -----------: | -------: | ------: | ----------------: |
| Logistic Regression |           5.62% |       87.37% |   10.57% |  0.9657 |            0.6719 |
| Random Forest       |          88.46% |       72.63% |   79.77% |  0.9681 |            0.8057 |

Random Forest was selected as the stronger overall model because it provided the best balance between detecting fraud and limiting false alerts.

**Tools:** Python, pandas, NumPy, scikit-learn, matplotlib, seaborn, KaggleHub and Google Colab

[View Task 3](./DataAnalytics-L2-FraudDetection/)

---

## Repository Structure

```text
OIBSIP/
├── DataAnalytics-L1-EDARetailSales/
│   ├── Elias_Ibrahim_Elias_Task1.ipynb
│   ├── README.md
│   └── outputs/
│
├── DataAnalytics-L1-CustomerSegmentation/
│   ├── Elias_Ibrahim_Elias_Task2.ipynb
│   ├── README.md
│   └── outputs/
│
├── DataAnalytics-L2-FraudDetection/
│   ├── Elias_Ibrahim_Elias_Task3.ipynb
│   ├── README.md
│   └── outputs/
│
└── README.md
```

Each project folder contains:

* A complete Jupyter/Google Colab notebook
* A project-specific README
* Generated charts and result files
* Written findings, limitations and recommendations

## Technical Skills Demonstrated

* Python programming
* Data cleaning and validation
* Exploratory data analysis
* Statistical summary and interpretation
* Data visualization
* Feature engineering
* Customer segmentation
* Unsupervised machine learning
* Supervised machine learning
* Imbalanced classification
* Model evaluation
* Business insight generation
* Git and GitHub
* Technical documentation

## Author

**Elias Ibrahim Elias**

Master’s Graduate in Computer and Communication Engineering
Artificial Intelligence, Machine Learning, Software Development and Data Analytics

[GitHub Profile](https://github.com/elias8080007)

