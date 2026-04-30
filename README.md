# Predictive-Dialing-System-for-Bank-Marketing-Campaign

# Bank Marketing Campaign: Predictive Dial ML for Term Deposit Subscription

Optimizing marketing efficiency through machine learning to identify high-potential term deposit subscribers and significantly reduce campaign operational costs.

## 📌 Project Overview
Bank telemarketing campaigns often suffer from high operational costs due to indiscriminate calling strategies. This project developed a predictive model to identify customers most likely to subscribe to a term deposit, enabling the bank to focus resources on high-probability leads.

**Key Achievements:**
* **38.6% Cost Reduction:** Saving approximately **$6,656/day** compared to a "call-all" strategy.
* **Recall of 75%:** Successfully capturing 75 of every 100 actual depositors.
* **Operational Efficiency:** Freed up **39 staff members** for reallocation to other revenue streams.
* **Call Optimization:** Eliminated **3,517 unnecessary calls** per day.

## 📊 Dataset Summary
* **Records:** 7,805 customer records.
* **Features:** 11 features including age, job, balance, housing loan, and previous campaign outcomes.
* **Class Distribution:** Balanced (47.8% Yes / 52.2% No for term deposits).

## ⚙️ Methodology

### 1. Data Preprocessing
* **Pipeline Design:** Integrated Simple Imputer (Median), feature encoding, and scaling pipeline.
* **RobustScaler:** Applied to numeric columns like `balance` and `campaign` to handle valid business outliers via IQR.
* **Feature Engineering:** Created `was_contacted_before` flag from `pdays` and encoded categorical variables.

### 2. Modeling & Selection
We compared multiple algorithms using 5-fold cross-validation with **Recall** as the primary metric to minimize missed revenue opportunities.

| Model | Recall Mean | Status |
| :--- | :--- | :--- |
| **Random Forest** | **0.634** | **✅ SELECTED** |
| AdaBoost | 0.643 | - |
| Voting Classifier | 0.633 | - |

**Why Random Forest?** It naturally handles multicollinearity, is robust to outliers, and provides stability through bagging, which reduces overfitting compared to boosting.

### 3. Hyperparameter Tuning
* **Optimal Threshold:** Calibrated at **0.40** to balance capturing 3 out of 4 depositors while reducing total calls by 45%.
* **Recall Improvement:** Increased from 71% (base) to **75%** after tuning.

## 📈 Business Impact Evaluation
Comparing the **Targeted Strategy (Threshold 0.40)** vs. the standard **Call All Strategy**:

| Metric | Call All Strategy | Targeted Strategy |
| :--- | :--- | :--- |
| Total Daily Calls | 7,813 | 4,296 |
| Depositors Captured | 3,732 (100%) | 2,793 (75%) |
| Operational Call Cost | $781 | $430 |
| Staff Required | 87 agents | 48 agents |
| **TOTAL DAILY COST** | **$17,258** | **$10,602** |

## 💡 Key Business Insights (SHAP Analysis)
* **Unknown Contact Channel:** The strongest negative predictor; verified contact methods are crucial for success.
* **Housing Loans:** Customers with existing housing loans are less likely to subscribe due to existing financial commitments.
* **Previous Success:** If a customer converted in a previous campaign, they are significantly more likely to convert again.
* **Account Balance:** Higher-balance customers show a stronger propensity to subscribe.

## 🚀 Strategic Recommendations
1. **Tiered Outreach:** Segment leads by probability scores; use senior agents for High Certainty leads (>0.80) and low-cost automation for Priority 3 leads (<0.40).
2. **Seasonal Scheduling:** Focus high-intensity campaigns in **March, September, October, and December** (historically highest conversion).
3. **Data Quality Program:** Invest in KYC to verify contact data, as "Unknown" contact types significantly reduce success rates.
4. **Retention focus:** Prioritize repeat engagement for customers who have successfully converted in the past.

---
*Created as part of Capstone Project III. Full details can be found in `bank_marketing_ml_presentation.pdf`.*---
*Created as part of Capstone Project III.*
