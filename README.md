# Predictive-Dialing-System-for-Bank-Marketing-Campaign

# Bank Marketing Campaign: Predictive Dial ML for Term Deposit Subscription

Optimizing marketing efficiency through machine learning to identify high-potential term deposit subscribers and significantly reduce campaign operational costs.

## 📌 Project Overview
[cite_start]Bank telemarketing campaigns often suffer from high operational costs due to indiscriminate calling strategies[cite: 5, 38]. [cite_start]This project develops a predictive model to identify customers most likely to subscribe to a term deposit, allowing the marketing team to focus resources on high-probability leads[cite: 5].

**Key Achievement:**
* [cite_start]**38.6% Cost Reduction:** Saving approximately **$6,656/day** compared to a "call-all" strategy[cite: 4, 38].
* [cite_start]**Recall of 75%:** Successfully capturing 75 out of 100 actual depositors[cite: 4, 33].
* [cite_start]**Operational Efficiency:** Freed up **39 staff members** for reallocation to other revenue streams[cite: 38, 48].

## 📊 Dataset Summary
* [cite_start]**Records:** 7,805 customer records[cite: 2, 6].
* [cite_start]**Features:** 11 features including age, job, balance, housing loan, and previous campaign outcomes[cite: 3, 7].
* [cite_start]**Class Distribution:** Balanced (48% Yes / 52% No for term deposits)[cite: 6, 8].

## ⚙️ Methodology

### 1. Data Preprocessing
* [cite_start]**Pipeline Design:** Integrated Simple Imputer (Median), feature encoding, and scaling[cite: 4, 21].
* [cite_start]**RobustScaler:** Used to handle significant outliers in `balance` and `campaign` features without losing valuable business information[cite: 21, 24].
* [cite_start]**Feature Engineering:** Created `was_contacted_before` flag and handled `-1` values in `pdays`[cite: 21].

### 2. Modeling & Selection
[cite_start]We compared 8 algorithms using 5-fold cross-validation with **Recall** as the primary metric to minimize missed revenue opportunities (False Negatives)[cite: 4, 25].

| Model | Recall Mean | Status |
| :--- | :--- | :--- |
| **Random Forest** | **0.634** | **✅ SELECTED** |
| AdaBoost | 0.643 | High Variance |
| Voting Classifier | 0.633 | - |

[cite_start]**Why Random Forest?** It naturally handles multicollinearity, is robust to outliers, and provides stable predictions through its bagging mechanism[cite: 27, 28, 29].

### 3. Hyperparameter Tuning
* [cite_start]**Optimal Threshold:** Calibrated at **0.40**[cite: 4, 31].
* [cite_start]**Tuned Parameters:** `n_estimators: 300`, `min_samples_leaf: 1`, `max_depth: None`, `class_weight: 'balanced'`[cite: 32].

## 📈 Business Impact Evaluation
Using the Targeted Strategy (Threshold 0.40) vs. the standard Call-All Strategy:

| Metric | Call All Strategy | Targeted Strategy |
| :--- | :--- | :--- |
| Total Daily Calls | 7,813 | 4,296 (45% fewer) |
| Daily Operational Cost | $17,258 | $10,602 |
| **Daily Savings** | - | **$6,656 (38.6%)** |

[cite_start]*Note: Based on cost-benefit framework where False Negatives (missed depositors) are weighted more heavily ($1 loss) than False Positives ($0.1 call cost)[cite: 6, 38].*

## 💡 Key Business Insights (SHAP Analysis)
* [cite_start]**Previous Success:** Customers who converted in previous campaigns are the strongest predictors for current success[cite: 18, 42].
* [cite_start]**Contact Data Quality:** "Unknown" contact types are major negative predictors; verified cellular channels perform best[cite: 15, 39, 44].
* [cite_start]**Financial Profile:** High account balances correlate with higher subscription probability, while active housing loans act as a negative indicator[cite: 13, 19, 41].

## 🚀 Strategic Recommendations
1. [cite_start]**Tiered Outreach:** Segment leads by probability scores (Priority 1: >0.80 for senior agents; Priority 3: <0.60 for Email/SMS)[cite: 48].
2. [cite_start]**CRM Cleanup:** Invest in contact verification to reduce "Unknown" data points[cite: 48, 49].
3. [cite_start]**Seasonal Timing:** Schedule high-intensity campaigns in **March, September, October, and December** for peak conversion[cite: 17, 50].
4. [cite_start]**Retention Program:** Prioritize re-engagement for prior subscribers first[cite: 52].

---
[cite_start]*Created as part of Capstone Project III.* [cite: 2]
