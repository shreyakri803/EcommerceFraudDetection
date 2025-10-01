# EcommerceFraudDetection
📝 Problem Statement-
E-commerce platforms face a significant challenge in safeguarding against fraudulent transactions. These fraudulent activities not only lead to financial losses but also erode customer trust. Since fraud accounts for a small percentage of overall transactions (~5%), the dataset is highly imbalanced.

The challenge is to:
* Detect fraudulent transactions accurately.
* Minimize false negatives (missed frauds).
* Avoid too many false positives (blocking genuine users).

🎯 Objective / Solution Approach
The solution involves building a fraud detection system that can:
* Extract and preprocess data using Python.
* Engineer advanced features that capture suspicious behaviors.
* Handle imbalanced data effectively.
* Train and evaluate machine learning models with a focus on precision & recall trade-off.
* Provide interpretable insights into fraud patterns (feature importance, distribution analysis).

  -----------
  
📊 Dataset Summary
* Shape:23,634 rows × 16 columns
* Data Types:
  * Categorical (object): Transaction ID, Customer ID, Transaction Date, Payment Method, Product Category, Customer Location, Device Used, IP Address, Shipping Address, Billing Address
  * Numeric (float/int): Transaction Amount, Quantity, Customer Age, Account Age Days, Transaction Hour, Is Fraudulent

---

🔍 Key Statistics

| Feature            | Mean   | Std Dev | Min   | 25%   | 50%    | 75%    | Max     |
| ------------------ | ------ | ------- | ----- | ----- | ------ | ------ | ------- |
| Transaction Amount | 229.37 | 282.05  | 10.00 | 69.07 | 151.41 | 296.13 | 9716.50 |
| Quantity           | 3.00   | 1.42    | 1     | 2     | 3      | 4      | 5       |
| Customer Age       | 34.56  | 10.00   | -2    | 28    | 35     | 41     | 73      |
| Account Age Days   | 178.66 | 107.38  | 1     | 84    | 178    | 272    | 365     |
| Transaction Hour   | 11.27  | 6.98    | 0     | 5     | 11     | 17     | 23      |

✅ Data Quality Notes
* No missing values in any column.
* Customer Age anomaly: Some negative values (likely data entry errors).
* Transaction Amount: Right-skewed with large outliers (up to $9716).
* Categorical Uniqueness:
  * Customer IDs: 23,634 unique
  * Payment Methods: 4
  * Product Categories: 5
  * Devices: 3
  * Customer Locations: ~14,868 unique
---
🎯 Target Variable (`Is Fraudulent`)

* **0 → Genuine transactions:** 94.83%
* **1 → Fraudulent transactions:** 5.17%
* **Class Imbalance:** The dataset is highly imbalanced, requiring special handling (SMOTE, class weighting, threshold tuning)
------------------------------------------------------------------------------------------------------------------------------


🛠️ Project Pipeline: SQL Extraction → Preprocessing → Feature Engineering → Handling Imbalance → Modeling → Evaluation → Insights & Deployment.

📚 Libraries & Tools
* Data Handling: pandas, numpy
* Visualization: matplotlib, seaborn
* Machine Learning: scikit-learn, xgboost, imblearn (for SMOTE)
* Metrics & Evaluation: sklearn.metrics (classification_report, confusion_matrix)

Insights & Takeaways
* Fraudulent patterns often linked to:
* High-value transactions.
* Transactions at odd hours.
* New or low-account-age customers.
* Address mismatches.


## 📈 Results

---

### **1. Baseline: Random Forest Classifier**

* **Accuracy:** 97%
* **Fraud Precision:** 95%
* **Fraud Recall:** 36%
* **Fraud F1-score:** 52%
* **Observation:**
  * Model was good at identifying fraud when flagged (high precision).
  * However, it missed most fraudulent cases (low recall → many false negatives).

---

