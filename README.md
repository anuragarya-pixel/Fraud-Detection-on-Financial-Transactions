# 🕵️ Fraud Detection on Financial Transactions Using Machine Learning

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Classifier-0E7C86)
![LightGBM](https://img.shields.io/badge/LightGBM-Classifier-1B2A41)

This project walks through an end-to-end exploratory data analysis of financial transaction records, with the aim of identifying the behavioural patterns that set fraudulent users apart from genuine ones. Drawing on those patterns, a machine learning model is then built to detect fraud automatically from historical data.

---

## 📑 Table of Contents

- [Data Analysis](#-data-analysis)
- [Feature Engineering](#-feature-engineering)
- [Project Structure](#-project-structure)
- [Technologies Used](#-technologies-used)
- [Model Building & Evaluation](#-model-building--evaluation)
- [Upcoming Improvements](#-upcoming-improvements)
- [Conclusion](#-conclusion)
- [Author](#-author)

---

## 📊 Data Analysis

### 🗂️ Dataset Overview

- **File:** `SOI_2025_Dataset.csv`
- **Target column:** `fraud_bool` (0 = Legit, 1 = Fraud)
- **Features analyzed:**
  - `credit_risk_score`, `bank_branch_count_8w`, `device_distinct_emails_8w`
  - `foreign_request`, `month`, `session_length_in_minutes`, `payment_type`
  - `prev_address_months_count`, `current_address_months_count`
  - `total_relationship_count`, `income`

### 🔍 Key Insights & Findings

| Factor | Observation |
|---|---|
| **Credit Risk Score** | Fraudulent users showed **surprisingly high credit scores**, which may point to **synthetic identities** or stolen identities. |
| **Bank Branch Usage** | Fraudsters visited fewer branches, hinting at **online-only** or **short-lived accounts**. |
| **Device–Email Mapping** | A single device tied to many email addresses suggests **account farming** or **bot activity**. |
| **Foreign Requests** | Requests with `foreign_request = 1` carried a higher fraud rate, making them valuable for **geolocation profiling**. |
| **Monthly Trend** | Fraud peaked in **Month 7 (July)**, possibly because of seasonal effects or reporting cycles. |
| **Session Length** | Fraudulent sessions were **brief**, consistent with **automated** or **scripted** behaviour. |
| **Device OS** | Fraud was more common on **Windows**, potentially because botnets and attack tools are easier to run there. |
| **Keep-Alive Sessions** | `keep_alive_session = 0` appeared often among fraud cases, signalling **non-persistent** sessions. |
| **Address Stability** | Many fraudsters had **missing or short residence durations**, which makes identity verification difficult. |
| **Income Trends** | **Low or missing income values** were slightly over-represented in fraud, suggesting **fabricated profiles**. |
| **Total Relationships** | Few relationships point to new, temporary or fake accounts being used for fraud. |
| **Payment Types** | Prepaid and anonymous cards recorded higher fraud rates. |

### 📈 Visualizations Included

- Boxplots, bar charts and countplots showing fraud patterns across:
  - Month, OS, payment type, device type, foreign requests, etc.
- Embedded in: [`data_analysis.ipynb`](./notebooks/01_data_analysis.ipynb)

---

## 🧱 Feature Engineering

### 🏠 Address Stability

- `-1` replaced with column medians for `prev_address_months_count`, `current_address_months_count`

### 💳 Encoded Categorical Features

- Label-encoded: `payment_type`, `employment_type`, `device_os`, etc.
- Saved mappings to `mappings.json`

### 🚀 Velocity Risk Features

- Transformed: `velocity_6h`, `velocity_8h`, `velocity_1w` with log scaling
- Created `velocity_risk_score` using weighted score map

### ✏️ Data Standardization

- Features normalized or scaled

### 🧪 Train-Test Split

- Used `train_test_split` to prepare model datasets

📓 Code in: [`feature_Engineering.ipynb`](./notebooks/02_feature_engineering.ipynb)

---

## 📁 Project Structure

```text
fraud_detect/
├── data/
│   └── SOI_2025_Dataset.csv
├── notebooks/
│   ├── 01_data_analysis.ipynb
│   ├── 02_feature_engineering.ipynb
│   ├── logistic_model.ipynb
│   ├── lightGBM.ipynb
│   └── XG_boost_part2.ipynb
├── mappings/
│   ├── mappings.json
│   └── weight_map(2).json
├── models/                  # Saved models
├── plots/
├── requirements.txt
├── README.md
└── .gitignore
```

---

## ⚙️ Technologies Used

- 🐍 Python 3.x, JSON
- 📊 Pandas, NumPy, Scikit-learn, XGBoost, LightGBM
- 🎨 Matplotlib, Seaborn
- 🧠 Jupyter Notebook

---

## 🤖 Model Building & Evaluation

### 1️⃣ Logistic Regression

- `sklearn.linear_model.LogisticRegression`
- Scaled numeric + encoded categorical features
- 📈 ROC Curve, Confusion Matrix, F1-score
- 📓 [`logistic_model.ipynb`](./notebooks/logistic_model.ipynb)

### 2️⃣ XGBoost Classifier

- `xgboost.XGBClassifier`
- Tuned parameters, tree ensembles
- Feature importance plots
- 📓 [`XG_boost_part2.ipynb`](./notebooks/XG_boost_part2.ipynb)

### 3️⃣ LightGBM Classifier

- `lightgbm.LGBMClassifier`
- Faster gradient boosting
- 📓 [`lightGBM.ipynb`](./notebooks/lightGBM.ipynb)

---

## 🔧 Upcoming Improvements

- Cross-validation for robustness
- Better handling of imbalance via:
  - `class_weight='balanced'`
  - SMOTE, undersampling
- Model ensembling to boost recall

---

## 🧠 Conclusion

This project examined fraudulent financial behaviour through exploratory analysis, feature engineering and predictive modelling. The results underline how much precision, interpretability and careful class balancing matter in practical fraud detection. With further refinement, the models can generalise better and move closer to production readiness.

---

## 👤 Author

**Anurag Arya**
🎓 B.Tech @ IIT Delhi
📬 GitHub: [https://github.com/anuragarya-pixel]
📨 Email: [ch1240765@iitd.ac.in](mailto:ch1240765@iitd.ac.in)
