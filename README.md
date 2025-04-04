

# 📉 Predicting Credit Card Account Cancellations

## 🚀 Overview
This repository contains the code, analysis, and documentation for a machine learning project titled **"Predicting Credit Card Account Cancellations."** It uses data from over 4,000 credit card customers at a large U.S. bank to:

- Understand key drivers behind account cancellations.
- Build predictive models to forecast future churn.
- Provide actionable insights to improve customer retention and reduce financial losses.

The dataset (`credit_card_df`) includes customer demographics, spending behavior, credit usage patterns, and account status (`customer_status`), indicating whether a customer’s account is active or closed.

---

## 🎯 Objectives
This project aims to answer the following:

1. **Which factors are associated with customer churn (closed accounts)?**
2. **Can we build accurate models to predict future account closures?**
3. **What strategies can the bank adopt to minimize customer churn?**

---

## 📊 Dataset
- **Source**: [`credit_card_df.rds`](https://gmubusinessanalytics.netlify.app/data/credit_card_df.rds)
- **Records**: 4,000+ customers
- **Target Variable**: `customer_status` (Levels: `closed_account`, `active`)  
  **Positive class**: `closed_account`

### 🧮 Key Features
- `age`: Customer age  
- `income`: Annual income (USD)  
- `credit_limit`: Current credit card limit  
- `utilization_ratio`: Monthly balance to credit limit ratio  
- `total_spend_last_year`: Total amount spent in the last year  

(See [📘 Data Definitions](#data-definitions) below for full list.)

---

## 🛠️ Methodology

### 🔧 Tools Used
- Language: **R**
- Libraries: `tidyverse`, `tidymodels`, `ggplot2`, `readr`, `rsample`, `randomForest`, etc.

### 🔍 Process
1. **Data Loading**  
   Data imported from a remote `.rds` file.

2. **Exploratory Data Analysis (EDA)**  
   Identified patterns, relationships, and anomalies in features (income, credit limit, card type, etc.).

3. **Modeling**
   - Data split: Training (80%) and Testing (20%) using `initial_split`.
   - Models trained:
     - Logistic Regression
     - K-Nearest Neighbors (KNN)
     - Random Forest (RF)
   - Cross-validated tuning (e.g., `mtry`, `min_n` for RF).
   - Evaluation metrics: **Accuracy**, **ROC-AUC**, **Confusion Matrix**, etc.

---

## 📈 Key Results

| Model               | ROC-AUC | Accuracy |
|--------------------|---------|----------|
| 🎯 **Random Forest**       | **0.9899**  | **0.949**    |
| K-Nearest Neighbors | 0.9200  | ~0.88    |
| Logistic Regression | 0.9500  | ~0.90    |

- **Random Forest outperformed all models**, with the highest precision and recall for `closed_account`.
- **EDA Insight**: Customers with high utilization ratios and lower income were more likely to close accounts.
- **Significant Features**: `utilization_ratio`, `credit_limit`, `months_inactive_last_year`, `income`.

---

## 💡 Recommendations

1. **Adjust Credit Limits**  
   Tailor credit limits based on income and spending behavior to maintain satisfaction.

2. **Targeted Campaigns**  
   Segment customers by card type or activity level to retain high-risk groups.

3. **Customer Segmentation**  
   Use clustering techniques to identify and engage customer archetypes.

4. **Proactive Retention Monitoring**  
   Monitor inactivity and utilization metrics to flag at-risk customers early.

---

## 📂 Repository Structure

```
credit-card-cancellation-prediction/
├── scripts/                # R scripts for EDA & modeling
│   └── analysis.R
├── data
├── visualizations/         # ROC curves, EDA plots
├── README.md               # Project overview
       # R package dependencies
```

---

## ⚙️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/credit-card-cancellation-prediction.git
```

### 2. Install Dependencies
Ensure R version 4.2.1+ is installed, then in your R console:
```r
install.packages(c("tidyverse", "tidymodels", "ggplot2"))
```

### 3. Load Dataset
```r
library(tidyverse)
credit_card_df <- readRDS(url("https://gmubusinessanalytics.netlify.app/data/credit_card_df.rds"))
```

---

## 📘 Data Definitions

| Variable                  | Definition                                                  | Type      |
|---------------------------|-------------------------------------------------------------|-----------|
| `customer_status`         | Status: `closed_account` or `active`                        | Factor    |
| `age`                     | Customer age                                                | Numeric   |
| `dependents`              | Number of household dependents                              | Numeric   |
| `education`               | Highest education level                                     | Factor    |
| `income`                  | Annual income (USD)                                         | Numeric   |
| `credit_limit`            | Customer's credit card limit                                | Numeric   |
| `utilization_ratio`       | Avg. monthly balance to credit limit ratio                  | Numeric   |
| `total_spend_last_year`   | Total credit card spend last year                           | Numeric   |

*(More variables are included in the notebook.)*

---

## ⚠️ Limitations
- Lack of temporal data restricts trend analysis over time.
- No cost-sensitive evaluation (e.g., cost of false positives).
- Does not include external behavioral or macroeconomic factors.

---

## 📌 Future Work
- Introduce **time-series** or **customer lifecycle** metrics.
- Quantify financial cost of prediction errors.
- Explore **ensemble stacking** to combine model strengths.