### **2. Random Forest (with Class Weights)**
* **Accuracy:** ~96%
* **Fraud Precision:** ~80%
* **Fraud Recall:** ~55%
* **Fraud F1-score:** ~65%
* **Observation:**
  * Using `class_weight='balanced'` improved recall slightly.
  * Still not enough for production-level fraud detection.

---

### **3. XGBoost (Baseline)**
* **Accuracy:** 96–97%
* **Fraud Precision:** ~88%
* **Fraud Recall:** ~60%
* **Fraud F1-score:** ~71%
* **Observation:**
  * Better balance between precision and recall than Random Forest.
  * More effective in capturing nonlinear fraud patterns.

---

### **4. XGBoost + SMOTE Oversampling**
* **Accuracy:** 95–96%
* **Fraud Precision:** ~83%
* **Fraud Recall:** ~74%
* **Fraud F1-score:** ~78%
* **Observation:**
  * Oversampling fraud cases improved recall significantly.
  * F1-score for fraud improved → fewer missed frauds.

---

### **5. XGBoost + SMOTE + Threshold Tuning** ✅ **(Best Model)**
* **Accuracy:** ~95%
* **Fraud Precision:** ~80%
* **Fraud Recall:** ~85%
* **Fraud F1-score:** ~82%
* **Observation:**
  * Tuned decision threshold to prioritize fraud detection.
  * Best trade-off: high recall with decent precision.
  * Much fewer false negatives (critical for fraud detection).

---

## 🎯 Key Takeaways

* **Random Forest:** High accuracy but poor fraud recall.
* **XGBoost (baseline):** Better balance between fraud precision & recall.
* **XGBoost + SMOTE + Threshold Tuning:** Best overall → strong recall (85%) with good precision.

✅ Final Model Selected: **XGBoost with SMOTE + Threshold Tuning**
⚡ Because in fraud detection, **catching more fraudulent cases (high recall)** is more important than slightly lowering precision.

flowchart LR
    A[Data Source (CSV)] --> B[Data Extraction (Pandas)]
    B --> C[Data Preprocessing (Cleaning, Encoding, Feature Engineering)]
    C --> D[Handle Class Imbalance (SMOTE, Class Weights)]
    D --> E[Model Training (Random Forest, XGBoost)]
    E --> F[Model Evaluation (Precision, Recall, F1, Confusion Matrix)]
    F --> G[Insights & Deployment Readiness]

---

## ✅ Conclusion & Future Work

### **Conclusion**
* Built an end-to-end pipeline for **e-commerce fraud detection** using **SQL + Python**.
* Explored and analyzed **23,634 transactions** with 16 features.
* Identified key challenges: **class imbalance (5% fraud)**, **outliers**, and **anomalous values** (e.g., negative ages).
* Designed **feature engineering** to capture suspicious behavior:
  * Address mismatches
  * Odd-hour and weekend transactions
  * High-value transactions
  * Customer behavior & transaction velocity
* **Baseline model (Random Forest):** High precision but low recall for fraud.
* **Improved model (XGBoost + SMOTE + threshold tuning):** Better fraud recall while keeping precision strong.
* Delivered insights into **patterns that indicate fraud**, helping improve trust and security in e-commerce.

---

### **Future Work**
* 🔹 **Anomaly Detection Models:** Explore Isolation Forest, One-Class SVM for rare fraud signals.
* 🔹 **Deep Learning Approaches:** Use LSTMs for sequential transaction patterns or Autoencoders for anomaly detection.
* 🔹 **Real-Time Fraud Detection:** Deploy pipeline with streaming data (Kafka, Spark, or AWS Kinesis).
* 🔹 **Explainability:** Apply SHAP or LIME to explain model predictions to business stakeholders.
* 🔹 **Integration with Business Rules:** Combine ML predictions with rule-based systems (e.g., flagging transactions over certain thresholds).
* 🔹 **Continuous Learning:** Automate model retraining as new fraud strategies emerge.
