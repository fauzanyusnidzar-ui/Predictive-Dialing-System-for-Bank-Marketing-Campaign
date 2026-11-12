# Bank Marketing Campaign: Predictive Dial ML for Term Deposit Subscription

Optimizing marketing efficiency through machine learning to identify high-potential term deposit subscribers and significantly reduce campaign operational costs.

## 📌 Project Overview
Bank telemarketing campaigns often suffer from high operational costs due to indiscriminate calling strategies. This project developed a predictive model to identify customers most likely to subscribe to a term deposit, enabling the bank to focus resources on high-probability leads.

**Key Achievements:**
* **39.4% Cost Reduction:** Saving approximately **$6,798/day** compared to a "call-all" strategy.
* **Recall of 75%:** Successfully capturing 75 of every 100 actual depositors.
* **Operational Efficiency:** Freed up **39 staff members** for reallocation to other revenue streams.
* **Call Optimization:** Eliminated **3,517 unnecessary calls** per day (45% less workload).

## 📊 Dataset Summary
* **Records:** 7,813 customer records.
* **Features:** 10 features + 1 target (`deposit`), including age, job, balance, housing loan, contact type, and previous campaign outcome.
* **Class Distribution:** Balanced (47.8% Yes / 52.2% No for term deposits).
* **Train/Test Split:** 80/20 stratified (6,250 / 1,563 rows).

## ⚙️ Methodology

### 1. Data Preprocessing
* **Pipeline Design:** Integrated Simple Imputer (Median), feature encoding, and scaling inside a single scikit-learn `Pipeline`, so it is fitted only on training folds (no data leakage).
* **RobustScaler:** Applied to numeric columns such as `balance` and `campaign`. These contain outliers that are valid business values, and RobustScaler handles them through median and IQR scaling.
* **Feature Engineering:** Created a `was_contacted_before` flag from `pdays`, used OrdinalEncoder for `housing` and `loan`, and OneHotEncoder for `job`, `contact`, `month` and `poutcome`.

### 2. Modeling & Selection
We compared 8 algorithms using 5-fold cross-validation with **Recall** as the primary metric to minimize missed revenue opportunities.

| Model | Recall Mean | Recall Std | Status |
| :--- | :--- | :--- | :--- |
| AdaBoost | 0.655 | ±0.024 | - |
| **Random Forest** | **0.640** | **±0.024** | **✅ SELECTED** |
| Voting Classifier | 0.637 | ±0.028 | - |
| KNN | 0.621 | ±0.026 | - |
| Stacking | 0.616 | ±0.038 | - |
| Decision Tree | 0.612 | ±0.019 | - |
| Logistic Regression | 0.590 | ±0.030 | - |
| Bagging | 0.586 | ±0.019 | - |

**Why Random Forest?** AdaBoost scored slightly higher, but Random Forest was chosen for five reasons:
* It naturally handles multicollinearity.
* It is robust to outliers.
* Bagging gives it stability and reduces overfitting compared to boosting.
* `class_weight='balanced'` handles the minority class.
* It works with a tree-based SHAP explainer for business interpretability.

### 3. Hyperparameter Tuning & Threshold Calibration
* **RandomizedSearchCV** (50 iterations × 5-fold CV) found these best parameters: `n_estimators=300`, `max_depth=None`, `min_samples_split=10`, `min_samples_leaf=1`, `max_features='log2'`, `class_weight='balanced'`.
* **Optimal Threshold:** Calibrated at **0.40**. At this threshold the model captures 3 out of 4 depositors and reduces total calls by 45%.
* **Recall Improvement:** Test Recall rose from 62% (base model) to **75%** after tuning (+12.6 pp). The train–test overfitting gap fell from 0.38 to 0.20.

## 🎯 Model Performance (Test Set)

| Recall | Precision | F1-Score | Accuracy |
| :---: | :---: | :---: | :---: |
| **75%** | **65%** | **0.69** | **69%** |

## 📈 Business Impact Evaluation
Comparing the **Targeted Strategy (Threshold 0.40)** with the standard **Call All Strategy** on the full population of 7,813 leads:

| Metric | Call All Strategy | Targeted Strategy |
| :--- | :--- | :--- |
| Total Daily Calls | 7,813 | 4,296 |
| Depositors Captured | 3,732 (100%) | 2,793 (75%) |
| Missed Opportunities | 0 | 939 |
| Operational Call Cost | $781 | $430 |
| Opportunity Loss ($1 per missed depositor) | $0 | $939 |
| Staff Required | 87 agents | 48 agents |
| Staff Overhead | $16,477 | $9,091 |
| **TOTAL DAILY COST** | **$17,258** | **$10,460** |

**Net result:** **$6,798 saved per day**, a **39.4% total cost reduction**.

## 💡 Key Business Insights (SHAP Analysis)
* **Unknown Contact Channel:** The strongest negative predictor; verified contact methods are crucial for success.
* **Housing Loans:** Customers with existing housing loans are less likely to subscribe due to existing financial commitments.
* **Account Balance:** Higher-balance customers show a stronger propensity to subscribe.
* **Previous Success:** If a customer converted in a previous campaign, they are significantly more likely to convert again.
* **Age:** Older customers are more likely to subscribe to a term deposit.

## 🚀 Strategic Recommendations
1. **Tiered Outreach:** Segment leads by probability score:
   * **Priority 1 (> 0.80):** senior agents, same-day calls.
   * **Priority 2 (0.40–0.80):** standard campaign queue.
   * **Priority 3 (< 0.40):** low-cost Email/SMS automation.
2. **Seasonal Scheduling:** Focus high-intensity campaigns in **March, September, October, and December** (historically highest conversion), and reduce intensity in May.
3. **Data Quality Program:** Invest in KYC to verify contact data, as "Unknown" contact types significantly reduce success rates.
4. **Retention Focus:** Prioritize repeat engagement for customers who have successfully converted in the past.
5. **Model Governance:** Review performance every 3–6 months and retrain if Recall drops below 70%.

---
*Created as part of Capstone Project III. Full details can be found in `Bank Marketing Campaign — Predictive Dial ML (BOD).pdf`.*
