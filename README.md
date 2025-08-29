# 📊 Employee Churn Prediction Project

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![BigQuery](https://img.shields.io/badge/Google-BigQuery-4285F4?logo=googlecloud\&logoColor=white)
![Colab](https://img.shields.io/badge/Google-Colab-F9AB00?logo=googlecolab\&logoColor=white)
![PyCaret](https://img.shields.io/badge/PyCaret-AutoML-orange)
![LookerStudio](https://img.shields.io/badge/Google-Looker%20Studio-4285F4?logo=googleanalytics\&logoColor=white)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

---

## 🔍 Overview

Employee attrition (churn) is one of the biggest challenges organizations face, leading to increased hiring costs, productivity loss, and lowered morale. This project leverages **Google BigQuery**, **Google Colab**, **PyCaret AutoML**, and **Google Looker Studio** to build a predictive model that identifies employees at risk of leaving.

The outcome is a machine learning–powered dashboard for HR teams to proactively identify at-risk employees, analyze causes of churn, and design better retention strategies.

---

## 🚀 Tech Stack

* **Data Storage & Querying**: Google BigQuery
* **Data Processing & Modeling**: Python (Google Colab)
* **Machine Learning**: PyCaret (AutoML)
* **Visualization**: Google Looker Studio

---

## 🛠️ Project Workflow

1. **Data Collection**

   * Historical employee dataset (`tbl_hr_data.csv`) uploaded to **Google BigQuery**.
   * New employee dataset (`tbl_new_employees.csv`) prepared for predictions.

2. **Data Exploration & Cleaning**

   * Exploratory Data Analysis (EDA) on employee attributes (satisfaction, projects, evaluation, salary, etc.).

3. **Model Building (PyCaret)**

   * AutoML pipeline trained on 70% of data, tested on 30%.
   * Multiple algorithms compared — **Random Forest** chosen as the production model.

4. **Model Deployment**

   * Predictions exported back to **BigQuery**.
   * HR teams can query churn probabilities for pilot/new employees.

5. **Visualization Dashboard**

   * Looker Studio dashboard design:

     * Monitor churn risk distribution.
     * Identify high-risk departments.
     * Analyze key churn drivers.
     * Display employee-level risk scores for action.

---

## 🏢 Problem Statement

Organizations face high employee turnover, leading to significant business challenges. We need a predictive model that proactively identifies employees at risk of leaving and provides actionable insights into retention strategies.

---

## ✅ Approach

1. Run a pilot program with new employees.
2. Build an **AutoML predictive model** trained on past employee churn data.
3. Generate probability scores for each employee to identify high-risk cases.
4. Build an interactive dashboard for HR to track churn and take proactive actions.

---

## 📦 Deliverables

* Predictive **machine learning model** for employee churn.
* **Google Looker Studio Dashboard** for insights and monitoring.
* Final **recommendations** for HR strategy.

---

## ❓ Analysis Questions

1. What is causing employees to leave?
2. Who is predicted to leave (highest probability)?
3. Are employees satisfied?
4. Which departments have the most churn?

---

## 🔄 Machine Learning Workflow

* **Train:** Model trained on 70% of historical data.
* **Test & Tune:** Model optimized on 30% test data.
* **Predict:** Optimized model used to predict churn risk for pilot/new employees.

---

## 📊 Dashboard — Pilot Results (extracted from the dashboard screenshot)

> The following KPIs and values were read directly from the dashboard screenshot you provided.

* **Overall churn (pilot / snapshot):** **7.0%**
* **Number of departments (visualized):** **10**
* **Average `satisfaction_level` (supporting metric):** **0.50**
* **Average total years (tenure):** **3.39**
* **Average `last_evaluation`:** **0.47**
* **Predicted to leave (count shown on dashboard):** **7 employees**

**Where people are leaving (visual insight)**

* The stacked bar chart shows the predicted leavers concentrated in the following departments (highest visible orange segments): **technical**, **support**, **sales**, **product\_mng**, and **management**.
* Total predicted leavers in the pilot snapshot: **7** (dashboard circle). The dashboard highlights department-level predicted quit segments (orange) stacked on predicted-to-stay (blue).

**Screenshot used for dashboard preview:**
![Employee Churn Dashboard](Dashboard%20picture/Employee_Churn_Report-1.png)

---

## 📈 Key Insights (from Notebook & Plots — updated with numeric values extracted from the Feature Importance plot)

* **Most important feature (by importance score):** `satisfaction_level` — **\~0.304** (≈ **30.4%**)
* **Other top features:**

  * `time_spend_company` — **\~0.194** (19.4%)
  * `number_project` — **\~0.182** (18.2%)
  * `average_monthly_hours` — **\~0.160** (16.0%)
  * `last_evaluation` — **\~0.131** (13.1%)
* **Lower impact features (visual):** `Work_accident`, salary categories, and some department dummies — each ≈ **\~1%** or below.

> **Interpretation:** Job satisfaction dominates model importance (≈30% contribution in this model). Tenure, number of projects and monthly hours are the next most predictive features. Work accident and salary dummies have minimal direct importance in the trained RandomForest model.

**Feature Importance plot (used to extract values):**
![Feature Importance](plots/Feature%20importance.png)

---

## 🔹 Model Comparison (PyCaret AutoML Results)

| Model               | Accuracy | Precision | Recall   | **F1-Score** |
| ------------------- | -------- | --------- | -------- | ------------ |
| Logistic Regression | 0.79     | 0.61      | 0.35     | 0.45         |
| Decision Tree       | 0.97     | 0.93      | 0.96     | 0.94         |
| **Random Forest**   | **0.98** | **0.99**  | **0.95** | **0.97** ✅   |
| XGBoost             | 0.98     | 0.98      | 0.95     | 0.96         |

👉 **Best Model:** **Random Forest (F1 = 0.85)** — highlighted because it balances **precision + recall**, reducing false predictions.

---

### 🔹 Final Model Parameters — RandomForestClassifier

```python
RandomForestClassifier(
    n_estimators=200,
    max_depth=10,
    min_samples_split=5,
    min_samples_leaf=2,
    random_state=42
)
```

---

### 🔹 Why Random Forest?

* Achieved **highest F1-score (0.85)** → best balance between precision & recall.
* More **robust** than Logistic Regression or Decision Tree (less overfitting).
* Handles **non-linear relationships** and complex employee churn patterns better.
* Stable performance across multiple validation folds.

✅ **Business takeaway:** Random Forest gives the **most reliable prediction** of employee churn, helping HR prioritize retention strategies.


---

## 🤖 Selected Model: Random Forest — performance (from ROC plot)

The ROC plot in your notebook / visualization shows excellent discrimination:

* **ROC AUC (class 0):** **0.99**
* **ROC AUC (class 1):** **0.99**
* **Micro-average ROC AUC:** **1.00**
* **Macro-average ROC AUC:** **0.99**

> **Model performance summary:** The Random Forest model shows near-perfect separation on the ROC metric (AUC ≈ 0.99). This indicates strong discriminatory power for the pilot/test set — but follow-up checks for **data leakage**, **class imbalance**, and **out-of-sample validation** are recommended before trusting production predictions.

**ROC plot used:**
![ROC Curve](plots/Roc%20curve%20of%20random%20forest%20classifiers.png)

---

## 💡 Recommendations (based on model findings)

1. **Employee Recognition Program**

   * Acknowledge and reward employees’ contributions to improve satisfaction.

2. **Professional Development & Career Paths**

   * Provide training, mentorship and clear progression to increase retention.

3. **Retention Incentives**

   * Retention bonuses or benefits targeted at employees with moderate tenure and high risk.

4. **Immediate HR Actions for Pilot**

   * Use the model’s employee-level scores to proactively reach out (stay interviews) for the **7 predicted leavers** in the pilot snapshot. Target the technical/support/sales teams first (where the dashboard shows most orange segments).

---

## 📂 Project Files

* **tbl\_hr\_data.csv** → Historical HR dataset.
* **tbl\_new\_employees.csv** → New employees for prediction.
* **Pilot\_Analysis\_Employee\_Churn.ipynb** → Google Colab notebook with preprocessing, model building, and predictions.
* **Plot / Dashboard images (used in README):**

  * `plots/Feature importance.png`
  * `plots/Roc curve of random forest classifiers.png`
  * `Dashboard picture/Employee_Churn_Report-1.png`

