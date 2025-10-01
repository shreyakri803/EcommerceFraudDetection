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
